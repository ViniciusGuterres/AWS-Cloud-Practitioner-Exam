# AWS Shield - CLF-C02 Practice Questions

## Section 1: Practice Questions

### Question 1
AnyCompany Retail runs an e-commerce website on AWS using CloudFront and Application Load Balancer. During a recent product launch, their website experienced a sudden surge in traffic that caused unexpected scaling costs. The IT manager wants to protect against both DDoS attacks and the associated cost increases during future traffic spikes.

Which AWS Shield option should they choose?

a) AWS Shield Standard with Amazon CloudWatch alarms

b) AWS Shield Advanced with DDoS cost protection

c) AWS WAF with rate-based rules

d) AWS Shield Standard with Auto Scaling policies

---

### Question 2
Which statement BEST describes the difference between AWS Shield Standard and AWS Shield Advanced?

a) Shield Standard protects only EC2 instances, while Shield Advanced protects all AWS resources

b) Shield Standard is free and provides automatic Layer 3/4 DDoS protection, while Shield Advanced costs $3,000/month and includes 24/7 DRT support and cost protection

c) Shield Standard requires manual configuration, while Shield Advanced is automatically enabled for all AWS accounts

d) Shield Standard protects against application layer attacks, while Shield Advanced protects against network layer attacks

---

### Question 3
A financial services company needs to ensure their customer-facing application remains available 24/7 to meet regulatory compliance requirements. They are concerned about DDoS attacks disrupting service availability and want access to AWS security experts during an attack.

Which combination of AWS services would BEST meet these requirements? (Select TWO)

a) AWS Shield Advanced for 24/7 DDoS Response Team support

b) AWS Shield Standard for automatic DDoS protection

c) Amazon GuardDuty for threat detection

d) AWS WAF for application layer protection

e) AWS Config for compliance monitoring

---

### Question 4
AnyCompany Gaming hosts multiplayer game servers on AWS and recently experienced a DDoS attack that made their game unplayable for several hours. They want to prevent future attacks but have a limited budget and cannot afford expensive security solutions.

What is the MOST cost-effective approach to gain immediate DDoS protection?

a) Purchase AWS Shield Advanced subscription for comprehensive protection

b) Rely on AWS Shield Standard, which is automatically enabled and free for all AWS customers

c) Implement AWS WAF with custom rules to block malicious traffic

d) Deploy third-party DDoS protection software on EC2 instances

---

### Question 5
According to the AWS Shared Responsibility Model, which of the following is the CUSTOMER's responsibility when using AWS Shield?

a) Maintaining the physical infrastructure that runs Shield detection systems

b) Updating the threat detection algorithms used by Shield

c) Configuring which AWS resources to protect with Shield Advanced

d) Operating the global network infrastructure that mitigates DDoS attacks

---

### Question 6
AnyCompany Media streams video content globally using Amazon CloudFront. During a viral content release, they experienced massive traffic that could have been a DDoS attack or legitimate user demand. They want protection that distinguishes between attacks and legitimate traffic spikes without incurring scaling charges during actual attacks.

Which AWS Shield feature addresses this requirement?

a) AWS Shield Standard automatic detection

b) AWS Shield Advanced DDoS cost protection

c) AWS Shield traffic filtering rules

d) AWS Shield geo-blocking capabilities

---

### Question 7
A startup company is launching a new web application on AWS and wants to understand what DDoS protection they receive without any additional configuration or cost.

What DDoS protection does AWS provide by default?

a) No protection - customers must purchase AWS Shield Advanced

b) AWS Shield Standard, which protects against common Layer 3 and Layer 4 DDoS attacks at no additional cost

c) AWS WAF protection for application layer attacks included with all AWS accounts

d) Basic protection only for Amazon S3 and CloudFront, requiring Shield Advanced for other services

---

### Question 8
Which AWS services are directly protected by AWS Shield Advanced? (Select TWO)

a) Amazon RDS database instances

b) Amazon Route 53 hosted zones

c) Amazon S3 buckets

d) Amazon CloudFront distributions

e) AWS Lambda functions

---

### Question 9
AnyCompany Healthcare is evaluating AWS Shield Advanced for their patient portal application. The IT director wants to understand the primary cost components before making a purchasing decision.

What are the main costs associated with AWS Shield Advanced?

a) $3,000 per month per organization with a 1-year commitment, plus potential data transfer fees for DRT mitigation actions

b) $3,000 per month per AWS account with no commitment required

c) $300 per month per protected resource with pay-as-you-go pricing

d) Free for the first year, then $3,000 per month based on traffic volume

---

### Question 10
A company uses AWS Shield Advanced to protect their application. During a DDoS attack, they want to receive immediate notifications and view detailed attack metrics.

Which AWS service should they use to monitor Shield events and configure attack notifications?

a) AWS CloudTrail

b) Amazon CloudWatch

c) AWS Config

d) Amazon Inspector

---

## Section 2: Answers and Justifications

### Question 1: Correct Answer - B

**Why B is correct:**
AWS Shield Advanced with DDoS cost protection is the correct solution because it provides two critical features this scenario requires: (1) enhanced DDoS protection beyond Shield Standard, and (2) DDoS cost protection that prevents scaling charges during attacks. Shield Advanced includes credits for scaling costs incurred during DDoS attacks on protected resources like CloudFront and Application Load Balancers, directly addressing the manager's concern about unexpected costs during traffic spikes.

**Why other options are incorrect:**
- **A (Shield Standard with CloudWatch):** Shield Standard is free and provides basic protection, but it does NOT include cost protection against scaling charges during attacks. CloudWatch provides monitoring but doesn't prevent costs.
- **C (AWS WAF with rate-based rules):** WAF protects against application layer (Layer 7) attacks and can limit request rates, but it doesn't provide comprehensive DDoS protection or cost protection for infrastructure scaling during attacks.
- **D (Shield Standard with Auto Scaling):** While Auto Scaling helps handle traffic increases, it doesn't prevent the costs associated with scaling during attacks. Shield Standard lacks the cost protection feature needed.

---

### Question 2: Correct Answer - B

**Why B is correct:**
This accurately describes the key differences between Shield Standard and Advanced: Shield Standard is automatically included at no cost for all AWS customers and protects against common network (Layer 3) and transport (Layer 4) DDoS attacks. Shield Advanced costs $3,000/month, provides 24/7 access to the AWS DDoS Response Team (DRT), includes advanced attack diagnostics, and offers DDoS cost protection. This aligns with CLF-C02 exam objectives around understanding service tiers and pricing models.

**Why other options are incorrect:**
- **A (EC2 only vs all resources):** Incorrect - Shield Standard protects multiple AWS resources (CloudFront, Route 53, ELB, etc.), not just EC2. The difference isn't about resource coverage but about the level of protection and support.
- **C (Manual vs automatic):** Incorrect - Shield Standard is automatically enabled, not manually configured. Shield Advanced requires enrollment but isn't "automatic" for all accounts.
- **D (Application vs network layers):** Incorrect - This reverses the reality. Shield (both tiers) primarily protects against network/transport layer attacks. Application layer protection requires AWS WAF integration.

---

### Question 3: Correct Answers - A and D

**Why A is correct:**
AWS Shield Advanced provides 24/7 access to the AWS DDoS Response Team (DRT), which directly addresses the requirement for "access to AWS security experts during an attack." This specialized support ensures expert assistance is available around the clock to help maintain the required 24/7 availability for regulatory compliance.

**Why D is correct:**
AWS WAF provides application layer (Layer 7) protection, which complements Shield's network/transport layer protection. Together, they create comprehensive defense across all layers. Shield Advanced includes AWS WAF at no additional cost for protected resources, making this combination both effective and cost-efficient for complete DDoS protection.

**Why other options are incorrect:**
- **B (Shield Standard):** While Shield Standard provides automatic protection, it doesn't include 24/7 DRT support, which is specifically required in the scenario.
- **C (GuardDuty):** GuardDuty is a threat detection service that monitors for malicious activity and unauthorized behavior, but it doesn't provide DDoS protection or mitigation capabilities.
- **E (AWS Config):** Config is a compliance monitoring and configuration management service. It doesn't provide DDoS protection or help maintain application availability during attacks.

---

### Question 4: Correct Answer - B

**Why B is correct:**
AWS Shield Standard is the most cost-effective solution because it's completely free and automatically enabled for all AWS customers. It provides protection against the most common network and transport layer DDoS attacks without requiring any configuration or additional cost. For a company with budget constraints, this is the immediate, no-cost protection they need. This aligns with CLF-C02 cost optimization principles.

**Why other options are incorrect:**
- **A (Shield Advanced):** While Shield Advanced provides enhanced protection, it costs $3,000/month with a 1-year commitment, which contradicts the "limited budget" constraint in the scenario.
- **C (AWS WAF with custom rules):** WAF incurs costs based on the number of web ACLs, rules, and requests processed. It also requires configuration expertise and doesn't provide comprehensive network-layer DDoS protection like Shield.
- **D (Third-party software on EC2):** This would incur EC2 instance costs, software licensing fees, and operational overhead for management and maintenance, making it more expensive than the free Shield Standard option.

---

### Question 5: Correct Answer - C

**Why C is correct:**
Under the AWS Shared Responsibility Model, customers are responsible for configuring which resources they want to protect with Shield Advanced (if they choose to enable it). This includes selecting CloudFront distributions, Route 53 hosted zones, Elastic Load Balancers, and other eligible resources for enhanced protection. Configuration and management of AWS services are customer responsibilities. This is a core CLF-C02 exam concept.

**Why other options are incorrect:**
- **A (Physical infrastructure):** AWS is responsible for the physical security and maintenance of all infrastructure, including the hardware and facilities that run Shield. This is part of "Security OF the Cloud."
- **B (Threat detection algorithms):** AWS manages and updates the threat detection algorithms, machine learning models, and mitigation techniques used by Shield. Customers don't have access to or responsibility for these internal systems.
- **D (Global network infrastructure):** AWS operates and maintains the global network infrastructure used for DDoS mitigation. This includes the distributed architecture that absorbs and filters attack traffic.

---

### Question 6: Correct Answer - B

**Why B is correct:**
AWS Shield Advanced DDoS cost protection specifically addresses this scenario. This feature provides credits for scaling charges incurred during DDoS attacks on protected resources (CloudFront, Route 53, ELB, Global Accelerator). If traffic spikes are determined to be DDoS attacks, customers receive credits for the associated scaling costs, preventing unexpected bills. This distinguishes between legitimate traffic (which customers pay for) and attack traffic (which is credited).

**Why other options are incorrect:**
- **A (Shield Standard automatic detection):** While Shield Standard detects and mitigates attacks automatically, it does NOT include cost protection. Customers still pay for scaling charges during attacks with Shield Standard.
- **C (Traffic filtering rules):** Shield doesn't use customer-configured "traffic filtering rules" - it uses AWS-managed detection and mitigation. This option describes a feature more similar to AWS WAF.
- **D (Geo-blocking capabilities):** Geo-blocking (restricting access by geographic location) is a feature of CloudFront and WAF, not Shield. It also doesn't address the cost protection requirement.

---

### Question 7: Correct Answer - B

**Why B is correct:**
AWS Shield Standard is automatically enabled for all AWS customers at no additional cost. It provides protection against the most common and frequently occurring network (Layer 3) and transport (Layer 4) DDoS attacks, including SYN/ACK floods, reflection attacks, and UDP floods. This is a foundational CLF-C02 concept about AWS's built-in security features and the value proposition of AWS Cloud.

**Why other options are incorrect:**
- **A (No protection without Advanced):** Incorrect - AWS provides Shield Standard protection automatically and free to all customers. Shield Advanced is optional for enhanced protection.
- **C (WAF included with all accounts):** Incorrect - AWS WAF is a separate service that incurs charges based on usage. It's not automatically included or free. Shield Standard is the free DDoS protection service.
- **D (Only S3 and CloudFront):** Incorrect - Shield Standard protects multiple AWS services including CloudFront, Route 53, Elastic Load Balancing, AWS Global Accelerator, and Elastic IP addresses on EC2 instances, not just S3 and CloudFront.

---

### Question 8: Correct Answers - B and D

**Why B is correct:**
Amazon Route 53 hosted zones are directly protected by AWS Shield Advanced. Shield Advanced provides enhanced DDoS protection for Route 53, defending against DNS query floods and other DNS-targeted attacks. This ensures DNS resolution remains available even during large-scale attacks, which is critical for application availability.

**Why D is correct:**
Amazon CloudFront distributions are primary resources protected by AWS Shield Advanced. CloudFront's global edge network combined with Shield Advanced provides distributed DDoS defense with enhanced detection, mitigation, and 24/7 DRT support. CloudFront is one of the core services eligible for Shield Advanced protection and DDoS cost protection.

**Why other options are incorrect:**
- **A (RDS database instances):** RDS instances are not directly protected by Shield Advanced. However, they can benefit indirectly if they're behind protected resources like Application Load Balancers. Shield Advanced specifically protects edge services and load balancers.
- **C (S3 buckets):** S3 buckets are not directly protected by Shield Advanced. S3 has built-in DDoS resilience, but Shield Advanced protection applies to CloudFront distributions that serve S3 content, not the buckets themselves.
- **E (Lambda functions):** Lambda functions are not directly protected by Shield Advanced. Lambda's serverless architecture provides inherent DDoS resilience, but Shield Advanced focuses on protecting network-facing resources like CloudFront, Route 53, and load balancers.

---

### Question 9: Correct Answer - A

**Why A is correct:**
AWS Shield Advanced costs $3,000 per month per organization (not per account) with a 1-year subscription commitment. Additional charges may apply for data transfer fees associated with DDoS Response Team (DRT) mitigation actions if the DRT needs to apply advanced mitigation techniques. This pricing structure is important for CLF-C02 exam understanding of AWS billing models and cost considerations.

**Why other options are incorrect:**
- **B (Per account with no commitment):** Incorrect - Shield Advanced is priced per organization (covering all accounts in an AWS Organization), not per individual account. It also requires a 1-year commitment, not pay-as-you-go.
- **C ($300 per resource):** Incorrect - Shield Advanced doesn't charge per protected resource. The $3,000/month fee covers protection for multiple eligible resources within the organization. This pricing model would be prohibitively expensive for most use cases.
- **D (Free first year):** Incorrect - Shield Advanced is not free for any period. It costs $3,000/month from the start of the subscription. There is no free trial or introductory period for Shield Advanced.

---

### Question 10: Correct Answer - B

**Why B is correct:**
Amazon CloudWatch is the correct service for monitoring AWS Shield events and configuring attack notifications. Shield publishes DDoS attack metrics to CloudWatch, including DDoSDetected, DDoSAttackBitsPerSecond, and DDoSAttackPacketsPerSecond. Customers can create CloudWatch alarms to receive notifications when attacks are detected and view detailed metrics through CloudWatch dashboards. This integration is essential for operational visibility during security events.

**Why other options are incorrect:**
- **A (CloudTrail):** CloudTrail logs API calls and account activity for auditing and compliance, but it doesn't provide real-time attack metrics or monitoring for DDoS events. CloudTrail is for governance and compliance tracking, not operational monitoring.
- **C (AWS Config):** Config tracks resource configuration changes and compliance status over time. It doesn't monitor real-time security events like DDoS attacks or provide attack metrics and notifications.
- **D (Amazon Inspector):** Inspector is a vulnerability assessment service that scans EC2 instances and container images for security vulnerabilities and compliance issues. It doesn't monitor DDoS attacks or provide Shield event notifications.
