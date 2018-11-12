# VPC

A VPC is a `virtual data center` in the cloud. Every region has a `default VPC`.

VPCs allow you to create the following:

- VPN connections
- Virtual Private Gateways
- Route Tables, Subnets, conforming to common IP CIDR block standards
- Security Groups and Network Access Control Lists (NACLs)

Traffic flows into an EC2 instance in one of two possible paths:

1. Internet Gateway -> AWS VPC Router -> VPC Route Table -> Network ACL -> Subnet and associated security group(s) -> Public Instance (with public subnet CIDR block)
2. Virtual Private Gateway -> AWS VPC Router -> VPC Route Table -> Network ACL -> Subnet and associated security group(s) -> Private Instance (with private subnet CIDR block)

*One subnet always equals one availability zone*

There is a _soft_ limit of 5 possible VPCs in a given region, but you can email AWS and ask for an increase.

## Possible CIDR block ranges

When creating a VPC, you can one three possible private-network subnet classes / network IP ranges

- 10.0.0.0 - 10.255.255.255 (10/8 prefix)
- 172.16.0.0 - 172.31.255.255 (172.16/12 prefix)
- 192.168.0.0 - 192.168.255.255 (192.168/16 prefix)

## Differences between default VPC and a custom VPC

1. The default VPC is user friendly and allows you script out or immediately deploy things into it with much less effort and configuration (i.e. if you don't specify which VPC to use, the default VPC is inferred)
2. `All subnets in the default VPC have a route out to the internet`; you don't have to worry about setting that up or misconfiguring it
3. Each EC2 instance has both a public and a private IP address

## NAT Instances & NAT Gateways

- *NAT Instance* - This is just an `EC2 instance` which you put into a `public subnet`, whose sole purpose is to route traffic through, to `protect other AWS resources in private subnets from public WAN traffic`. 

You enable the traffic routing through the NAT instance by setting up the VPC route table entry for private subnets or the default route table to route `0.0.0.0/0` traffic through the NAT instance, instead of the Internet Gateway.

When setting up a NAT instance, `you must disable source/destination checks`, because the NAT instance is never going to be a source or destination of traffic, but rather a middleman. _NAT instances are almost completely deprecated in favor of NAT Gateways._

The question then becomes: _Why are NAT Instances bad?_ The answer is the amount of bottlenecks it introduces. 

```text
- If you use a single NAT instance to funnel all traffic from all private subnets through, you could instantly saturate the amount of bandwidth enabled on the instance type.
- If the NAT instance dies, all of the WAN connectivity dies with it.
- It is in a single AZ, and is not highly available.
- You cannot automatically scale it, because adding new NAT instances requires manual updates to the route table entries on the VPC.
- You are responsible for patching and protecting the NAT instance from viruses and malware, vs. AWS handling it for you with NAT Gateways
- You have to place a NAT instance behind a security group - with NAT Gateways, you don't have to do this.
```

One of the few benefits of rolling your own NAT Instance is that `you can also use it as a bastion server (jump box).`

- *NAT Gateway* - These operate on IPv4 only. You can setup an `Egress Only Internet Gateway` which works with IPv6. You still need to place a NAT Gateway in a public subnet, and you also need to allocate an elastic IP address to it. This is to allow AWS to scale it automatically, but let you point all of your traffic at a single IPv4 endpoint. They also scale traffic egressing out of them `up to 10Gbps`

You do need to` create a NAT Gateway in each availability zone - they do not span AZs`.

## Importance of a Bastion Server

1. A `bastion` (otherwise known as a jumpbox), is important because it is a single DMZ which acts a link between instances in a private subnet (segregated from public internet access), and a public subnet. These are commonly used to route traffic through, so the instances in the private subnet can make outbound connections to the internet (to do things like update, patch, or download files), but the bastion restricts traffic the other way.

## What is VPC Peering and why should I care?

VPC Peering is a connection betwen two VPCs that enables you to route traffic between them using private IP addresses. Without peering, the only way you could do this would be to address them over public IPs. Once peered, each VPC sees the other as if its within its own private network.

You can peer any two VPCs as long as they are within a single `region`.

A VPC peering connection `does not act like a gateway or a VPN connection - it uses the existing VPC infrastructure already in place`. There is no single point of failure or bandwidth bottleneck when two VPCs are peered.

## Network ACLs vs. Security Groups

1. Network ACLs are associated with a VPC, therefore, any VPC can only have `one` Network ACL. This means the network ACL has to be generic enough to stack on top of security groups and individual subnets within the VPC.
2. The *DEFAULT* network ACL that comes with the default VPC `allows all inbound and outbound traffic`
3. When you create a new *CUSTOM* network ACL, the `default rules are to deny all inbound and outbound traffic`. Therefore, network ACLs are `stateless` and are configured on the principle of `deny first`
4. Rules allowing or denying traffic are evaluated `in numerical order`, meaning that _rule 100 takes priority over rule 101, if rule 100 allows HTTP traffic and rule 101 denies it_
5. Network ACLs are inspected and evaluated `BEFORE` security groups, so if you implement custom Network ACLs, make sure the rules make sense and do not conflict with security group rules, because they are applied first.

## Important VPC Peering Notes

1. You cannot peer two VPCs which have the same subnet class and CIDR block configuration - for example, `you cannot peer a 10.0.0.0/16 CIDR block VPC with a 10.0.0.0/24 CIDR block VPC.`
2. Transitive Peering is NOT supported, meaning if you Peer VPC A -> VPC B, and VPC B -> VPC C, VPC A `cannot` communicate with VPC C. You can only communicate between two directly peered VPCs
3. You cannot create a peering connection in `two different regions.`

## Exam Tips

1. You can only associate `one route table with a subnet`.
2. Every route table has a local route for communication within the VPC over IPv4 or IPv6. You cannot modify or delete these routes (they are created automatically)
3. You can only have `one internet gateway per VPC`
4. When you create a new VPC, it automatically creates a default route (Route Table), a default Security Group, and a default Network ACL, but `it will not create subnets for you`
5. When creating a subnet, the first four IP addresses and the last IP address is `NOT AVAILABLE FOR USE`. AKA each subnet `always loses 5 IP addresses`
    ```text
    - 1st - network address
    - 2nd - reserved by AWS for the VPC router
    - 3rd - reserved by AWS because the DNS server requires the base VPC network range plus 2
    - 4th - reserved by AWS for future use
    - Last - reserved network broadcast address
    ```
6. Creating a `custom internet gateway is detached when it's first created`
7. `Security Groups are tied to the VPC that they are created in`. You can't share a security group configuration among multiple VPCs.
8. The `default route table` which is created when you make a new VPC *automatically associates any subnets to be internet accessible*, which is one reason why you want to make a custom VPC if you want to mess with private subnets
9. Security Groups are `stateful`, while Network ACLs are `stateless` - meaning you have to specify inbound and outbound rules in an NACL, but a security groups assumes both inbound and outbound permissions when you open a port, for example
10. There is `no transitive peering` in VPCs
11. Network ACLs are `Stateless`, whereas Security Groups are `stateful`
12. You `can block specific IP addresses using Network ACLs`, but you can't do that with Security Groups
