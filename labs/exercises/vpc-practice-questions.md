# AWS VPC Practice Questions - CLF-C02 Exam Preparation

## Section 1: CLF-C02 Practice Questions

### Question 1
A company wants to launch EC2 instances in an isolated network environment within AWS where they have complete control over IP addressing and routing. Which AWS service should they use?

A) Amazon CloudFront  
B) AWS Direct Connect  
C) Amazon VPC (Virtual Private Cloud)  
D) AWS Transit Gateway

### Question 2
Which of the following statements about AWS VPC pricing is correct?

A) You are charged hourly for each VPC you create  
B) Creating a VPC, subnets, route tables, and Internet Gateway incurs no additional charges  
C) You must pay a monthly subscription fee to use VPC features  
D) VPC usage is charged based on the number of EC2 instances launched

### Question 3
A startup needs to host a web application where the web servers should be accessible from the internet, but the database servers should remain private and not directly accessible from the internet. How should they configure their VPC?

A) Place both web servers and database servers in private subnets  
B) Place both web servers and database servers in public subnets  
C) Place web servers in public subnets and database servers in private subnets  
D) Create separate VPCs for web servers and database servers

### Question 4
What is the primary purpose of an Internet Gateway in an AWS VPC?

A) To provide a connection between multiple VPCs  
B) To enable communication between a VPC and the internet  
C) To monitor network traffic within the VPC  
D) To provide DNS resolution for VPC resources

### Question 5
A company has an on-premises data center and wants to securely connect it to their AWS VPC to create a hybrid cloud environment. Which combination of AWS services would be most appropriate for this requirement?

A) Internet Gateway and Elastic Load Balancer  
B) Virtual Private Gateway and Site-to-Site VPN  
C) NAT Gateway and CloudFront  
D) Transit Gateway and Direct Connect only

---

## Section 2: Answers and Justifications

### Question 1 - Answer: C) Amazon VPC (Virtual Private Cloud)

**Correct Answer Justification:**
Amazon VPC is specifically designed to provide a logically isolated network environment within AWS where customers have complete control over their virtual networking environment, including IP address ranges, subnets, route tables, and network gateways. This directly addresses the requirement for an isolated network with control over IP addressing and routing.

**Why Other Options Are Incorrect:**
- **A) Amazon CloudFront:** This is a content delivery network (CDN) service for distributing content globally, not for creating isolated network environments.
- **B) AWS Direct Connect:** This provides a dedicated network connection from on-premises to AWS, but doesn't create the isolated network environment itself.
- **D) AWS Transit Gateway:** This is used to connect multiple VPCs and on-premises networks, but you still need VPC as the foundational isolated network.

### Question 2 - Answer: B) Creating a VPC, subnets, route tables, and Internet Gateway incurs no additional charges

**Correct Answer Justification:**
AWS VPC core components (VPC itself, subnets, route tables, Internet Gateway, and security groups) are provided at no additional charge. This is a key cost benefit of VPC that's important for the CLF-C02 exam. You only pay for optional components like NAT Gateways, VPN connections, and data transfer.

**Why Other Options Are Incorrect:**
- **A) Hourly charges for VPC:** VPC creation and basic components are free.
- **C) Monthly subscription fee:** There are no subscription fees for basic VPC functionality.
- **D) Charged based on EC2 instances:** VPC charges are independent of the number of EC2 instances; EC2 instances have their own separate pricing.

### Question 3 - Answer: C) Place web servers in public subnets and database servers in private subnets

**Correct Answer Justification:**
This follows the standard three-tier architecture security best practice. Public subnets have routes to an Internet Gateway, making resources accessible from the internet (appropriate for web servers). Private subnets don't have direct internet access, providing security for sensitive resources like databases. This is a fundamental VPC design pattern tested in CLF-C02.

**Why Other Options Are Incorrect:**
- **A) Both in private subnets:** Web servers wouldn't be accessible from the internet, defeating the purpose of a web application.
- **B) Both in public subnets:** Database servers would be directly accessible from the internet, creating security vulnerabilities.
- **D) Separate VPCs:** This adds unnecessary complexity and cost for a simple web application architecture.

### Question 4 - Answer: B) To enable communication between a VPC and the internet

**Correct Answer Justification:**
An Internet Gateway (IGW) is specifically designed to enable bidirectional communication between resources in a VPC and the internet. It's a horizontally scaled, redundant, and highly available VPC component that allows internet access for resources with public IP addresses in public subnets.

**Why Other Options Are Incorrect:**
- **A) Connection between VPCs:** This describes VPC Peering or Transit Gateway, not Internet Gateway.
- **C) Monitor network traffic:** This describes services like VPC Flow Logs or CloudWatch, not Internet Gateway functionality.
- **D) DNS resolution:** This describes Amazon Route 53 or VPC DNS resolver, not Internet Gateway.

### Question 5 - Answer: B) Virtual Private Gateway and Site-to-Site VPN

**Correct Answer Justification:**
For securely connecting an on-premises data center to AWS VPC, you need a Virtual Private Gateway (the AWS-side VPN endpoint) and a Site-to-Site VPN connection (encrypted IPsec tunnels). This combination provides secure, encrypted connectivity over the internet, which is the most common and cost-effective solution for hybrid cloud connectivity tested in CLF-C02.

**Why Other Options Are Incorrect:**
- **A) Internet Gateway and ELB:** Internet Gateway provides public internet access, not secure private connectivity to on-premises.
- **C) NAT Gateway and CloudFront:** NAT Gateway provides outbound internet access for private resources, and CloudFront is a CDN - neither provides on-premises connectivity.
- **D) Transit Gateway and Direct Connect only:** While this could work, it's more complex and expensive than necessary. Direct Connect alone requires physical setup and is typically for high-bandwidth requirements, making VPN more appropriate for basic hybrid connectivity.

---

## Key Learning Points for CLF-C02

### VPC Fundamentals
- VPC provides logically isolated network environment
- Core components (VPC, subnets, route tables, IGW) are free
- Supports both public and private subnets for different security requirements

### Security Best Practices
- Use public subnets for internet-facing resources
- Use private subnets for sensitive resources like databases
- Security groups and NACLs provide layered security

### Hybrid Connectivity
- Virtual Private Gateway + Site-to-Site VPN for secure on-premises connectivity
- Internet Gateway for public internet access
- Different solutions for different connectivity requirements

### Cost Considerations
- Basic VPC components are free
- Charges apply for optional services (NAT Gateway, VPN connections)
- Understanding what's free vs. chargeable is important for CLF-C02
