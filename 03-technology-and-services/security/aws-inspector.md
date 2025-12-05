# AWS Inspector

## Service Overview

AWS Inspector is an automated security assessment service that continuously scans AWS workloads for software vulnerabilities and unintended network exposure to help improve security and compliance.

### 💡 Foundational Concepts

**What Problem Does It Solve?**

Organizations running applications on AWS face security challenges:
- **Software vulnerabilities:** Applications may have known security flaws (CVEs - Common Vulnerabilities and Exposures)
- **Outdated packages:** Operating systems and libraries with unpatched security issues
- **Network exposure:** Resources accidentally exposed to the internet or overly permissive security groups
- **Compliance requirements:** Need to prove security posture for audits (PCI-DSS, HIPAA, SOC 2)
- **Manual scanning is slow:** Manually checking hundreds of EC2 instances and containers for vulnerabilities is impractical

Traditional vulnerability scanning requires:
- Installing and maintaining scanning software
- Scheduling regular scans
- Manually reviewing and prioritizing findings
- Tracking remediation efforts

**Core Value Proposition:**

AWS Inspector automatically and continuously scans your EC2 instances, container images (ECR), and Lambda functions for software vulnerabilities and network configuration issues. It provides a risk score for each finding, prioritizes remediation based on severity, and integrates with AWS Security Hub for centralized security management—all without installing agents or managing scanning infrastructure.

**Simple Analogy:** Think of Inspector as an automated security guard that continuously patrols your AWS environment, checking every door and window (network exposure) and inspecting every piece of equipment (software) for defects or vulnerabilities. It creates a detailed report of issues found, prioritized by severity, so you know what to fix first.

### 🌐 Key Benefits & Value Proposition

**1. Automated Continuous Scanning (Operational Excellence)**
- Automatically scans EC2 instances, container images, and Lambda functions
- Continuous monitoring (not just point-in-time scans)
- No need to schedule or trigger scans manually
- **Cloud Advantage:** *Automation* - Eliminates manual vulnerability scanning processes

**2. Comprehensive Vulnerability Detection**
- Identifies software vulnerabilities (CVEs) in operating systems and applications
- Detects unintended network exposure and overly permissive security groups
- Scans container images in Amazon ECR for vulnerabilities
- **Cloud Advantage:** *Security at scale* - Automated security across entire infrastructure

**3. Risk-Based Prioritization**
- Assigns risk scores to findings (Critical, High, Medium, Low)
- Prioritizes vulnerabilities based on exploitability and impact
- Provides remediation guidance for each finding
- **Cloud Advantage:** *Intelligent insights* - Focus on highest-risk issues first

**4. Agentless Scanning (Simplified Management)**
- No agents to install or manage for EC2 instances (uses SSM Agent)
- Automatic scanning of ECR container images on push
- Lambda function scanning without code changes
- **Cloud Advantage:** *Reduced operational overhead* - No scanning infrastructure to maintain

**5. Integrated Security Management**
- Automatic integration with AWS Security Hub
- Findings sent to Amazon EventBridge for automated responses
- Centralized view of security posture across AWS accounts
- **Cloud Advantage:** *Built-in integration* - Works seamlessly with AWS security ecosystem

### 🔒 Security and Compliance (CLF-C02 Focus)

**AWS Shared Responsibility Model:**

| **AWS Responsibility (Security OF the Cloud)** | **Customer Responsibility (Security IN the Cloud)** |
|---|---|
| ✅ Physical security of Inspector infrastructure | ✅ Enable Inspector in AWS accounts and regions |
| ✅ Service availability and scalability | ✅ Define which resources to scan (EC2, ECR, Lambda) |
| ✅ Vulnerability database updates | ✅ Review and remediate Inspector findings |
| ✅ Scanning engine maintenance | ✅ Patch vulnerable software and update packages |
| ✅ API security and access controls | ✅ Configure network security groups based on findings |
| ✅ Integration with AWS services | ✅ Manage IAM permissions for Inspector access |
| ✅ Findings data encryption | ✅ Set up automated responses via EventBridge |

**Key Security Features:**

- **Continuous Vulnerability Scanning:** Automatically scans for CVEs in software packages
- **Network Reachability Analysis:** Identifies unintended network exposure
- **Container Image Scanning:** Scans ECR images for vulnerabilities before deployment
- **Lambda Function Scanning:** Detects vulnerabilities in Lambda code dependencies
- **Risk Scoring:** CVSS (Common Vulnerability Scoring System) scores for prioritization
- **Remediation Guidance:** Provides specific steps to fix vulnerabilities
- **Multi-Account Support:** Centralized scanning across AWS Organizations

**What Inspector Scans:**

**1. Amazon EC2 Instances:**
- Operating system vulnerabilities (Linux and Windows)
- Application vulnerabilities in installed packages
- Network exposure and security group misconfigurations
- Requires SSM Agent (pre-installed on AWS-provided AMIs)

**2. Amazon ECR Container Images:**
- Vulnerabilities in container image layers
- Operating system packages in containers
- Application dependencies
- Scans on image push and continuously

**3. AWS Lambda Functions:**
- Vulnerabilities in function code dependencies
- Application packages and libraries
- Scans on deployment and continuously

**Compliance Support:**
- Helps meet PCI-DSS requirements (vulnerability management)
- Supports HIPAA compliance (security assessments)
- Assists with SOC 2, ISO 27001 compliance
- Provides evidence for security audits
- CIS (Center for Internet Security) benchmark checks

**Finding Types:**

- **Package Vulnerabilities:** Known CVEs in installed software
- **Network Reachability:** Resources accessible from the internet
- **Code Vulnerabilities:** Issues in Lambda function dependencies

### 💰 Billing, Pricing, and Support

**Pricing Model: Pay-As-You-Go (Per Resource Scanned)**

**1. Amazon EC2 Instance Scanning:**
- **$1.50 per instance per month**
- Charged for each EC2 instance scanned
- Includes continuous scanning (not per-scan pricing)
- Prorated for partial months

**2. Amazon ECR Container Image Scanning:**
- **$0.09 per image scan** (on push)
- **$0.01 per image per month** for continuous monitoring (re-scan)
- Charged per unique image (not per tag)

**3. AWS Lambda Function Scanning:**
- **$0.60 per function per month**
- Charged for each Lambda function scanned
- Includes continuous scanning

**Pricing Examples:**

**Example 1: Small Startup**
- 10 EC2 instances
- 5 ECR images (scanned monthly)
- 3 Lambda functions
- **Cost:** (10 × $1.50) + (5 × $0.09) + (5 × $0.01) + (3 × $0.60) = $15 + $0.45 + $0.05 + $1.80 = **$17.30/month**

**Example 2: Medium Business**
- 100 EC2 instances
- 50 ECR images (scanned weekly, 4 times/month)
- 20 Lambda functions
- **Cost:** (100 × $1.50) + (50 × 4 × $0.09) + (50 × $0.01) + (20 × $0.60) = $150 + $18 + $0.50 + $12 = **$180.50/month**

**Example 3: Enterprise**
- 1,000 EC2 instances
- 200 ECR images (scanned daily, 30 times/month)
- 100 Lambda functions
- **Cost:** (1,000 × $1.50) + (200 × 30 × $0.09) + (200 × $0.01) + (100 × $0.60) = $1,500 + $540 + $2 + $60 = **$2,102/month**

**Free Trial:**
- **15-day free trial** for new accounts
- Includes EC2, ECR, and Lambda scanning
- Evaluate Inspector before committing

**Cost Optimization Tips:**
- Enable Inspector only in regions where you have resources
- Scan ECR images on push (not continuously) if images rarely change
- Use tags to exclude non-production resources from scanning
- Leverage the 15-day free trial to assess value
- Disable scanning for decommissioned resources

**Support:**
- Available under all AWS Support Plans
- 24/7 support for Business and Enterprise plans
- Integration with AWS Security Hub for centralized management
- Extensive documentation and best practices

### 🎯 Common Use Cases (Scenario-Based)

**1. Continuous Vulnerability Management**
- **Scenario:** A SaaS company runs 200 EC2 instances and needs to continuously monitor for security vulnerabilities to meet SOC 2 compliance requirements.
- **Solution:** Enable AWS Inspector to automatically scan all EC2 instances for CVEs, prioritize findings by risk score, and remediate critical vulnerabilities.
- **Benefit:** Continuous security monitoring, compliance evidence for audits, reduced risk of exploitation.

**2. Container Security Before Deployment**
- **Scenario:** A development team uses Docker containers stored in Amazon ECR and wants to ensure no vulnerable images are deployed to production.
- **Solution:** Enable Inspector for ECR to automatically scan container images on push, block deployment of images with critical vulnerabilities.
- **Benefit:** Prevents vulnerable containers from reaching production, shift-left security approach.

**3. Serverless Application Security**
- **Scenario:** A fintech company uses AWS Lambda for payment processing and must ensure Lambda functions don't have vulnerable dependencies.
- **Solution:** Enable Inspector for Lambda to scan function code dependencies for known vulnerabilities, receive alerts for critical findings.
- **Benefit:** Secure serverless applications, meet PCI-DSS requirements, protect sensitive financial data.

**4. Network Exposure Detection**
- **Scenario:** A healthcare organization wants to ensure no EC2 instances with patient data are accidentally exposed to the internet.
- **Solution:** Use Inspector's network reachability analysis to identify instances accessible from the internet, remediate overly permissive security groups.
- **Benefit:** Prevent data breaches, maintain HIPAA compliance, reduce attack surface.

**5. Multi-Account Security Posture**
- **Scenario:** An enterprise with 50 AWS accounts needs centralized visibility into vulnerabilities across all accounts.
- **Solution:** Enable Inspector across all accounts using AWS Organizations, aggregate findings in Security Hub for centralized management.
- **Benefit:** Unified security view, consistent security policies, simplified compliance reporting.

### 🔗 Related Core Services

**1. Amazon EC2 (Elastic Compute Cloud)**
- **Relationship:** Inspector scans EC2 instances for vulnerabilities and network exposure
- **Integration:** Requires SSM Agent on EC2 instances (pre-installed on AWS AMIs)
- **CLF-C02 Context:** EC2 runs applications; Inspector secures those applications

**2. Amazon ECR (Elastic Container Registry)**
- **Relationship:** Inspector scans container images stored in ECR for vulnerabilities
- **Integration:** Automatic scanning on image push to ECR repositories
- **CLF-C02 Context:** ECR stores container images; Inspector ensures images are secure

**3. AWS Lambda**
- **Relationship:** Inspector scans Lambda function code dependencies for vulnerabilities
- **Integration:** Automatic scanning when Lambda functions are deployed or updated
- **CLF-C02 Context:** Lambda runs serverless code; Inspector secures function dependencies

**4. AWS Security Hub**
- **Relationship:** Security Hub aggregates Inspector findings with other AWS security service findings
- **Integration:** Inspector automatically sends findings to Security Hub for centralized management
- **CLF-C02 Context:** Security Hub provides unified security view; Inspector contributes vulnerability findings

**5. Amazon EventBridge (formerly CloudWatch Events)**
- **Relationship:** EventBridge receives Inspector findings and triggers automated responses
- **Integration:** Create EventBridge rules to trigger Lambda functions, SNS notifications, or other actions based on Inspector findings
- **CLF-C02 Context:** EventBridge enables automated remediation; Inspector provides security findings

**6. AWS Systems Manager**
- **Relationship:** Inspector uses SSM Agent to scan EC2 instances
- **Integration:** SSM Agent must be installed and running on EC2 instances for Inspector to scan them
- **CLF-C02 Context:** Systems Manager provides agent infrastructure; Inspector uses it for scanning

**7. AWS Organizations**
- **Relationship:** Enables centralized Inspector management across multiple AWS accounts
- **Integration:** Designate an Inspector administrator account to manage findings across all member accounts
- **CLF-C02 Context:** Organizations provides multi-account structure; Inspector provides cross-account security scanning

**8. AWS Identity and Access Management (IAM)**
- **Relationship:** IAM controls who can enable Inspector, view findings, and configure scans
- **Integration:** IAM policies define permissions for Inspector operations
- **CLF-C02 Context:** IAM provides access control; Inspector provides vulnerability scanning

### 📊 AWS Inspector vs. Other AWS Security Services

**Quick Comparison (CLF-C02 Exam Context):**

| Service | Primary Purpose | What It Scans/Protects |
|---------|----------------|------------------------|
| **AWS Inspector** | Vulnerability scanning | EC2 instances, ECR images, Lambda functions |
| **Amazon GuardDuty** | Threat detection | AWS accounts, workloads, data (malicious activity) |
| **AWS Macie** | Data security | S3 buckets (sensitive data discovery) |
| **AWS Security Hub** | Centralized security | Aggregates findings from multiple services |
| **AWS Config** | Configuration compliance | Resource configuration changes |
| **AWS WAF** | Web application firewall | Web applications (HTTP/HTTPS attacks) |
| **AWS Shield** | DDoS protection | Applications (DDoS attacks) |

**Key Differences:**

- **Inspector:** Finds vulnerabilities in software and network configurations
- **GuardDuty:** Detects active threats and malicious behavior
- **Macie:** Discovers sensitive data in S3
- **Security Hub:** Aggregates findings from all security services

**Exam Tip:** Choose Inspector when the scenario mentions **"vulnerability scanning,"** **"CVE detection,"** **"container image security,"** or **"software vulnerabilities."**

### ✅ Key Exam Points

**Remember for CLF-C02:**

✅ **Primary Purpose:** Automated vulnerability scanning for EC2, ECR, and Lambda  
✅ **Continuous Scanning:** Not point-in-time; continuously monitors for new vulnerabilities  
✅ **What It Scans:** EC2 instances, ECR container images, Lambda functions  
✅ **Agentless:** Uses existing SSM Agent (no additional agent installation)  
✅ **Pricing:** $1.50/EC2/month, $0.09/ECR scan, $0.60/Lambda/month  
✅ **Findings:** Software vulnerabilities (CVEs) and network exposure  
✅ **Risk Scoring:** Prioritizes findings by severity (Critical, High, Medium, Low)  
✅ **Integration:** Works with Security Hub, EventBridge, Organizations  
✅ **Compliance:** Helps meet PCI-DSS, HIPAA, SOC 2 requirements  
✅ **Use Case Keywords:** "vulnerability scanning," "CVE detection," "container security," "software vulnerabilities"

### 🎓 Practice Scenarios

**Scenario 1:** A company needs to scan EC2 instances for known software vulnerabilities to meet PCI-DSS compliance requirements.  
**Answer:** AWS Inspector (automated vulnerability scanning for EC2)

**Scenario 2:** An organization wants to detect malicious activity and threats across their AWS account, including unusual API calls and compromised credentials.  
**Answer:** Amazon GuardDuty (threat detection, not Inspector which scans for vulnerabilities)

**Scenario 3:** A development team wants to ensure Docker container images don't have critical vulnerabilities before deploying to production.  
**Answer:** AWS Inspector for ECR (scans container images for CVEs)

**Scenario 4:** A business needs to discover which S3 buckets contain personally identifiable information (PII) for GDPR compliance.  
**Answer:** AWS Macie (data discovery in S3, not Inspector which scans for vulnerabilities)

**Scenario 5:** A company wants to identify EC2 instances that are unintentionally exposed to the internet due to misconfigured security groups.  
**Answer:** AWS Inspector (network reachability analysis)

**Scenario 6:** An enterprise needs centralized visibility into security findings from Inspector, GuardDuty, and Macie across 100 AWS accounts.  
**Answer:** AWS Security Hub (aggregates findings from multiple services)

**Scenario 7:** A serverless application using Lambda functions needs to be scanned for vulnerable code dependencies.  
**Answer:** AWS Inspector for Lambda (scans function dependencies for CVEs)

---

## Official AWS Documentation

- [AWS Inspector Official Documentation](https://docs.aws.amazon.com/inspector/)
- [AWS Inspector FAQs](https://aws.amazon.com/inspector/faqs/)
- [AWS Inspector Pricing](https://aws.amazon.com/inspector/pricing/)
- [AWS Inspector User Guide](https://docs.aws.amazon.com/inspector/latest/user/what-is-inspector.html)
- [AWS Inspector Findings](https://docs.aws.amazon.com/inspector/latest/user/findings.html)
- [AWS Inspector Best Practices](https://docs.aws.amazon.com/inspector/latest/user/inspector-best-practices.html)
- [Scanning Amazon ECR with Inspector](https://docs.aws.amazon.com/inspector/latest/user/enable-disable-scanning-ecr.html)
