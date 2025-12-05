# AWS GuardDuty

## Service Overview

AWS GuardDuty is an intelligent threat detection service that continuously monitors AWS accounts, workloads, and data for malicious activity and unauthorized behavior using machine learning and threat intelligence.

### 💡 Foundational Concepts

**What Problem Does It Solve?**

Organizations face sophisticated security threats that traditional security tools may miss:
- **Compromised credentials:** Stolen AWS access keys used by attackers
- **Unusual API calls:** Suspicious activity indicating account compromise
- **Cryptocurrency mining:** Unauthorized use of EC2 instances for mining
- **Data exfiltration:** Attempts to steal data from S3 buckets
- **Malware and backdoors:** Malicious software on EC2 instances
- **Port scanning and reconnaissance:** Attackers probing for vulnerabilities
- **Insider threats:** Malicious activity from within the organization

Traditional security monitoring requires:
- Installing and maintaining security software
- Analyzing massive amounts of log data manually
- Keeping threat intelligence databases updated
- 24/7 security operations center (SOC) staffing
- Expertise in identifying attack patterns

**Core Value Proposition:**

AWS GuardDuty eliminates the complexity of threat detection by continuously analyzing billions of events across your AWS accounts using machine learning, anomaly detection, and integrated threat intelligence. It automatically identifies suspicious activity (like compromised EC2 instances, unusual API calls, or data exfiltration attempts) and provides actionable security findings—all without deploying agents or managing infrastructure.

**Simple Analogy:** Think of GuardDuty as an intelligent security camera system with AI that watches your entire AWS environment 24/7. Instead of just recording everything, it learns normal behavior patterns and immediately alerts you when something suspicious happens—like someone using stolen keys to access your account or an EC2 instance suddenly communicating with known malicious servers.

### 🌐 Key Benefits & Value Proposition

**1. Intelligent Threat Detection (Security at Scale)**
- Uses machine learning to identify anomalous behavior
- Integrated threat intelligence from AWS, CrowdStrike, and Proofpoint
- Detects known malicious IPs, domains, and attack patterns
- **Cloud Advantage:** *Built-in intelligence* - Enterprise-grade threat detection without managing threat feeds

**2. Continuous Monitoring (Operational Excellence)**
- 24/7 automated monitoring of AWS accounts and workloads
- No agents to install or maintain
- Analyzes billions of events in real-time
- **Cloud Advantage:** *Automation* - Eliminates need for manual log analysis and 24/7 SOC staffing

**3. Comprehensive Coverage**
- Monitors AWS CloudTrail events (API calls and account activity)
- Analyzes VPC Flow Logs (network traffic patterns)
- Examines DNS logs (domain name queries)
- Scans S3 data access patterns
- Monitors EKS audit logs (Kubernetes activity)
- **Cloud Advantage:** *Unified security* - Single service monitors multiple data sources

**4. Easy to Enable (Agility)**
- Enable with a single click in AWS Console
- No infrastructure to deploy or manage
- Starts providing findings within minutes
- **Cloud Advantage:** *Rapid deployment* - Security in minutes, not weeks

**5. Cost-Effective Security**
- Pay only for events analyzed (no upfront costs)
- No need to purchase and maintain SIEM tools
- Reduces need for expensive security operations staff
- **Cloud Advantage:** *Pay-as-you-go* - No capital expenditure on security infrastructure

### 🔒 Security and Compliance (CLF-C02 Focus)

**AWS Shared Responsibility Model:**

| **AWS Responsibility (Security OF the Cloud)** | **Customer Responsibility (Security IN the Cloud)** |
|---|---|
| ✅ Physical security of GuardDuty infrastructure | ✅ Enable GuardDuty in AWS accounts and regions |
| ✅ Service availability and scalability | ✅ Review and respond to GuardDuty findings |
| ✅ Threat intelligence database updates | ✅ Configure automated responses (EventBridge) |
| ✅ Machine learning model training and updates | ✅ Investigate and remediate security threats |
| ✅ Data source integration (CloudTrail, VPC Flow Logs, DNS) | ✅ Manage IAM permissions for GuardDuty access |
| ✅ Encryption of findings data | ✅ Configure trusted IP lists and threat lists |
| ✅ Service patching and maintenance | ✅ Enable GuardDuty across all AWS accounts (Organizations) |

**Key Security Features:**

- **Multi-Account Support:** Centralized monitoring across AWS Organizations
- **Threat Intelligence:** Integrated feeds from AWS, CrowdStrike, Proofpoint
- **Machine Learning:** Detects anomalies based on baseline behavior
- **Severity Levels:** Findings categorized as Low, Medium, High
- **Automated Responses:** Integration with EventBridge for automated remediation
- **No Data Movement:** Analyzes metadata only; doesn't access actual data
- **IAM Integration:** Fine-grained access control for findings

**What GuardDuty Detects:**

**1. Compromised Credentials:**
- AWS access keys used from unusual locations
- API calls from known malicious IPs
- Impossible travel (API calls from distant locations in short time)
- Disabled CloudTrail logging (attacker covering tracks)

**2. Compromised EC2 Instances:**
- EC2 instance communicating with known malware servers
- Cryptocurrency mining activity
- Backdoor communication patterns
- Port scanning and reconnaissance activity
- Unusual network traffic patterns

**3. Compromised S3 Buckets:**
- Suspicious data access patterns
- Unusual API calls to S3 buckets
- Data exfiltration attempts
- Anonymous access to sensitive buckets

**4. Reconnaissance Activity:**
- Port scanning from EC2 instances
- Unusual API call patterns (enumeration)
- Brute force login attempts
- Suspicious DNS queries

**5. Kubernetes Threats (EKS):**
- Suspicious container activity
- Privilege escalation attempts
- Anonymous access to Kubernetes APIs

**Finding Types Examples:**
- **UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration** - EC2 credentials used outside AWS
- **CryptoCurrency:EC2/BitcoinTool.B!DNS** - EC2 instance mining cryptocurrency
- **Backdoor:EC2/C&CActivity.B!DNS** - EC2 communicating with command & control server
- **Recon:EC2/PortProbeUnprotectedPort** - Port scanning activity detected

**Compliance Support:**
- Helps meet PCI-DSS requirements (threat detection)
- Supports HIPAA compliance (security monitoring)
- Assists with SOC 2, ISO 27001 compliance
- Provides evidence for security audits
- CIS AWS Foundations Benchmark alignment

### 💰 Billing, Pricing, and Support

**Pricing Model: Pay-As-You-Go (Per Million Events Analyzed)**

**1. CloudTrail Event Analysis (Management Events):**
- **First 500,000 events/month:** $4.50 per million events
- **Next 2 million events/month:** $2.00 per million events
- **Over 2.5 million events/month:** $0.50 per million events
- Tiered pricing reduces cost at scale

**2. VPC Flow Log and DNS Log Analysis:**
- **First 500 GB/month:** $1.00 per GB
- **Next 2,000 GB/month:** $0.50 per GB
- **Over 2,500 GB/month:** $0.25 per GB
- Tiered pricing for network traffic analysis

**3. S3 Data Event Analysis:**
- **First 500,000 events/month:** $0.80 per million events
- **Next 2 million events/month:** $0.40 per million events
- **Over 2.5 million events/month:** $0.20 per million events

**4. EKS Audit Log Analysis:**
- **First 500,000 events/month:** $0.80 per million events
- **Next 2 million events/month:** $0.40 per million events
- **Over 2.5 million events/month:** $0.20 per million events

**Pricing Examples:**

**Example 1: Small Business**
- 1 million CloudTrail events/month
- 100 GB VPC Flow Logs/month
- No S3 or EKS monitoring
- **Cost:** (0.5M × $4.50/M) + (0.5M × $2.00/M) + (100 × $1.00) = $2.25 + $1.00 + $100 = **$103.25/month**

**Example 2: Medium Business**
- 5 million CloudTrail events/month
- 1,000 GB VPC Flow Logs/month
- 2 million S3 events/month
- **Cost:** (0.5M × $4.50/M) + (2M × $2.00/M) + (2.5M × $0.50/M) + (500GB × $1.00) + (500GB × $0.50) = $2.25 + $4.00 + $1.25 + $500 + $250 = **$757.50/month**

**Example 3: Enterprise**
- 20 million CloudTrail events/month
- 5,000 GB VPC Flow Logs/month
- 10 million S3 events/month
- **Cost:** Approximately **$2,500-$3,000/month** (with tiered pricing discounts)

**Free Trial:**
- **30-day free trial** for new accounts
- Includes all GuardDuty features
- Full functionality to evaluate findings

**Cost Optimization Tips:**
- Enable GuardDuty only in regions where you have resources
- Use trusted IP lists to reduce false positives
- Leverage the 30-day free trial to assess value
- Monitor usage with AWS Cost Explorer
- Consider disabling S3 or EKS monitoring if not needed

**Support:**
- Available under all AWS Support Plans
- 24/7 support for Business and Enterprise plans
- Integration with AWS Security Hub for centralized management
- Extensive documentation and best practices

### 🎯 Common Use Cases (Scenario-Based)

**1. Detecting Compromised AWS Credentials**
- **Scenario:** A company's AWS access keys are accidentally committed to a public GitHub repository. Attackers find and use these credentials to access the AWS account.
- **Solution:** GuardDuty detects unusual API calls from the compromised credentials (different location, unusual services accessed) and generates a high-severity finding.
- **Benefit:** Immediate alert enables rapid response to revoke credentials before significant damage occurs.

**2. Identifying Cryptocurrency Mining**
- **Scenario:** An attacker exploits a vulnerability in a web application to gain access to EC2 instances and installs cryptocurrency mining software.
- **Solution:** GuardDuty detects the EC2 instance communicating with known cryptocurrency mining pools and generates a finding.
- **Benefit:** Stops unauthorized resource usage, prevents inflated AWS bills, and removes malware.

**3. Preventing Data Exfiltration from S3**
- **Scenario:** An insider or attacker attempts to download large amounts of sensitive data from S3 buckets to an external location.
- **Solution:** GuardDuty detects unusual S3 data access patterns (large volume, unusual time, suspicious destination) and alerts security team.
- **Benefit:** Prevents data breaches, protects sensitive information, maintains compliance.

**4. Detecting Reconnaissance and Port Scanning**
- **Scenario:** An attacker gains access to an EC2 instance and uses it to scan the network for other vulnerable systems.
- **Solution:** GuardDuty detects port scanning activity from the compromised EC2 instance and generates a finding.
- **Benefit:** Identifies compromised instances early, prevents lateral movement, limits attack scope.

**5. Multi-Account Security Monitoring**
- **Scenario:** An enterprise with 100 AWS accounts needs centralized threat detection across all accounts without deploying agents or tools in each account.
- **Solution:** Enable GuardDuty across all accounts using AWS Organizations, designate a GuardDuty administrator account to view all findings centrally.
- **Benefit:** Unified security monitoring, consistent threat detection, simplified management.

**6. Kubernetes Security (EKS)**
- **Scenario:** A containerized application running on Amazon EKS experiences suspicious activity, potentially indicating a container escape or privilege escalation attempt.
- **Solution:** GuardDuty monitors EKS audit logs and detects suspicious Kubernetes API calls or container behavior.
- **Benefit:** Protects containerized workloads, detects container-specific threats, maintains EKS security.

### 🔗 Related Core Services

**1. AWS Security Hub**
- **Relationship:** Security Hub aggregates GuardDuty findings with other AWS security service findings
- **Integration:** GuardDuty automatically sends findings to Security Hub for centralized security management
- **CLF-C02 Context:** Security Hub provides unified security view; GuardDuty contributes threat detection findings

**2. Amazon EventBridge (formerly CloudWatch Events)**
- **Relationship:** EventBridge receives GuardDuty findings and triggers automated responses
- **Integration:** Create EventBridge rules to trigger Lambda functions, SNS notifications, or automated remediation based on GuardDuty findings
- **CLF-C02 Context:** EventBridge enables automated incident response; GuardDuty provides threat findings

**3. AWS CloudTrail**
- **Relationship:** GuardDuty analyzes CloudTrail logs to detect suspicious API activity
- **Integration:** GuardDuty automatically accesses CloudTrail data (no configuration needed)
- **CLF-C02 Context:** CloudTrail logs API calls; GuardDuty analyzes those logs for threats

**4. Amazon VPC (Virtual Private Cloud)**
- **Relationship:** GuardDuty analyzes VPC Flow Logs to detect network-based threats
- **Integration:** GuardDuty automatically analyzes VPC Flow Logs (no need to enable Flow Logs separately)
- **CLF-C02 Context:** VPC provides network isolation; GuardDuty monitors network traffic for threats

**5. Amazon S3**
- **Relationship:** GuardDuty monitors S3 data events to detect suspicious access patterns
- **Integration:** Enable S3 protection in GuardDuty to monitor S3 bucket activity
- **CLF-C02 Context:** S3 stores data; GuardDuty protects against data exfiltration

**6. AWS Identity and Access Management (IAM)**
- **Relationship:** IAM controls who can enable GuardDuty, view findings, and configure settings
- **Integration:** IAM policies define permissions for GuardDuty operations
- **CLF-C02 Context:** IAM provides access control; GuardDuty detects compromised credentials

**7. AWS Organizations**
- **Relationship:** Enables centralized GuardDuty management across multiple AWS accounts
- **Integration:** Designate a GuardDuty administrator account to manage findings across all member accounts
- **CLF-C02 Context:** Organizations provides multi-account structure; GuardDuty provides cross-account threat detection

**8. AWS Lambda**
- **Relationship:** Lambda functions can be triggered by GuardDuty findings for automated remediation
- **Integration:** Use EventBridge to trigger Lambda functions when GuardDuty detects threats
- **CLF-C02 Context:** Lambda executes remediation logic; GuardDuty provides threat findings

### 📊 AWS GuardDuty vs. Other AWS Security Services

**Quick Comparison (CLF-C02 Exam Context):**

| Service | Primary Purpose | What It Detects/Protects |
|---------|----------------|--------------------------|
| **AWS GuardDuty** | Threat detection | Malicious activity, compromised credentials, unusual behavior |
| **AWS Inspector** | Vulnerability scanning | Software vulnerabilities (CVEs) in EC2, ECR, Lambda |
| **AWS Macie** | Data security | Sensitive data (PII) in S3 buckets |
| **AWS Security Hub** | Centralized security | Aggregates findings from multiple services |
| **AWS Config** | Configuration compliance | Resource configuration changes and compliance |
| **AWS WAF** | Web application firewall | HTTP/HTTPS attacks on web applications |
| **AWS Shield** | DDoS protection | Distributed denial-of-service attacks |

**Key Differences:**

- **GuardDuty:** Detects active threats and malicious behavior (threat detection)
- **Inspector:** Finds vulnerabilities in software (vulnerability scanning)
- **Macie:** Discovers sensitive data in S3 (data classification)
- **Security Hub:** Aggregates findings from all security services (centralized management)

**Exam Tip:** Choose GuardDuty when the scenario mentions **"threat detection,"** **"malicious activity,"** **"compromised credentials,"** **"unusual behavior,"** or **"cryptocurrency mining."**

### ✅ Key Exam Points

**Remember for CLF-C02:**

✅ **Primary Purpose:** Intelligent threat detection for AWS accounts and workloads  
✅ **Continuous Monitoring:** 24/7 automated monitoring using machine learning  
✅ **No Agents Required:** Analyzes existing AWS data sources (CloudTrail, VPC Flow Logs, DNS)  
✅ **What It Detects:** Compromised credentials, malicious activity, cryptocurrency mining, data exfiltration  
✅ **Pricing:** Pay per million events analyzed (tiered pricing)  
✅ **30-Day Free Trial:** Full functionality for evaluation  
✅ **Easy to Enable:** Single click in AWS Console, no infrastructure to deploy  
✅ **Integration:** Works with Security Hub, EventBridge, Organizations  
✅ **Threat Intelligence:** Uses AWS, CrowdStrike, and Proofpoint threat feeds  
✅ **Use Case Keywords:** "threat detection," "malicious activity," "compromised credentials," "unusual behavior"

### 🎓 Practice Scenarios

**Scenario 1:** A company wants to detect if AWS access keys are compromised and used by attackers from unusual locations.  
**Answer:** AWS GuardDuty (detects compromised credentials and unusual API activity)

**Scenario 2:** An organization needs to scan EC2 instances for software vulnerabilities and missing security patches.  
**Answer:** AWS Inspector (vulnerability scanning, not GuardDuty which detects threats)

**Scenario 3:** A business wants to identify which S3 buckets contain credit card numbers and personally identifiable information.  
**Answer:** AWS Macie (data discovery in S3, not GuardDuty which detects threats)

**Scenario 4:** A company suspects an EC2 instance is being used for unauthorized cryptocurrency mining.  
**Answer:** AWS GuardDuty (detects cryptocurrency mining activity)

**Scenario 5:** An enterprise needs centralized visibility into security findings from GuardDuty, Inspector, and Macie across 50 AWS accounts.  
**Answer:** AWS Security Hub (aggregates findings from multiple services)

**Scenario 6:** A security team wants to automatically isolate compromised EC2 instances when GuardDuty detects malicious activity.  
**Answer:** Use GuardDuty + EventBridge + Lambda for automated remediation

**Scenario 7:** A company wants to detect unusual network traffic patterns indicating data exfiltration attempts.  
**Answer:** AWS GuardDuty (analyzes VPC Flow Logs for network threats)

**Scenario 8:** An organization needs to monitor Kubernetes clusters (EKS) for suspicious container activity and privilege escalation.  
**Answer:** AWS GuardDuty with EKS protection enabled

---

## Official AWS Documentation

- [AWS GuardDuty Official Documentation](https://docs.aws.amazon.com/guardduty/)
- [AWS GuardDuty FAQs](https://aws.amazon.com/guardduty/faqs/)
- [AWS GuardDuty Pricing](https://aws.amazon.com/guardduty/pricing/)
- [AWS GuardDuty User Guide](https://docs.aws.amazon.com/guardduty/latest/ug/what-is-guardduty.html)
- [AWS GuardDuty Findings](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings.html)
- [AWS GuardDuty Best Practices](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_best-practices.html)
- [Automated Response to GuardDuty Findings](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings_cloudwatch.html)
