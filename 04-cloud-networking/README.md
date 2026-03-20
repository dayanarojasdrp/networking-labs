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
In Google Cloud Platform (GCP), the VPC is **global**, meaning a single VPC can span multiple regions. Subnets are **regional**, and resources are deployed within them. The diagram shows:
- A global VPC (`10.0.0.0/16`)
- Public Subnet (`10.0.1.0/24`) with a Web Server
- Private Subnet (`10.0.2.0/24`) with a Database Server
- Firewall Rules applied at the VPC level
- Cloud NAT for outbound traffic from the private subnet

### 4.2 Subnets (Regional)
- **Public Subnet**: Instances can have public IPs and connect directly to the Internet.
- **Private Subnet**: Instances have only private IPs and cannot connect directly to the Internet. Outbound traffic is routed through Cloud NAT.

### 4.3 Firewall Rules
Firewall rules in GCP are applied to the **entire VPC**, not individual instances. They are defined by protocol, port, source/destination IP, and instance tags.
- Example rules:
  - Allow HTTP/HTTPS from `0.0.0.0/0` to Web Server
  - Allow MySQL (tcp:3306) only from Web Server tag to Database Server
  - Allow SSH only from a trusted admin IP

### 4.4 Cloud Router / Cloud NAT
- **Cloud Router**: Provides dynamic routing between on-premises and GCP networks.
- **Cloud NAT**: Allows instances in private subnets to initiate outbound connections to the Internet without exposing them to inbound traffic.

### 4.5 Example: VPC Peering
VPC Peering in GCP connects two VPCs privately without using public IPs or VPN. Traffic flows internally across Google’s backbone network.
- Example: Peering between `VPC-A (10.0.0.0/16)` and `VPC-B (192.168.0.0/16)` allows private communication between instances in both networks.

### 4.6 Example: GCP Load Balancer
GCP offers several types of load balancers:
- **HTTP(S) Load Balancer**: Global, distributes traffic across regions.
- **TCP/UDP Load Balancer**: Regional, for non-HTTP workloads.
- **Internal Load Balancer**: Balances traffic within a VPC for private applications.
Example: A global HTTP(S) Load Balancer distributing traffic to multiple Web Servers across different regions.


## 5. Cloud Networking Comparison (AWS vs Azure vs GCP)

### 5.1 VPC/VNet Model
- **AWS**: VPC is regional, each region has its own VPCs.
- **Azure**: VNet is regional, scoped to a specific region.
- **GCP**: VPC is global, can span multiple regions.

### 5.2 Subnet Model
- **AWS**: Subnets are regional, tied to Availability Zones.
- **Azure**: Subnets are regional, defined within a VNet.
- **GCP**: Subnets are regional, but belong to a global VPC.

### 5.3 Routing
- **AWS**: Route tables per subnet, explicit association required.
- **Azure**: System routes by default, User Defined Routes (UDR) for customization.
- **GCP**: One route table per VPC, applies to all subnets.

### 5.4 NAT
- **AWS**: NAT Gateway or NAT Instance for private subnets.
- **Azure**: NAT Gateway for outbound Internet access from private subnets.
- **GCP**: Cloud NAT provides outbound Internet access for private subnets.

### 5.5 Firewalls
- **AWS**: Security Groups (instance-level, stateful) and NACLs (subnet-level, stateless).
- **Azure**: NSGs (subnet or NIC-level) and Azure Firewall (centralized).
- **GCP**: Firewall Rules applied at the VPC level, using tags to target instances.

### 5.6 Load Balancers
- **AWS**: ALB (HTTP/HTTPS), NLB (TCP/UDP), CLB (classic).
- **Azure**: Azure Load Balancer (Layer 4), Application Gateway (Layer 7).
- **GCP**: Global HTTP(S) Load Balancer, TCP/UDP Load Balancer, Internal Load Balancer.

---

## 6. Traffic Flow Examples

### 6.1 AWS Traffic Flow
- Public Subnet → Internet Gateway → Internet
- Private Subnet → NAT Gateway → Internet
- Internal traffic flows via local routes within the VPC.

### 6.2 Azure Traffic Flow
- Public Subnet → Internet via default system route
- Private Subnet → NAT Gateway or Azure Firewall → Internet
- Internal traffic controlled by NSGs and UDRs.

### 6.3 GCP Traffic Flow
- Public Subnet → Internet (VM with public IP + default route)
- Private Subnet → Cloud NAT → Internet (outbound only)
- Internal traffic controlled by Firewall Rules applied at the VPC level.

---

## 7. Conclusions
- **AWS**: Strong regional isolation, granular control with SGs and NACLs.  
- **Azure**: Flexible NSGs and centralized Azure Firewall, good hybrid integration.  
- **GCP**: Simplified global VPC model, firewall rules applied at VPC level, Cloud NAT for private subnets.  

Overall, all three clouds provide similar building blocks (VPC/VNet, subnets, routing, NAT, firewalls, load balancers), but the **scope and implementation differ**:
- AWS and Azure are **regional-first**.  
- GCP is **global-first**.  
- Security models vary: instance-level (AWS), subnet/NIC-level (Azure), VPC-level (GCP).  

