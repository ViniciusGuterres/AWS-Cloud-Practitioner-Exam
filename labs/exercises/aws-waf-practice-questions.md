# AWS WAF - CLF-C02 Practice Questions

## Section 1: Practice Questions

### Question 1
AnyCompany Retail operates an e-commerce website that has been experiencing SQL injection attacks attempting to access customer payment information. The security team needs to implement protection against these web exploits without modifying the application code or deploying additional hardware.

Which AWS service should they use to address this requirement?

a) AWS Shield Standard

b) AWS WAF

c) Amazon GuardDuty

d) AWS Security Hub

---

### Question 2
A startup company is launching a public REST API using Amazon API Gateway. They are concerned about excessive requests from automated bots that could increase costs and degrade performance for legitimate users. 

What is the MOST cost-effective way to limit requests from individual IP addresses?

a) Use Amazon CloudFront with geographic restrictions to block traffic from specific countries

b) Configure AWS WAF with rate-based rules to automatically block IPs exceeding request thresholds

c) Deploy a Network Load Balancer with connection limits configured

d) Use AWS Shield Advanced to protect against all types of excessive requests

---

### Question 3
Which statement BEST describes the primary purpose of AWS WAF?

a) A managed service that protects against network and transport layer DDoS attacks on AWS resources

b) A firewall service that filters HTTP/HTTPS requests to web applications based on customizable security rules

c) A threat detection service that continuously monitors for malicious activity across AWS accounts

d) A compliance service that automatically encrypts data in transit and at rest for web applications

---

### Question 4
AnyCompany Financial is deploying a web application on AWS and needs to comply with PCI DSS requirements. They must demonstrate protection against common web exploits like cross-site scripting (XSS) and SQL injection.

Which combination of AWS services provides this protection? (Select TWO)

a) AWS WAF with managed rules for OWASP Top 10 vulnerabilities

b) Amazon Inspector for continuous vulnerability scanning

c) AWS Shield Advanced for application-layer protection

d) Application Load Balancer to distribute traffic across multiple instances

e) AWS WAF with custom rules targeting specific attack patterns

---

### Question 5
A media company uses Amazon CloudFront to deliver content globally. They want to block access from specific countries due to licensing restrictions while also protecting against common web attacks.

Where should AWS WAF be deployed to achieve both requirements?

a) On the Amazon EC2 instances hosting the origin content

b) On the Application Load Balancer in front of the EC2 instances

c) On the Amazon CloudFront distribution

d) On the Amazon VPC using network ACLs

---

### Question 6
According to the AWS Shared Responsibility Model, which of the following is the CUSTOMER's responsibility when using AWS WAF?

a) Maintaining the underlying infrastructure that runs the WAF service

b) Patching and updating the WAF service platform

c) Creating and configuring Web ACLs and security rules

d) Ensuring global availability of the WAF service

---

### Question 7
AnyCompany SaaS has deployed AWS WAF to protect their web application. They want to monitor blocked requests and analyze traffic patterns to improve their security rules.

Which AWS service should they use to view WAF metrics and logs?

a) AWS CloudTrail

b) Amazon CloudWatch

c) AWS Config

d) Amazon Inspector

---

### Question 8
A company is concerned about a newly discovered web application vulnerability that could affect their production environment. They need immediate protection while their development team works on a permanent fix.

What is the FASTEST way to implement protection using AWS WAF?

a) Write custom rules from scratch to block the specific vulnerability pattern

b) Deploy AWS Managed Rules that are automatically updated for emerging threats

c) Migrate the application to a different AWS Region with enhanced security

d) Enable AWS Shield Advanced for comprehensive protection

---

### Question 9
How is AWS WAF primarily priced?

a) Fixed monthly fee based on the number of protected applications

b) Charges based on Web ACLs, rules, and the number of web requests processed

c) Free tier with unlimited requests, then tiered pricing based on bandwidth

d) Per-hour charges for each AWS resource protected by WAF

---

### Question 10
AnyCompany Healthcare runs multiple web applications across different AWS accounts. They need to enforce consistent WAF security policies across all applications to meet compliance requirements.

Which AWS service should they use to centrally manage WAF rules across multiple accounts?

a) AWS Organizations with Service Control Policies (SCPs)

b) AWS Systems Manager

c) AWS Firewall Manager

d) AWS Control Tower

---

## Section 2: Answers and Justifications

### Question 1: Correct Answer - B

**Why B is correct:**
AWS WAF is specifically designed to protect web applications from common web exploits including SQL injection, cross-site scripting (XSS), and other OWASP Top 10 vulnerabilities. It filters HTTP/HTTPS requests based on customizable rules without requiring application code changes or hardware deployment. This directly addresses the requirement to protect against SQL injection attacks at the application layer.

**Why other options are incorrect:**

**A) AWS Shield Standard** - Shield protects against network and transport layer DDoS attacks (Layer 3/4), not application-layer exploits like SQL injection (Layer 7). Shield focuses on volumetric attacks, not web application vulnerabilities.

**C) Amazon GuardDuty** - GuardDuty is a threat detection service that monitors for malicious activity and unauthorized behavior across AWS accounts. It doesn't actively block or filter web traffic; it only detects and alerts on threats.

**D) AWS Security Hub** - Security Hub is a security posture management service that aggregates findings from multiple AWS security services. It provides visibility and compliance checking but doesn't actively protect against web exploits.

---

### Question 2: Correct Answer - B

**Why B is correct:**
AWS WAF rate-based rules are specifically designed to automatically block IP addresses that exceed a specified number of requests within a five-minute period. This is the most cost-effective solution because: (1) it directly addresses bot traffic and excessive requests, (2) it's automated with no manual intervention required, (3) WAF pricing is based on usage, making it economical for startups, and (4) it protects the API Gateway from processing unwanted requests, reducing overall costs.

**Why other options are incorrect:**

**A) Amazon CloudFront with geographic restrictions** - Geographic restrictions block entire countries/regions, not individual IPs making excessive requests. This doesn't address bot traffic from allowed geographic locations and is too broad for the requirement.

**C) Network Load Balancer with connection limits** - NLB operates at Layer 4 (transport layer) and doesn't inspect HTTP requests or track request rates per IP address. It's designed for high-performance TCP/UDP traffic distribution, not application-layer rate limiting.

**D) AWS Shield Advanced** - Shield Advanced is expensive ($3,000/month minimum) and primarily protects against DDoS attacks, not general bot traffic or rate limiting. This is not cost-effective for a startup and is overkill for the stated requirement.

---

### Question 3: Correct Answer - B

**Why B is correct:**
This statement accurately describes AWS WAF's primary purpose: it's a web application firewall that inspects and filters HTTP/HTTPS requests (Layer 7) based on rules you define. It allows or blocks requests based on conditions like IP addresses, HTTP headers, body content, URI strings, SQL injection patterns, and cross-site scripting attempts.

**Why other options are incorrect:**

**A) Network and transport layer DDoS protection** - This describes AWS Shield, not AWS WAF. While WAF can help mitigate some application-layer DDoS attacks through rate-based rules, its primary purpose is filtering web requests based on security rules, not DDoS protection.

**C) Threat detection service** - This describes Amazon GuardDuty, which monitors for malicious activity and generates findings. WAF actively blocks traffic; it doesn't just detect threats.

**D) Compliance service with automatic encryption** - This describes aspects of services like AWS Certificate Manager (ACM) or AWS KMS. WAF doesn't handle encryption; it filters HTTP/HTTPS requests based on security rules.

---

### Question 4: Correct Answers - A and E

**Why A is correct:**
AWS Managed Rules for WAF include pre-configured rule groups specifically designed to protect against OWASP Top 10 vulnerabilities, which include XSS and SQL injection. These managed rules are maintained by AWS security experts and automatically updated, providing immediate protection that helps meet PCI DSS requirements for web application security.

**Why E is correct:**
Custom WAF rules allow the company to create specific protections tailored to their application's unique requirements and attack patterns. This flexibility is important for PCI DSS compliance, as organizations must demonstrate appropriate controls for their specific environment. Custom rules complement managed rules for comprehensive protection.

**Why other options are incorrect:**

**B) Amazon Inspector** - Inspector performs vulnerability assessments and security scanning of EC2 instances and container images. While useful for compliance, it doesn't actively protect against web exploits in real-time like WAF does.

**C) AWS Shield Advanced** - Shield Advanced protects against DDoS attacks at the network and transport layers (Layer 3/4), not application-layer exploits like XSS and SQL injection (Layer 7). While Shield Advanced includes WAF at no additional cost, Shield itself doesn't provide the web exploit protection required.

**D) Application Load Balancer** - ALB distributes traffic and provides high availability but doesn't inspect or filter requests for security threats. ALB can work with WAF, but by itself doesn't protect against XSS or SQL injection.

---

### Question 5: Correct Answer - C

**Why C is correct:**
Deploying AWS WAF on the CloudFront distribution is the optimal solution because: (1) it filters requests at AWS edge locations globally before they reach the origin, (2) CloudFront natively supports geographic restrictions (geo-blocking), (3) WAF rules can be applied at the edge for low-latency protection, and (4) this approach protects the origin infrastructure from both malicious traffic and unwanted geographic access. This single deployment point addresses both requirements efficiently.

**Why other options are incorrect:**

**A) On EC2 instances** - You cannot deploy AWS WAF directly on EC2 instances. WAF must be associated with CloudFront, Application Load Balancer, API Gateway, or AWS AppSync. Additionally, this wouldn't provide geographic restrictions or edge protection.

**B) On Application Load Balancer** - While WAF can be deployed on ALB, this only protects the regional endpoint and doesn't provide the global edge protection or geographic restrictions that CloudFront offers. Traffic would still reach AWS infrastructure before being blocked.

**D) On VPC using network ACLs** - Network ACLs operate at Layer 4 (network layer) and cannot inspect HTTP/HTTPS content for web attacks. They also don't provide the geographic restriction capabilities needed. WAF cannot be deployed on VPCs directly.

---

### Question 6: Correct Answer - C

**Why C is correct:**
Under the AWS Shared Responsibility Model, customers are responsible for security "IN" the cloud, which includes configuring AWS services. For WAF, this means customers must create Web ACLs, define security rules (custom or managed), configure rule conditions, associate WAF with resources (CloudFront, ALB, etc.), and monitor/adjust rules based on traffic patterns. AWS provides the service; customers configure how it protects their applications.

**Why other options are incorrect:**

**A) Maintaining underlying infrastructure** - This is AWS's responsibility (security "OF" the cloud). AWS manages the physical infrastructure, hardware, networking, and facilities that run the WAF service.

**B) Patching and updating the WAF service platform** - AWS is responsible for maintaining, patching, and updating the WAF service itself, including the underlying software and infrastructure. Customers don't have access to or responsibility for the service platform.

**D) Ensuring global availability** - AWS is responsible for the availability, redundancy, and global deployment of the WAF service. Customers benefit from this availability but don't manage it.

---

### Question 7: Correct Answer - B

**Why B is correct:**
Amazon CloudWatch is the primary service for monitoring AWS WAF. WAF automatically sends metrics to CloudWatch (such as allowed requests, blocked requests, counted requests) and can send detailed logs to CloudWatch Logs. CloudWatch enables you to create dashboards to visualize WAF activity, set up alarms for suspicious patterns, and analyze traffic trends to optimize security rules. This is the standard AWS approach for monitoring service metrics and logs.

**Why other options are incorrect:**

**A) AWS CloudTrail** - CloudTrail logs API calls made to AWS services, including changes to WAF configurations (who created/modified rules). However, it doesn't log the actual web requests that WAF processes or blocks. CloudTrail is for audit trails of management actions, not operational monitoring of traffic.

**C) AWS Config** - Config tracks configuration changes and compliance of AWS resources over time. It can monitor changes to WAF Web ACLs and rules but doesn't provide metrics or logs of blocked requests and traffic patterns.

**D) Amazon Inspector** - Inspector is a vulnerability assessment service for EC2 instances and container images. It doesn't monitor WAF activity or web traffic patterns.

---

### Question 8: Correct Answer - B

**Why B is correct:**
AWS Managed Rules provide the fastest protection because: (1) they're pre-configured by AWS security experts and ready to deploy immediately, (2) they're automatically updated when new threats emerge, including zero-day vulnerabilities, (3) no custom rule development or testing is required, and (4) they can be enabled in minutes through the AWS console or API. For emerging threats, AWS updates managed rules proactively, providing immediate protection while the development team works on permanent fixes.

**Why other options are incorrect:**

**A) Write custom rules from scratch** - Creating custom rules requires time to understand the vulnerability, develop rule logic, test for false positives, and deploy. This is slower than using pre-built managed rules and requires security expertise to implement correctly.

**C) Migrate to a different AWS Region** - Migrating regions doesn't address the vulnerability; the application would still be vulnerable in the new region. This is time-consuming, complex, and doesn't provide any security benefit for web application vulnerabilities.

**D) Enable AWS Shield Advanced** - Shield Advanced protects against DDoS attacks, not web application vulnerabilities. While Shield Advanced includes WAF at no additional cost, simply enabling Shield doesn't automatically protect against specific web exploits; you still need to configure WAF rules.

---

### Question 9: Correct Answer - B

**Why B is correct:**
AWS WAF uses a pay-as-you-go pricing model with three main components: (1) monthly charge per Web ACL deployed, (2) monthly charge per rule added to Web ACLs, and (3) charge per million web requests processed. Additional charges apply for managed rule groups, bot control, and CAPTCHA usage. This usage-based pricing aligns with AWS's cloud economics principle of paying only for what you use.

**Why other options are incorrect:**

**A) Fixed monthly fee per application** - WAF doesn't charge a fixed fee per application. Pricing is based on the number of Web ACLs, rules, and requests processed, which can vary significantly based on usage. This model wouldn't align with AWS's pay-as-you-go philosophy.

**C) Free tier with unlimited requests** - WAF doesn't offer a free tier or unlimited requests at any pricing level. All Web ACLs, rules, and requests are charged according to the published pricing model. AWS doesn't charge based on bandwidth for WAF.

**D) Per-hour charges for protected resources** - WAF charges are based on Web ACLs and rules (monthly) plus requests processed, not hourly charges per resource. The pricing model is designed around WAF usage, not the resources being protected.

---

### Question 10: Correct Answer - C

**Why C is correct:**
AWS Firewall Manager is specifically designed to centrally configure and manage firewall rules across multiple AWS accounts and resources in an AWS Organization. For WAF, Firewall Manager allows you to: (1) create and apply WAF policies across all accounts, (2) automatically apply rules to new resources, (3) ensure consistent security posture organization-wide, and (4) maintain compliance by enforcing mandatory security policies. This is the purpose-built solution for centralized WAF management.

**Why other options are incorrect:**

**A) AWS Organizations with SCPs** - Service Control Policies define maximum permissions for accounts in an organization but don't configure or manage WAF rules. SCPs control what actions are allowed (e.g., who can modify WAF), not the actual security rules themselves.

**B) AWS Systems Manager** - Systems Manager is designed for managing EC2 instances and on-premises servers (patching, configuration, automation). It doesn't manage WAF rules or security policies across accounts.

**D) AWS Control Tower** - Control Tower sets up and governs multi-account AWS environments with best-practice blueprints. While it can establish account baselines, it's not designed for ongoing, centralized management of WAF rules across accounts like Firewall Manager is.

---

## Additional Study Notes

### Key CLF-C02 Concepts for AWS WAF:

**Service Purpose:**
- Application-layer (Layer 7) firewall for web applications
- Protects against common web exploits (SQL injection, XSS, etc.)
- Customizable rules for specific security requirements

**Cost Optimization:**
- Pay-as-you-go pricing (Web ACLs + rules + requests)
- Reduces costs by blocking unwanted bot traffic
- Use managed rules to avoid custom rule development costs

**Security & Compliance:**
- Helps meet compliance requirements (PCI DSS, HIPAA)
- Part of defense-in-depth strategy with Shield
- Customer configures rules; AWS manages infrastructure

**Integration Points:**
- CloudFront (global edge protection)
- Application Load Balancer (regional protection)
- API Gateway (API protection)
- Works with CloudWatch for monitoring
- Managed centrally with Firewall Manager

**Common Exam Scenarios:**
- Protecting against web exploits without code changes
- Rate limiting for APIs and bot protection
- Geographic restrictions combined with security rules
- Compliance requirements for web application security
