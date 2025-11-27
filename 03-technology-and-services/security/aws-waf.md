# AWS WAF

## Service Overview

AWS WAF (Web Application Firewall) is a managed firewall service that protects web applications from common web exploits and malicious traffic by filtering HTTP/HTTPS requests based on customizable security rules.

### 💡 Foundational Concepts

AWS WAF solves the critical business problem of **"How do we protect our web applications from malicious attacks and unwanted traffic?"** Think of WAF as a security guard at the entrance of your web application that inspects every visitor (HTTP request) and blocks those that match suspicious patterns or violate your security rules.

**Core Value Proposition:** WAF protects businesses from common web attacks like SQL injection, cross-site scripting (XSS), and bot traffic that could compromise data, disrupt services, or consume resources. It provides customizable protection without requiring changes to application code or infrastructure.

**Key Components:**
- **Web ACLs (Access Control Lists)** - Collections of rules that define what traffic to allow or block
- **Rules** - Conditions that inspect web requests (IP addresses, HTTP headers, request body, URI strings)
- **Rule Groups** - Reusable sets of rules for common protection scenarios
- **Managed Rules** - Pre-configured rule sets maintained by AWS and AWS Marketplace sellers
- **Rate-Based Rules** - Protection against excessive requests from single sources (DDoS mitigation)

### 🌐 Key Benefits & Value Proposition

**1. Protection Against Common Web Exploits (Security Advantage)**
- Defends against OWASP Top 10 vulnerabilities (SQL injection, XSS, etc.)
- Blocks malicious bots and scrapers that consume resources
- Prevents application-layer attacks that could compromise data or availability
- **Cloud Advantage:** Security scales automatically with your application traffic

**2. Customizable and Flexible Security (Agility Advantage)**
- Create custom rules tailored to your specific application requirements
- Deploy rule changes in minutes without application downtime
- Use managed rule groups for instant protection against emerging threats
- **Cloud Advantage:** Experiment with security rules without upfront infrastructure investment

**3. Real-Time Visibility and Monitoring (Operational Excellence)**
- Detailed metrics and logs of web traffic patterns and blocked requests
- Integration with CloudWatch for monitoring and alerting
- Sampled web request inspection for troubleshooting and analysis
- **Cloud Advantage:** Gain insights into traffic patterns to optimize security posture

**4. Cost-Effective Protection (Cost Savings Advantage)**
- Pay only for what you use (Web ACLs and rules processed)
- Reduce costs by blocking unwanted bot traffic and malicious requests
- No upfront hardware or software investments required
- **Cloud Advantage:** Stop spending money on traditional firewall appliances and maintenance

**5. Seamless AWS Integration (Elasticity & Scalability Advantage)**
- Automatically scales to handle any volume of web traffic
- Deploys in minutes across global AWS infrastructure
- No performance impact on legitimate user traffic
- **Cloud Advantage:** Protection scales elastically with application demand

### 🔒 Security and Compliance (CLF-C02 Focus)

**AWS Shared Responsibility Model for AWS WAF:**

**AWS Responsibilities (Security OF the Cloud):**
- Maintaining the underlying WAF infrastructure and service availability
- Protecting the WAF service platform from attacks and vulnerabilities
- Ensuring global deployment and redundancy of WAF capabilities
- Managing the security of managed rule groups provided by AWS
- Patching and updating the WAF service infrastructure

**Customer Responsibilities (Security IN the Cloud):**
- **Creating and configuring Web ACLs** - Defining which rules to apply to protect applications
- **Defining security rules** - Specifying conditions for allowing or blocking traffic
- **Selecting appropriate managed rule groups** - Choosing pre-built rules that match security needs
- **Monitoring WAF metrics and logs** - Reviewing blocked requests and adjusting rules accordingly
- **Testing rule configurations** - Ensuring rules don't block legitimate traffic
- **Associating WAF with resources** - Attaching Web ACLs to CloudFront, ALB, API Gateway, or AppSync
- **Managing IAM permissions** - Controlling who can modify WAF configurations
- **Responding to security events** - Taking action based on WAF alerts and blocked traffic patterns

**Compliance Considerations:**
- WAF helps meet compliance requirements for web application security (PCI DSS, HIPAA, etc.)
- Logging capabilities support audit and compliance reporting needs
- Managed rules can help address specific regulatory requirements

### 💰 Billing, Pricing, and Support

**Primary Pricing Model: Pay-As-You-Go**

AWS WAF charges based on three components:

**1. Web ACL Charges:**
- Monthly fee per Web ACL deployed
- Charged for each Web ACL regardless of traffic volume

**2. Rule Charges:**
- Monthly fee per rule added to Web ACLs
- Includes custom rules and rules within rule groups
- Managed rule groups have separate pricing

**3. Request Charges:**
- Per million web requests processed by WAF
- Charged based on actual traffic volume inspected

**Additional Pricing Considerations:**
- **Managed Rule Groups** - Separate subscription fees for AWS Managed Rules and Marketplace rules
- **Bot Control** - Additional charges for advanced bot detection and mitigation
- **Fraud Control (Account Takeover Prevention)** - Premium feature with separate pricing
- **CAPTCHA** - Charges per CAPTCHA puzzle served to users
- **No data transfer charges** - WAF doesn't add data transfer costs

**Cost Optimization Tips:**
- Start with AWS Managed Rules to avoid creating complex custom rules
- Use rate-based rules to automatically block excessive requests
- Monitor CloudWatch metrics to identify and block unwanted traffic patterns
- Remove unused rules and Web ACLs to reduce monthly charges

**AWS Support Integration:**
- All support plans include access to WAF documentation and forums
- Developer, Business, and Enterprise Support plans provide technical assistance
- Enterprise Support includes access to Technical Account Managers for WAF optimization

### 🎯 Common Use Cases (Scenario-Based)

**1. E-Commerce Website Protection**
- **Problem:** Online store vulnerable to SQL injection attacks that could expose customer payment data
- **Solution:** Deploy AWS WAF with managed rules for SQL injection protection on Application Load Balancer
- **Benefit:** Automatically blocks malicious database queries while allowing legitimate customer transactions

**2. API Rate Limiting and Bot Protection**
- **Problem:** Public API experiencing excessive requests from bots, causing high costs and degraded performance
- **Solution:** Configure rate-based rules in WAF to limit requests per IP address and block known bot signatures
- **Benefit:** Reduces infrastructure costs by blocking unwanted traffic and ensures API availability for legitimate users

**3. Content Website DDoS Mitigation**
- **Problem:** News website facing application-layer DDoS attacks during high-traffic events
- **Solution:** Use WAF with CloudFront distribution to filter malicious requests at edge locations
- **Benefit:** Maintains website availability during attacks without impacting legitimate reader access

**4. Geographic Access Control**
- **Problem:** SaaS application needs to restrict access to specific countries due to compliance requirements
- **Solution:** Create WAF rules to allow or block traffic based on geographic location (IP address origin)
- **Benefit:** Ensures compliance with data sovereignty regulations while maintaining global accessibility where permitted

**5. Protection Against Zero-Day Vulnerabilities**
- **Problem:** Web application potentially vulnerable to newly discovered exploits before patches are available
- **Solution:** Deploy AWS Managed Rules that are automatically updated when new threats emerge
- **Benefit:** Immediate protection against emerging threats without manual rule updates or application changes

### 🔗 Related Core Services

**1. Amazon CloudFront (Content Delivery Network)**
- **Relationship:** WAF integrates directly with CloudFront distributions to filter traffic at edge locations
- **CLF-C02 Context:** Provides global protection by inspecting requests before they reach origin servers, reducing latency and improving security
- **Use Together:** Deploy WAF on CloudFront for web applications requiring global reach and low-latency protection

**2. Application Load Balancer (ALB)**
- **Relationship:** WAF can be associated with ALBs to protect applications running on EC2 instances or containers
- **CLF-C02 Context:** Filters malicious traffic before it reaches backend application servers, reducing load and improving security
- **Use Together:** Attach WAF to ALB for regional applications that don't use CloudFront

**3. Amazon API Gateway**
- **Relationship:** WAF protects REST APIs and HTTP APIs created with API Gateway
- **CLF-C02 Context:** Secures serverless APIs from common exploits and excessive requests
- **Use Together:** Use WAF with API Gateway to protect backend Lambda functions from malicious API calls

**4. AWS Shield (DDoS Protection)**
- **Relationship:** WAF and Shield work together for comprehensive protection (Shield for network/transport layer, WAF for application layer)
- **CLF-C02 Context:** Shield Advanced customers get WAF at no additional charge for protected resources
- **Use Together:** Combine Shield Standard (free) with WAF for complete DDoS and application-layer protection

**5. Amazon CloudWatch (Monitoring and Logging)**
- **Relationship:** WAF sends metrics and logs to CloudWatch for monitoring, alerting, and analysis
- **CLF-C02 Context:** Provides visibility into blocked requests, traffic patterns, and rule effectiveness
- **Use Together:** Use CloudWatch dashboards to monitor WAF activity and create alarms for suspicious traffic patterns

**6. AWS Firewall Manager (Centralized Management)**
- **Relationship:** Firewall Manager centrally configures and manages WAF rules across multiple AWS accounts
- **CLF-C02 Context:** Simplifies security management for organizations with multiple applications and accounts
- **Use Together:** Use Firewall Manager to enforce consistent WAF policies across an entire organization

---

## Official AWS Documentation

- [AWS WAF Product Page](https://aws.amazon.com/waf/)
- [AWS WAF Documentation](https://docs.aws.amazon.com/waf/)
- [AWS WAF FAQs](https://aws.amazon.com/waf/faqs/)
- [AWS WAF Pricing](https://aws.amazon.com/waf/pricing/)
- [AWS WAF Developer Guide](https://docs.aws.amazon.com/waf/latest/developerguide/)
