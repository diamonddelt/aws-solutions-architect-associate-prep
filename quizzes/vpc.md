# VPC Quiz

1. True or False: You can accelerate your application by adding a second Internet Gateway to your VPC.
    - `False` - you can only have one internet gateway per VPC
2. You have just created a 2nd VPC and launched an EC2 instance in a subnet of that VPC. You want this instance to be publicly available, but you forgot to assign a public IP address during creation. How might you make your instance reachable from the outside world?
    - `Create an Internet gateway and an Elastic IP address. Associate the Elastic IP with the EC2 instance.` An IGW is provided by default in a default VPC, but not in a manually created VPC. A Public IP address is needed, and of the options provided an EIP is the best option
3. Is this statement true: Security Groups are stateful and Network Access Control Lists are stateless.
    - Yes, `SGs are stateful` (open traffic both ways), while `NACLs are stateless` (have to specify each way)
4. At which of the following levels can VPC Flow Logs be created? (Choose 3)
    - `VPC`, `Subnet`, and `Network Interface` level
5. Security groups act like a firewall at the instance level, whereas _________ are an additional layer of security that act at the subnet level
    - Network ACL
6. Which of the following is a chief advantage of using VPC endpoints to connect your VPC to services such as S3?
    - Traffic between your VPC and the other service `does not leave the Amazon network.` In contrast to a NAT gateway, traffic between your VPC and the other service does not leave the Amazon network when using VPC endpoints.
7. What is the purpose of an Egress-Only Internet Gateway? (Choose 2)
    - `Prevents IPv6 based Internet resources initiating a connection into a VPC`
    - Allows `VPC based IPv6 traffic to communicate to the Internet`
    - The purpose of an "Egress-Only Internet Gateway" is to allow IPv6 based traffic within a VPC to access the Internet, whilst denying any Internet based resources the possibility of initiating a connection back into the VPC. With this in mind, the latter two options are correct. The first two options cannot be correct as it does not support IPv4 data communication nor does it allow a Security Group to be associated with it. 
8. By default, how many VPCs am I allowed in each AWS Region?
    - `5`
9. Which of the following offers the largest range of internal IP addresses?
    - `/16` - The /16 offers 65,536 possible addresses.
10. True or False: An Application Load Balancer must be deployed into at least two subnets.
    - `True`
11. By default, instances in new subnets in a custom VPC can communicate with each other across Availability Zones.
    - `True` - In a custom VPC with new subnets in each AZ, there is a `Route that supports communication across all subnets/AZs`. Plus a `Default SG with an allow rule 'All traffic, All protocols, All ports, from anything using this Default SG'`
12. When you create a custom VPC, which of the following are created automaticaly? (Choose 3)
    - `Security Group`
    - `Network Access Control List`
    - `Route Table`
    - When you create a custom VPC, a default Security Group, Access control List, and Route Table are created automaticaly. You must create your own subnets, Internet Gateway, and NAT Gateway (if you need one.)
13. Which of the following are true for Security Groups? (Choose 3)
    - `Security Groups operate at the instance level.`
    - `Security Groups support "allow" rules only.`
    - `Security Groups evaluate all rules before deciding whether to allow traffic.`
14. A VPN connection consists of which of the following components? (Choose 2)
    - `Virtual Private Gateway and Customer Gateway` (representing both sides of the VPN connection)
15. In a default VPC, all Amazon EC2 instances are assigned 2 IP addresses at launch. What are they?
    - A Private IP Address & Public IP Address
16. In Amazon VPC, does an instance retain its private IP?
    - `No`, it does not. When an instance is torn down and spun up again, it is always given a randomly allocated private IP within the range left.
17. Are you permitted to conduct your own vulnerability scans on your own VPC without alerting AWS first?
    - `No`, you must let AWS know before you do a `vulnerability` to load test on an instance
18. How many internet gateways can I attach to my custom VPC?
    - `1` - whether it's default or custom, `only one internet gateway per VPC`
19. VPC stands for
    - `Virtual Private Cloud`
20. Which of the following allows you to SSH or RDP into an EC2 instance located in a private subnet?
    - `Bastion Host`
21. When I create a new security group, all outbound traffic is allowed by default.
    - `True`
22. True or False: A subnet can span multiple Availability Zones.
    - `False` - Each subnet must reside entirely within one Availability Zone and cannot span zones.
23. You have five VPCs in a 'hub and spoke' configuration, with VPC 'A' in the center and individually paired with VPCs 'B', 'C', 'D', and 'E', which make up the 'spokes'. There are no other VPC connections. Which of the following VPCs can VPC 'B' communicate with directly?
    - VPC 'A' only - because `transitive peering` is not allowed when peering VPCs.
24. When peering VPCs, you may peer your VPC only with another VPC in your same AWS account.
    - `False` - You may peer a VPC to another VPC that's `in your same account`, or to `any VPC in any other account`.