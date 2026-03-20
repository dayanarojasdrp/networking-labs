# Azure Networking

## Virtual Network (VNet)
An Azure VNet is the fundamental building block of networking in Azure. It defines the IP address space and provides logical isolation for resources, similar to an AWS VPC.

## Public vs Private Subnets
- **Public Subnet**: Associated with a route to the Internet via the Azure Internet Gateway. Instances in this subnet can receive inbound traffic if they have a public IP.
- **Private Subnet**: Instances in this subnet cannot be reached directly from the internet. Outbound traffic can be routed through Azure NAT Gateway or Azure Firewall.

## Network Security Groups (NSG)
NSGs are stateful firewalls applied at the subnet or NIC (Network Interface Card) level. They control inbound and outbound traffic using rules based on source/destination IP, port, and protocol.

### Example NSG Rules
- **Web Server NSG (Public Subnet)**:
  - Allow inbound HTTP (TCP/80) from `Any`
  - Allow inbound HTTPS (TCP/443) from `Any`
  - Allow inbound SSH (TCP/22) only from a trusted IP
- **Database NSG (Private Subnet)**:
  - Allow inbound SQL (TCP/1433) only from the Web Server NSG
  - No inbound traffic allowed directly from the internet

## Azure Firewall
Azure Firewall is a managed, cloud-based network security service. It provides centralized control over traffic entering and leaving the VNet.
- Can filter traffic based on application rules (FQDNs, domains).
- Supports logging and monitoring for compliance.
- Complements NSGs by providing network-wide protection.

## Route Tables
- **Public Route Table**:
  - `10.0.0.0/16 → Local`
  - `0.0.0.0/0 → Internet Gateway`
- **Private Route Table**:
  - `10.0.0.0/16 → Local`
  - `0.0.0.0/0 → NAT Gateway or Azure Firewall`

## Differences with AWS
- **VNet vs VPC**: Conceptually similar, but Azure VNets are regional and can be peered across regions more easily.
- **NSG vs Security Group**: NSGs can be applied at both subnet and NIC level, while AWS SGs are only applied at the instance level.
- **Azure Firewall vs AWS Security Groups/NACLs**: Azure Firewall provides centralized, managed protection, whereas AWS relies on SGs (instance-level) and NACLs (subnet-level).
- **NAT Gateway**: Both AWS and Azure use NAT Gateways for outbound internet access from private subnets, but Azure integrates NAT Gateway as a separate resource linked to the subnet.
