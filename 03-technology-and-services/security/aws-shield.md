# AWS Shield

## Service Overview

AWS Shield is a managed Distributed Denial of Service (DDoS) protection service that safeguards applications running on AWS against network and transport layer attacks.

### 💡 Foundational Concepts

AWS Shield solves the critical business problem of **"How do we keep our applications available when under attack?"** Think of Shield as a protective barrier that filters out malicious traffic attempting to overwhelm your applications, ensuring legitimate users can always access your services.

**Core Value Proposition:** Shield protects businesses from DDoS attacks that could cause application downtime, revenue loss, and reputation damage. It automatically detects and mitigates attacks without requiring manual intervention or specialized security expertise.

**Key Components:**
- **AWS Shield Standard** - Automatic protection included free with all AWS accounts
- **AWS Shield Advanced** - Enhanced protection with additional features and 24/7 DDoS Response Team (DRT) support
- **DDoS Attack Detection** - Real-time monitoring and automatic threat identification
- **Attack Mitigation** - Automatic traffic filtering and rerouting during attacks

### 🌐 Key Benefits & Value Proposition

**1. Always-On Protection (High Availability Advantage)**
- Continuous monitoring and automatic attack detection 24/7/365
- Instant mitigation without manual intervention or configuration changes
- Protects application availability during peak traffic and attack scenarios

**2. Cost Protection (Cost Savings Advantage)**
- Shield Standard included at no additional cost for all AWS customers
- Shield Advanced provides DDoS cost protection - no charges for scaling during attacks
- Prevents revenue loss from application downtime and service disruptions

**3. Comprehensive Coverage (Security Advantage)**
- Protects against the most common network and transport layer DDoS attacks
- Defends multiple AWS resources (CloudFront, Route 53, Elastic Load Balancing, EC2)
- Integrates with AWS WAF for application layer (Layer 7) protection

**4. Global Scale (Global Reach & Elasticity Advantage)**
- Leverages AWS global infrastructure for distributed attack mitigation
- Automatically scales protection capacity to handle large-scale attacks
- No performance impact on legitimate traffic during normal operations

**5. Expert Support (Shield Advanced) (Operational Excellence)**
- 24/7 access to AWS DDoS Response Team (DRT) for attack response
- Proactive engagement during high-severity events
- Post-attack analysis and recommendations for improved protection

### 🔒 Security and Compliance (CLF-C02 Focus)

**AWS Shared Responsibility Model for AWS Shield:**

**AWS Responsibilities:**
- Operating and maintaining the Shield infrastructure and detection systems
- Providing automatic DDoS protection at the network and transport layers
- Monitoring global traffic patterns for attack identification
- Ensuring Shield service availability and performance
- Maintaining physical security of Shield infrastructure
- Updating threat detection algorithms and mitigation techniques

**Customer Responsibilities:**
- Enabling Shield Advanced if enhanced protection is required (Standard is automatic)
- Configuring protected resources (CloudFront distributions, Route 53 hosted zones, etc.)
- Implementing application-layer security controls (AWS WAF rules)
- Monitoring Shield metrics and notifications through CloudWatch
- Responding to Shield Advanced health checks and recommendations
- Designing resilient architectures that complement DDoS protection

**Security Best Practices:**
- Use Shield Standard as baseline protection for all AWS resources
- Enable Shield Advanced for business-critical applications requiring guaranteed uptime
- Combine Shield with AWS WAF for comprehensive Layer 3-7 protection
- Implement CloudWatch alarms for DDoS attack notifications
- Follow AWS Well-Architected Framework security pillar guidelines

### 💰 Billing, Pricing, and Support

**AWS Shield Standard:**
- **Cost:** Free - automatically included with all AWS accounts
- **Coverage:** Protection for all AWS customers at no additional charge
- **Included Protection:** Network layer (Layer 3) and transport layer (Layer 4) DDoS attacks

**AWS Shield Advanced:**
- **Cost:** $3,000 per month per organization (1-year subscription commitment)
- **Additional Charges:** Data transfer fees for DDoS Response Team (DRT) mitigation actions
- **DDoS Cost Protection:** Protects against scaling charges during DDoS attacks for:
  - Amazon CloudFront
  - Amazon Route 53
  - Elastic Load Balancing
  - AWS Global Accelerator

**Included Features with Shield Advanced:**
- 24/7 access to AWS DDoS Response Team (DRT)
- Advanced real-time attack notifications and detailed diagnostics
- Integration with AWS WAF at no additional cost for protected resources
- Cost protection (credits) for scaling charges incurred during attacks
- Proactive engagement for high-severity events

**Support Integration:**
- Shield Standard works with all AWS Support plans
- Shield Advanced includes specialized DRT support regardless of AWS Support plan
- Access to AWS Health Dashboard for attack visibility and notifications

### 🎯 Common Use Cases (Scenario-Based)

**1. E-Commerce Website Protection**
A retail company runs an online store on AWS and needs to ensure their website remains available during Black Friday sales and potential DDoS attacks. Shield Standard automatically protects their CloudFront distribution and Application Load Balancer from network-layer attacks, while Shield Advanced provides guaranteed uptime and cost protection during traffic spikes.

**2. Gaming Application Availability**
A gaming company hosts multiplayer game servers on EC2 instances behind an Elastic Load Balancer. They use Shield Standard for baseline DDoS protection and Shield Advanced for 24/7 DRT support to quickly respond to sophisticated attacks that could disrupt gameplay and frustrate users.

**3. Financial Services Platform**
A fintech startup provides a mobile banking application that must maintain 99.99% uptime for regulatory compliance. They implement Shield Advanced with AWS WAF to protect their API endpoints from both network-layer DDoS attacks and application-layer threats, ensuring continuous service availability for customers.

**4. Media Streaming Service**
A video streaming platform uses CloudFront to deliver content globally. Shield Standard protects against common DDoS attacks automatically, while Shield Advanced provides cost protection during viral content releases that generate massive traffic spikes, preventing unexpected infrastructure scaling costs.

### 🔗 Related Core Services

**1. AWS WAF (Web Application Firewall)**
- **Relationship:** Shield protects against network/transport layer attacks (Layer 3-4), while WAF defends against application layer attacks (Layer 7)
- **Integration:** Shield Advanced includes AWS WAF at no additional cost for protected resources
- **Use Together:** Combined protection provides comprehensive defense from infrastructure to application layers

**2. Amazon CloudFront**
- **Relationship:** CloudFront distributions are primary resources protected by Shield
- **Integration:** Shield Standard automatically protects all CloudFront distributions; Shield Advanced provides enhanced protection
- **Use Together:** CloudFront's global edge network combined with Shield creates distributed DDoS defense

**3. Amazon Route 53**
- **Relationship:** Route 53 hosted zones benefit from Shield's DNS-level DDoS protection
- **Integration:** Shield protects Route 53 from DNS query floods and other DNS-targeted attacks
- **Use Together:** Ensures DNS resolution remains available even during large-scale DDoS attacks

**4. Elastic Load Balancing (ELB)**
- **Relationship:** Application Load Balancers and Network Load Balancers are protected by Shield
- **Integration:** Shield automatically detects and mitigates attacks targeting load balancers
- **Use Together:** Load balancer health combined with Shield protection ensures application availability

**5. Amazon CloudWatch**
- **Relationship:** CloudWatch provides metrics, alarms, and dashboards for Shield events
- **Integration:** Shield publishes DDoS attack metrics to CloudWatch for monitoring and alerting
- **Use Together:** Real-time visibility into attack patterns and automatic notifications during incidents

### Official AWS documentation: https://docs.aws.amazon.com/waf/latest/developerguide/shield-chapter.html