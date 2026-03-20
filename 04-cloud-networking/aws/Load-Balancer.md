# AWS Load Balancer Architecture

## Internet Gateway
The Internet Gateway (IGW) connects the VPC to the internet. It allows inbound traffic from external clients to reach AWS resources that are associated with public subnets.

## Load Balancer (ALB/NLB)
The Load Balancer is deployed across public subnets. It receives inbound HTTP/HTTPS traffic from the IGW and distributes it to multiple EC2 instances.  
- Application Load Balancer (ALB): Layer 7, supports path-based and host-based routing.  
- Network Load Balancer (NLB): Layer 4, optimized for high performance and low latency.  

## Public Subnet
Instances in the public subnet can be directly registered with the Load Balancer. They may have public IPs and are accessible through the IGW.

## Private Subnet
Instances in the private subnet cannot be reached directly from the internet. However, they can still be registered as targets behind the Load Balancer.  
- The LB forwards traffic to them using private IP addresses.  
- Outbound traffic from these instances to the internet is routed through a NAT Gateway.  

## Route Tables
- **Public Route Table**:  
  - `10.0.0.0/16 → Local`  
  - `0.0.0.0/0 → IGW`  
- **Private Route Table**:  
  - `10.0.0.0/16 → Local`  
  - `0.0.0.0/0 → NAT Gateway`  

## Security Groups
Security Groups act as stateful firewalls applied to EC2 instances and the Load Balancer.  
- **Load Balancer SG**: Allows inbound HTTP (TCP/80) and HTTPS (TCP/443) from `0.0.0.0/0`.  
- **Web Server SG (Public Subnet)**: Allows inbound traffic only from the Load Balancer SG.  
- **Application/Database SG (Private Subnet)**: Allows inbound traffic only from the Web Server SG or the Load Balancer SG, depending on the architecture.  

## Benefits
- Distributes HTTP/HTTPS traffic across multiple instances.  
- Improves availability and scalability by balancing load.  
- Integrates with Security Groups to enforce access control.  
