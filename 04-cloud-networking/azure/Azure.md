
## Differences with AWS
- **VNet vs VPC**: Conceptually similar, but Azure VNets are regional and can be peered across regions more easily.
- **NSG vs Security Group**: NSGs can be applied at both subnet and NIC level, while AWS SGs are only applied at the instance level.
- **Azure Firewall vs AWS Security Groups/NACLs**: Azure Firewall provides centralized, managed protection, whereas AWS relies on SGs (instance-level) and NACLs (subnet-level).
- **NAT Gateway**: Both AWS and Azure use NAT Gateways for outbound internet access from private subnets, but Azure integrates NAT Gateway as a separate resource linked to the subnet.
