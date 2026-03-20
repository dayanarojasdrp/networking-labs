# LAB 04 – Cloud Networking (AWS, Azure, GCP)

# AWS Networking

## Virtual Private Cloud (VPC)
A VPC is a logically isolated network within AWS. It defines the IP address range and provides the foundation for deploying subnets, route tables, gateways, and security controls.

## Public vs Private Subnets
- **Public Subnet**: Associated with a route table that points to the Internet Gateway (IGW). Instances in this subnet can receive inbound traffic from the internet if they have a public IP.
- **Private Subnet**: Associated with a route table that points to the NAT Gateway. Instances in this subnet cannot be reached directly from the internet, but they can initiate outbound connections through the NAT Gateway.

## Route Tables
- **Public Route Table**: Contains a default route (`0.0.0.0/0`) pointing to the IGW, enabling internet access for public resources.
- **Private Route Table**: Contains a default route (`0.0.0.0/0`) pointing to the NAT Gateway, allowing private instances to access the internet without being exposed.

## Internet Gateway (IGW) and NAT Gateway
- **Internet Gateway (IGW)**: Connects the VPC to the internet, enabling inbound and outbound traffic for public subnets.
- **NAT Gateway**: Deployed in a public subnet, it allows instances in private subnets to access the internet for updates or external services, while preventing inbound connections from the internet.

## Security Groups
Security Groups are stateful firewalls applied directly to EC2 instances. They control inbound and outbound traffic at the instance level.

### Example Rules
- **Web Server SG (Public Subnet)**:
  - Allow inbound HTTP (TCP/80) from `0.0.0.0/0`
  - Allow inbound HTTPS (TCP/443) from `0.0.0.0/0`
  - Allow inbound SSH (TCP/22) only from a trusted IP (e.g., your workstation)
- **Database SG (Private Subnet)**:
  - Allow inbound MySQL (TCP/3306) only from the Web Server SG
  - Deny all inbound traffic from the internet

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


## 4. GCP Networking
### 4.1 VPC Diagram
### 4.2 Subnets (Regional)
### 4.3 Firewall Rules
### 4.4 Cloud Router / Cloud NAT
### 4.5 Example: VPC Peering
### 4.6 Example: GCP Load Balancer

## 5. Cloud Networking Comparison (AWS vs Azure vs GCP)
### 5.1 VPC/VNet Model
### 5.2 Subnet Model
### 5.3 Routing
### 5.4 NAT
### 5.5 Firewalls
### 5.6 Load Balancers

## 6. Traffic Flow Examples
### 6.1 AWS Traffic Flow
### 6.2 Azure Traffic Flow
### 6.3 GCP Traffic Flow

## 7. Conclusions
