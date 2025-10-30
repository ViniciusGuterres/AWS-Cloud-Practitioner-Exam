# AWS VPC (Virtual Private Cloud)

## What is AWS VPC?

AWS Virtual Private Cloud (VPC) is a **logically isolated network** within the AWS cloud where you can launch AWS resources in a virtual network that you define. VPC gives you complete control over your virtual networking environment, including IP address ranges, subnets, route tables, and network gateways.

**Key Concept:** VPC provides a secure, isolated section of the AWS cloud where you can launch resources in a virtual network that closely resembles a traditional network in your own data center, but with the benefits of AWS scalable infrastructure.

## Core Components

### 1. Subnets
**Definition:** A range of IP addresses within your VPC where you can place AWS resources

**Subnet Types:**
- **Public subnet** - Has a route to an Internet Gateway for internet access
- **Private subnet** - No direct route to the internet, resources remain private
- **Availability Zone specific** - Each subnet exists in exactly one AZ
- **CIDR blocks** - Define IP address ranges for each subnet

### 2. Internet Gateway (IGW)
**Definition:** A gateway that allows communication between your VPC and the internet

**Internet Gateway Features:**
- **Bidirectional access** - Enables inbound and outbound internet traffic
- **Highly available** - Redundant and horizontally scaled
- **One per VPC** - Each VPC can have only one Internet Gateway
- **Public IP requirement** - Resources need public IPs to communicate through IGW

### 3. Route Tables
**Definition:** Rules that determine where network traffic from subnets is directed

**Route Table Components:**
- **Local routes** - Automatically created for VPC internal communication
- **Custom routes** - Define paths to specific destinations
- **Subnet associations** - Each subnet must be associated with a route table
- **Main route table** - Default route table for the VPC

### 4. Security Groups
**Definition:** Virtual firewalls that control inbound and outbound traffic at the instance level

**Security Group Characteristics:**
- **Stateful** - Return traffic is automatically allowed
- **Allow rules only** - You can only specify allow rules, not deny rules
- **Instance level** - Applied to individual EC2 instances
- **Default deny** - All traffic is denied unless explicitly allowed

## Key Features ⭐ **EXAM FOCUS**

### Network Isolation and Security
- **Logical isolation** - Your VPC is isolated from other AWS customers
- **Multiple layers of security** - Security groups and NACLs provide defense in depth
- **Private IP addressing** - Use RFC 1918 private IP address ranges
- **Secure connectivity** - VPN and Direct Connect for hybrid connectivity

### Flexible Network Architecture
- **Multiple subnets** - Create public and private subnets across AZs
- **Custom IP ranges** - Choose your own IP address ranges (CIDR blocks)
- **Multiple connectivity options** - Internet, VPN, Direct Connect, VPC Peering
- **Scalable design** - Easily expand and modify network architecture

### High Availability and Fault Tolerance
- **Multi-AZ deployment** - Spread resources across multiple Availability Zones
- **Redundant gateways** - Internet Gateways are highly available by design
- **Elastic IP addresses** - Static public IP addresses that can move between instances
- **Load balancer integration** - Distribute traffic across multiple AZs

## VPC Networking Concepts

### Public vs Private Subnets
**Public Subnet:**
- Has a route to an Internet Gateway
- Resources can have public IP addresses
- Direct internet connectivity
- Suitable for web servers, load balancers

**Private Subnet:**
- No direct route to the internet
- Resources use private IP addresses only
- Access internet through NAT Gateway/Instance
- Suitable for databases, application servers

### CIDR Blocks
**Definition:** Classless Inter-Domain Routing notation for IP address ranges

**Common CIDR Examples:**
- **10.0.0.0/16** - Provides 65,536 IP addresses
- **172.16.0.0/12** - Provides 1,048,576 IP addresses
- **192.168.0.0/16** - Provides 65,536 IP addresses
- **10.0.1.0/24** - Provides 256 IP addresses (subnet example)

## Usage Examples

### Example 1: Basic VPC with Public and Private Subnets
```
VPC: 10.0.0.0/16

Public Subnet (us-east-1a): 10.0.1.0/24
- Web servers with public IPs
- Route to Internet Gateway

Private Subnet (us-east-1a): 10.0.2.0/24
- Database servers with private IPs only
- Route to NAT Gateway for outbound internet

Private Subnet (us-east-1b): 10.0.3.0/24
- Application servers for high availability
- Route to NAT Gateway for outbound internet
```

### Example 2: Multi-Tier Web Application Architecture
```
VPC: 172.16.0.0/16

Web Tier (Public Subnets):
- us-east-1a: 172.16.1.0/24 (Web servers)
- us-east-1b: 172.16.2.0/24 (Web servers)

Application Tier (Private Subnets):
- us-east-1a: 172.16.11.0/24 (App servers)
- us-east-1b: 172.16.12.0/24 (App servers)

Database Tier (Private Subnets):
- us-east-1a: 172.16.21.0/24 (Primary DB)
- us-east-1b: 172.16.22.0/24 (Standby DB)
```

### Example 3: Security Group Configuration
```
Web Server Security Group:
Inbound Rules:
- HTTP (80) from 0.0.0.0/0 (anywhere)
- HTTPS (443) from 0.0.0.0/0 (anywhere)
- SSH (22) from 10.0.0.0/16 (VPC only)

Database Security Group:
Inbound Rules:
- MySQL (3306) from Web Server Security Group
- SSH (22) from Bastion Host Security Group
```

## Additional VPC Components

### NAT Gateway
- **Purpose** - Allows private subnet resources to access the internet
- **Outbound only** - Enables outbound internet access, blocks inbound
- **Managed service** - AWS-managed, highly available
- **Placement** - Must be placed in a public subnet

### Network ACLs (NACLs)
- **Subnet-level firewall** - Controls traffic at the subnet level
- **Stateless** - Must configure both inbound and outbound rules
- **Allow and deny rules** - Can explicitly deny traffic
- **Default NACL** - Allows all traffic by default

### VPC Endpoints
- **Private connectivity** - Access AWS services without internet gateway
- **Gateway endpoints** - For S3 and DynamoDB
- **Interface endpoints** - For other AWS services using private IP
- **Cost optimization** - Avoid data transfer charges through internet

### Elastic IP Addresses
- **Static public IPs** - IP addresses that don't change
- **Instance mobility** - Can be moved between instances
- **Charged when unused** - Small hourly charge for unused Elastic IPs
- **Limited quantity** - 5 per region by default (can be increased)

## Pricing ⭐ **EXAM FOCUS**

### VPC Pricing (Most Components are Free)
- **VPC creation** - Free
- **Subnets** - Free
- **Route tables** - Free
- **Internet Gateway** - Free
- **Security Groups** - Free

### Chargeable Components
- **NAT Gateway** - $0.045 per hour + data processing charges
- **VPC Endpoints** - $0.01 per hour per endpoint + data processing
- **VPN Connection** - $0.05 per hour per connection
- **Elastic IP addresses** - $0.005 per hour when not associated with running instance

### Example Cost Calculation
```
Basic VPC Setup:
- VPC with subnets: $0/month
- Internet Gateway: $0/month
- NAT Gateway: $0.045 × 24 × 30 = $32.40/month
- 2 Elastic IPs (unused): 2 × $0.005 × 24 × 30 = $7.20/month

Total: $39.60/month
```

## Integration with Other Services

### Amazon EC2
- **Instance placement** - Launch EC2 instances in specific subnets
- **Security groups** - Apply firewall rules to instances
- **Elastic IPs** - Assign static public IP addresses
- **Placement groups** - Optimize instance placement for performance

### Elastic Load Balancing
- **Application Load Balancer** - Distribute HTTP/HTTPS traffic across subnets
- **Network Load Balancer** - High-performance load balancing
- **Cross-AZ load balancing** - Distribute traffic across Availability Zones
- **Health checks** - Monitor instance health across subnets

### Amazon RDS
- **DB Subnet Groups** - Define subnets where RDS instances can be placed
- **Multi-AZ deployments** - High availability across Availability Zones
- **Security groups** - Control database access
- **Private connectivity** - Keep databases in private subnets

### AWS Lambda
- **VPC configuration** - Run Lambda functions inside your VPC
- **Private resource access** - Access RDS, ElastiCache, and other private resources
- **Security groups** - Apply security group rules to Lambda functions
- **ENI management** - AWS manages network interfaces automatically

## Best Practices

### Network Design
1. **Plan IP addressing** - Choose non-overlapping CIDR blocks
2. **Multi-AZ architecture** - Distribute resources across AZs
3. **Separate tiers** - Use different subnets for web, app, and database tiers
4. **Reserve IP space** - Leave room for future growth

### Security Best Practices
1. **Principle of least privilege** - Only allow necessary traffic
2. **Defense in depth** - Use both security groups and NACLs
3. **Private subnets** - Keep sensitive resources in private subnets
4. **Regular audits** - Review security group rules regularly

### Cost Optimization
1. **NAT Gateway placement** - Use one NAT Gateway per AZ only if needed
2. **Elastic IP management** - Release unused Elastic IPs
3. **VPC Endpoints** - Use for frequently accessed AWS services
4. **Data transfer optimization** - Keep traffic within the same AZ when possible

### High Availability
1. **Multi-AZ deployment** - Spread resources across multiple AZs
2. **Redundant NAT Gateways** - Deploy NAT Gateways in multiple AZs
3. **Load balancer distribution** - Use load balancers across AZs
4. **Auto Scaling** - Implement auto scaling across AZs

## Common Use Cases ⭐ **EXAM FOCUS**

### 1. Web Applications
- **Three-tier architecture** - Web, application, and database tiers
- **Public-facing websites** - Web servers in public subnets
- **Secure backends** - Application and database servers in private subnets
- **Load balancing** - Distribute traffic across multiple AZs

### 2. Enterprise Applications
- **Hybrid connectivity** - Connect to on-premises networks via VPN
- **Directory services** - Integrate with existing Active Directory
- **File sharing** - Secure file storage and sharing
- **Business applications** - ERP, CRM, and other enterprise software

### 3. Development and Testing
- **Isolated environments** - Separate dev, test, and production VPCs
- **Cost-effective testing** - Spin up and tear down test environments
- **Security testing** - Isolated environments for security testing
- **CI/CD pipelines** - Automated deployment across environments

### 4. Data Processing and Analytics
- **Big data processing** - Secure environments for data processing
- **Data lakes** - Store and analyze large datasets
- **Machine learning** - Isolated environments for ML workloads
- **ETL processes** - Extract, transform, and load data securely

## Limitations and Considerations

### VPC Limits
- **VPCs per region** - 5 per region (can be increased)
- **Subnets per VPC** - 200 per VPC
- **Security groups per VPC** - 2,500 per VPC
- **Rules per security group** - 60 inbound, 60 outbound rules

### IP Address Considerations
- **Reserved addresses** - AWS reserves 5 IP addresses per subnet
- **CIDR block limitations** - Cannot change VPC CIDR after creation
- **Overlapping ranges** - Cannot peer VPCs with overlapping CIDR blocks
- **IPv6 support** - Optional IPv6 support available

### Performance Considerations
- **Cross-AZ traffic** - Data transfer charges apply
- **NAT Gateway bandwidth** - Up to 45 Gbps bandwidth
- **Security group limits** - Performance impact with many rules
- **Network ACL processing** - Processed in rule number order

## Key Exam Points

✅ **Logically isolated network** - VPC provides network isolation in AWS cloud  
✅ **Public and private subnets** - Control internet access for resources  
✅ **Security groups** - Stateful firewalls at instance level  
✅ **Internet Gateway** - Enables internet access for public subnets  
✅ **NAT Gateway** - Allows private subnet resources to access internet  
✅ **Multi-AZ deployment** - High availability across Availability Zones  
✅ **Free core components** - VPC, subnets, IGW, security groups are free  

## Common Exam Scenarios

**Scenario:** "Need to isolate AWS resources in a private network"  
**Answer:** Create a VPC to provide logical network isolation

**Scenario:** "Web servers need internet access, but databases should remain private"  
**Answer:** Place web servers in public subnets and databases in private subnets

**Scenario:** "Private subnet resources need to download updates from the internet"  
**Answer:** Use a NAT Gateway in a public subnet to provide outbound internet access

**Scenario:** "Need to control traffic between application tiers"  
**Answer:** Use security groups to control traffic between different tiers

**Scenario:** "Application requires high availability across multiple locations"  
**Answer:** Deploy resources across multiple Availability Zones within the VPC

## Practice Questions

**Q: What is the primary purpose of a VPC?**  
A: To provide a logically isolated network environment within AWS

**Q: What's the difference between public and private subnets?**  
A: Public subnets have routes to an Internet Gateway, private subnets do not

**Q: What AWS component allows private subnet resources to access the internet?**  
A: NAT Gateway (or NAT Instance)

**Q: Are security groups stateful or stateless?**  
A: Stateful - return traffic is automatically allowed

**Q: What are the main free components of VPC?**  
A: VPC itself, subnets, route tables, Internet Gateway, and security groups

**Q: How many Internet Gateways can be attached to a VPC?**  
A: One Internet Gateway per VPC

**Q: What is the purpose of route tables in a VPC?**  
A: To determine where network traffic from subnets is directed

**Q: What happens to an Elastic IP address when it's not associated with a running instance?**  
A: You are charged a small hourly fee for unused Elastic IP addresses
