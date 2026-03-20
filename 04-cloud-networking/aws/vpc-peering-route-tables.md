# VPC Peering Route Tables

## VPC A Route Table
- 10.1.0.0/16 → Local
- 10.2.0.0/16 → VPC Peering Connection

## VPC B Route Table
- 10.2.0.0/16 → Local
- 10.1.0.0/16 → VPC Peering Connection

## Notes
- Each VPC must have a route to the other VPC's CIDR block pointing to the peering connection.
- These routes enable private communication between EC2 instances across VPCs.
- No internet access is provided through the peering connection.
- Peering does not support transitive routing: traffic cannot pass through one VPC to reach a third.
