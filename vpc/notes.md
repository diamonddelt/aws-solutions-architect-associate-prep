# VPC

A VPC is a `virtual data center` in the cloud. Every region has a `default VPC`.

VPCs allow you to create the following:

- VPN connections
- Virtual Private Gateways
- Route Tables, Subnets, conforming to common IP CIDR block standards

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

## What is VPC Peering and why should I care?

VPC Peering is a connection betwen two VPCs that enables you to route traffic between them using private IP addresses. Without peering, the only way you could do this would be to address them over public IPs. Once peered, each VPC sees the other as if its within its own private network.

You can peer any two VPCs as long as they are within a single `region`.

A VPC peering connection `does not act like a gateway or a VPN connection - it uses the existing VPC infrastructure already in place`. There is no single point of failure or bandwidth bottleneck when two VPCs are peered.

## Important VPC Peering Notes

1. You cannot peer two VPCs which have the same subnet class and CIDR block configuration - for example, `you cannot peer a 10.0.0.0/16 CIDR block VPC with a 10.0.0.0/24 CIDR block VPC.`
2. Transitive Peering is NOT supported, meaning if you Peer VPC A -> VPC B, and VPC B -> VPC C, VPC A `cannot` communicate with VPC C. You can only communicate between two directly peered VPCs
3. You cannot create a peering connection in `two different regions.`

## Exam Tips

1. You can only associate `one route table with a subnet`.
2. Every route table has a local route for communication within the VPC over IPv4 or IPv6. You cannot modify or delete these routes (they are created automatically)
3. You can only have `one internet gateway per VPC`