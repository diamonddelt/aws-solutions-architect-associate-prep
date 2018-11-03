# VPC

## What is VPC Peering and why should I care?

VPC Peering is a connection betwen two VPCs that enables you to route traffic between them using private IP addresses. Without peering, the only way you could do this would be to address them over public IPs. Once peered, each VPC sees the other as if its within its own private network.

You can peer any two VPCs as long as they are within a single `region`.

A VPC peering connection `does not act like a gateway or a VPN connection - it uses the existing VPC infrastructure already in place`. There is no single point of failure or bandwidth bottleneck when two VPCs are peered.

## Important VPC Peering Notes

1. You cannot peer two VPCs which have the same subnet class and CIDR block configuration - for example, `you cannot peer a 10.0.0.0/16 CIDR block VPC with a 10.0.0.0/24 CIDR block VPC.`
2. Transitive Peering is NOT supported, meaning if you Peer VPC A -> VPC B, and VPC B -> VPC C, VPC A `cannot` communicate with VPC C. You can only communicate between two directly peered VPCs
3. You cannot create a peering connection in `two different regions.`