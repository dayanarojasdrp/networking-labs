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


## 3. Azure Networking
### 3.1 VNet Diagram
### 3.2 Subnets
### 3.3 NSG
### 3.4 Azure Firewall
### 3.5 Route Tables (UDR)
### 3.6 Example: VNet Peering
### 3.7 Example: Azure Load Balancer

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
