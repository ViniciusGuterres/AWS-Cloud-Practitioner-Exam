# AWS Detective

## Service Overview

AWS Detective is a security investigation service that automatically collects, analyzes, and visualizes log data from AWS resources to help security teams investigate and quickly identify the root cause of potential security issues or suspicious activities.

### 💡 Foundational Concepts

**What Problem Does It Solve?**

When a security incident occurs (like GuardDuty detecting a compromised EC2 instance), security teams face challenges:
- **Data overload:** Millions of log entries from CloudTrail, VPC Flow Logs, and GuardDuty findings
- **Time-consuming investigation:** Manually correlating data across multiple sources takes hours or days
- **Complex relationships:** Understanding how resources, users, and IP addresses are connected
- **Root cause analysis:** Determining what actually happened and how the attack progressed
- **Limited context:** Individual logs don't show the full picture of an incident

Traditional security investigation requires:
- Manually querying multiple log sources
- Building custom dashboards and queries
- Expertise in log analysis and correlation
- Significant time investment per incident

**Core Value Proposition:**

AWS Detective automatically collects and processes log data from your AWS environment, organizes it into a graph database, and provides interactive visualizations that show relationships between resources, users, and activities. When GuardDuty alerts you to a threat, Detective helps you quickly understand what happened, who was involved, and what resources were affected—reducing investigation time from hours to minutes.

**Simple Analogy:** Think of Detective as a crime scene investigator with a sophisticated evidence board. When an alarm goes off (GuardDuty finding), Detective automatically gathers all the evidence (logs), connects the dots (relationships), creates a visual timeline, and shows you exactly what happened—like a detective's evidence board with strings connecting suspects, locations, and events.

### 🌐 Key Benefits & Value Proposition

**1. Automated Data Collection and Analysis (Operational Excellence)**
- Automatically ingests data from CloudTrail, VPC Flow Logs, and GuardDuty
- Processes billions of events to build behavior baselines
- No manual log collection or correlation required
- **Cloud Advantage:** *Automation* - Eliminates manual log analysis and correlation

**2. Visual Investigation Tools**
- Interactive graphs showing relationships between resources, users, and IP addresses
- Timeline views of activities leading up to and following security events
- Pre-built visualizations for common investigation scenarios
- **Cloud Advantage:** *Simplified operations* - Complex data presented in easy-to-understand visuals

**3. Faster Incident Response**
- Reduces investigation time from hours to minutes
- Quickly identifies root cause of security issues
- Provides context around GuardDuty findings
- **Cloud Advantage:** *Agility* - Rapid response to security incidents

**4. Machine Learning-Based Insights**
- Establishes baseline behavior for users, roles, and resources
- Identifies deviations from normal patterns
- Highlights unusual activities automatically
- **Cloud Advantage:** *Intelligent insights* - AI-powered anomaly detection

**5. Cost-Effective Investigation**
- Pay only for data ingested and analyzed
- No need to build custom SIEM or log analysis infrastructure
- Reduces time security analysts spend on investigations
- **Cloud Advantage:** *Pay-as-you-go* - No upfront investment in investigation tools

### 🔒 Security and Compliance (CLF-C02 Focus)

**AWS Shared Responsibility Model:**

| **AWS Responsibility (Security OF the Cloud)** | **Customer Responsibility (Security IN the Cloud)** |
|---|---|
| ✅ Physical security of Detective infrastructure | ✅ Enable Detective in AWS accounts and regions |
| ✅ Service availability and scalability | ✅ Investigate security findings and incidents |
| ✅ Data processing and graph database management | ✅ Take action based on investigation results |
| ✅ Machine learning model training and updates | ✅ Manage IAM permissions for Detective access |
| ✅ Encryption of data at rest and in transit | ✅ Configure data retention policies |
| ✅ Service patching and maintenance | ✅ Enable Detective across AWS Organizations |
| ✅ Integration with AWS security services | ✅ Respond to and remediate security incidents |

**Key Security Features:**

- **Automatic Data Ingestion:** Collects CloudTrail, VPC Flow Logs, and GuardDuty findings automatically
- **Behavior Baselines:** Establishes normal behavior patterns using machine learning
- **Relationship Mapping:** Visualizes connections between users, roles, IP addresses, and resources
- **Timeline Analysis:** Shows sequence of events before, during, and after security incidents
- **Multi-Account Support:** Investigates across AWS Organizations member accounts
- **IAM Integration:** Fine-grained access control for investigation capabilities
- **Data Retention:** Stores up to 1 year of historical data for investigations

**What Detective Analyzes:**

**1. AWS CloudTrail Logs:**
- API calls and management events
- User and role activities
- Service-to-service interactions
- Authentication events

**2. VPC Flow Logs:**
- Network traffic patterns
- IP address communications
- Port and protocol usage
- Data transfer volumes

**3. GuardDuty Findings:**
- Security threats and anomalies
- Compromised resources
- Malicious activities
- Suspicious behavior

**Investigation Capabilities:**

- **User/Role Analysis:** Track activities of specific IAM users or roles
- **IP Address Investigation:** Identify all activities from suspicious IP addresses
- **Resource Investigation:** Analyze behavior of specific EC2 instances or resources
- **Finding Investigation:** Deep dive into GuardDuty findings with full context
- **Timeline Reconstruction:** Visualize sequence of events during incidents

**Compliance Support:**
- Provides evidence for security incident investigations
- Helps meet audit requirements for incident response
- Supports SOC 2, ISO 27001 compliance
- Demonstrates security monitoring capabilities
- Maintains historical data for forensic analysis

### 💰 Billing, Pricing, and Support

**Pricing Model: Pay-As-You-Go (Per GB of Data Ingested)**

**Data Ingestion Pricing:**

**1. CloudTrail and GuardDuty Data:**
- **$2.00 per GB** of data ingested per month
- Includes CloudTrail management events and GuardDuty findings

**2. VPC Flow Logs Data:**
- **$0.50 per GB** of data ingested per month
- Network traffic analysis data

**Pricing Examples:**

**Example 1: Small Business**
- 50 GB CloudTrail/GuardDuty data per month
- 200 GB VPC Flow Logs per month
- **Cost:** (50 × $2.00) + (200 × $0.50) = $100 + $100 = **$200/month**

**Example 2: Medium Business**
- 200 GB CloudTrail/GuardDuty data per month
- 1,000 GB VPC Flow Logs per month
- **Cost:** (200 × $2.00) + (1,000 × $0.50) = $400 + $500 = **$900/month**

**Example 3: Enterprise**
- 1,000 GB CloudTrail/GuardDuty data per month
- 5,000 GB VPC Flow Logs per month
- **Cost:** (1,000 × $2.00) + (5,000 × $0.50) = $2,000 + $2,500 = **$4,500/month**

**Important Pricing Notes:**

✅ **No upfront costs:** Pay only for data ingested  
✅ **Data retention included:** Up to 1 year of historical data at no extra charge  
✅ **No per-query charges:** Unlimited investigations and queries  
✅ **Multi-account pricing:** Data from all member accounts aggregated for pricing

**Free Trial:**
- **30-day free trial** for new accounts
- Includes full Detective functionality
- Evaluate investigation capabilities before committing

**Cost Optimization Tips:**
- Enable Detective only in regions where you have active resources
- Monitor data ingestion volumes with CloudWatch
- Leverage the 30-day free trial to assess value
- Consider data retention needs (Detective stores 1 year automatically)
- Disable Detective in unused regions

**Support:**
- Available under all AWS Support Plans
- 24/7 support for Business and Enterprise plans
- Integration with AWS Security Hub
- Extensive documentation and investigation guides

### 🎯 Common Use Cases (Scenario-Based)

**1. Investigating GuardDuty Findings**
- **Scenario:** GuardDuty alerts that an EC2 instance is communicating with a known malicious IP address. The security team needs to understand what happened, when it started, and what data may have been compromised.
- **Solution:** Use Detective to visualize the EC2 instance's activities, see all API calls made, identify which user launched the instance, and trace the timeline of suspicious network connections.
- **Benefit:** Reduces investigation time from hours to minutes, provides complete context, enables faster remediation.

**2. Analyzing Compromised Credentials**
- **Scenario:** GuardDuty detects that AWS access keys are being used from an unusual location. The security team needs to determine what actions were taken with the compromised credentials.
- **Solution:** Detective shows all API calls made using the compromised credentials, which resources were accessed, and whether any data was exfiltrated.
- **Benefit:** Quickly identifies scope of compromise, determines what data was accessed, guides remediation efforts.

**3. Insider Threat Investigation**
- **Scenario:** A company suspects an employee may be accessing sensitive data inappropriately or attempting to steal intellectual property before leaving the company.
- **Solution:** Use Detective to analyze the user's activities over time, identify unusual access patterns, and see which S3 buckets or databases were accessed.
- **Benefit:** Provides evidence for HR investigations, identifies data at risk, supports legal proceedings if necessary.

**4. Post-Incident Forensics**
- **Scenario:** After a security incident is contained, the security team needs to create a detailed timeline of events for a post-mortem report and to improve security controls.
- **Solution:** Detective provides a complete timeline of the incident, showing how the attacker gained access, what they did, and how they moved laterally through the environment.
- **Benefit:** Comprehensive incident documentation, identifies security gaps, improves future defenses.

**5. Multi-Account Security Investigation**
- **Scenario:** An enterprise with 100 AWS accounts detects suspicious activity that may span multiple accounts. Investigating across all accounts manually would take days.
- **Solution:** Enable Detective across AWS Organizations to investigate activities across all member accounts from a single console.
- **Benefit:** Unified investigation view, faster cross-account analysis, identifies attack patterns across organization.

### 🔗 Related Core Services

**1. Amazon GuardDuty**
- **Relationship:** GuardDuty detects threats; Detective investigates them
- **Integration:** Detective automatically ingests GuardDuty findings and provides investigation context
- **CLF-C02 Context:** GuardDuty alerts on threats; Detective helps understand what happened and why

**2. AWS Security Hub**
- **Relationship:** Security Hub aggregates findings; Detective investigates them
- **Integration:** Detective findings can be viewed in Security Hub for centralized security management
- **CLF-C02 Context:** Security Hub provides unified view; Detective provides investigation capabilities

**3. AWS CloudTrail**
- **Relationship:** CloudTrail logs API calls; Detective analyzes those logs
- **Integration:** Detective automatically ingests CloudTrail data for investigation
- **CLF-C02 Context:** CloudTrail records activities; Detective visualizes and analyzes them

**4. Amazon VPC (Virtual Private Cloud)**
- **Relationship:** VPC Flow Logs provide network traffic data; Detective analyzes it
- **Integration:** Detective automatically ingests VPC Flow Logs for network investigation
- **CLF-C02 Context:** VPC provides network isolation; Detective analyzes network traffic patterns

**5. AWS Identity and Access Management (IAM)**
- **Relationship:** IAM controls who can use Detective and investigate findings
- **Integration:** IAM policies define permissions for Detective operations; Detective analyzes IAM user/role activities
- **CLF-C02 Context:** IAM provides access control; Detective investigates user and role behavior

**6. AWS Organizations**
- **Relationship:** Enables centralized Detective management across multiple AWS accounts
- **Integration:** Designate a Detective administrator account to investigate across all member accounts
- **CLF-C02 Context:** Organizations provides multi-account structure; Detective provides cross-account investigations

**7. Amazon EventBridge**
- **Relationship:** EventBridge can trigger automated actions based on Detective findings
- **Integration:** Use EventBridge to automate responses when Detective identifies specific patterns
- **CLF-C02 Context:** EventBridge enables automation; Detective provides investigation insights

### 📊 AWS Security Services Workflow

**Understanding How Detective Fits in the Security Ecosystem:**

```
1. DETECTION (GuardDuty)
   ↓ Detects threat: "EC2 instance communicating with malicious IP"
   
2. INVESTIGATION (Detective)
   ↓ Analyzes: What happened? Who was involved? What was accessed?
   
3. RESPONSE (Manual or Automated)
   ↓ Remediate: Isolate instance, revoke credentials, patch vulnerability
   
4. AGGREGATION (Security Hub)
   ↓ Centralize: View all findings and investigation results in one place
```

**Service Comparison for CLF-C02:**

| Service | Purpose | When to Use |
|---------|---------|-------------|
| **GuardDuty** | Threat detection | Detect malicious activity and threats |
| **Detective** | Investigation | Understand what happened after threat detected |
| **Inspector** | Vulnerability scanning | Find software vulnerabilities before exploitation |
| **Macie** | Data discovery | Identify sensitive data in S3 |
| **Security Hub** | Centralized management | Aggregate findings from all security services |

**Exam Tip:** Choose Detective when the scenario mentions **"investigating security incidents,"** **"root cause analysis,"** **"understanding what happened,"** or **"analyzing GuardDuty findings."**

### ✅ Key Exam Points

**Remember for CLF-C02:**

✅ **Primary Purpose:** Investigate and analyze security incidents detected by GuardDuty  
✅ **Automated Data Collection:** Ingests CloudTrail, VPC Flow Logs, and GuardDuty findings automatically  
✅ **Visual Investigation:** Provides interactive graphs and timelines for incident analysis  
✅ **Reduces Investigation Time:** From hours to minutes with automated correlation  
✅ **Pricing:** $2.00/GB for CloudTrail/GuardDuty data, $0.50/GB for VPC Flow Logs  
✅ **30-Day Free Trial:** Full functionality for evaluation  
✅ **Data Retention:** Stores up to 1 year of historical data  
✅ **Multi-Account:** Investigates across AWS Organizations  
✅ **Integration:** Works with GuardDuty, Security Hub, CloudTrail  
✅ **Use Case Keywords:** "investigate," "root cause," "analyze findings," "incident response"

### 🎓 Practice Scenarios

**Scenario 1:** GuardDuty detects a compromised EC2 instance, and the security team needs to quickly understand what the instance did and what data it accessed.  
**Answer:** AWS Detective (investigates GuardDuty findings with visual analysis)

**Scenario 2:** A company wants to continuously monitor AWS accounts for malicious activity and threats.  
**Answer:** Amazon GuardDuty (threat detection, not Detective which investigates after detection)

**Scenario 3:** After a security incident, the security team needs to create a detailed timeline showing how the attacker gained access and what they did.  
**Answer:** AWS Detective (provides timeline analysis and root cause investigation)

**Scenario 4:** An organization needs to scan EC2 instances for software vulnerabilities and missing patches.  
**Answer:** AWS Inspector (vulnerability scanning, not Detective which investigates incidents)

**Scenario 5:** A business wants to understand the full scope of activities performed by compromised AWS credentials.  
**Answer:** AWS Detective (analyzes all API calls and activities associated with credentials)

**Scenario 6:** A company needs centralized visibility into security findings from GuardDuty, Inspector, and Macie.  
**Answer:** AWS Security Hub (aggregates findings, not Detective which investigates them)

**Scenario 7:** A security analyst needs to investigate whether a specific IP address has accessed any resources in the AWS environment over the past 6 months.  
**Answer:** AWS Detective (provides historical analysis and IP address investigation)

---

## Official AWS Documentation

- [AWS Detective Official Documentation](https://docs.aws.amazon.com/detective/)
- [AWS Detective FAQs](https://aws.amazon.com/detective/faqs/)
- [AWS Detective Pricing](https://aws.amazon.com/detective/pricing/)
- [AWS Detective User Guide](https://docs.aws.amazon.com/detective/latest/userguide/what-is-detective.html)
- [AWS Detective Investigation Guide](https://docs.aws.amazon.com/detective/latest/userguide/detective-investigation.html)
- [AWS Detective Best Practices](https://docs.aws.amazon.com/detective/latest/userguide/detective-best-practices.html)
- [Investigating GuardDuty Findings with Detective](https://docs.aws.amazon.com/detective/latest/userguide/guardduty-finding-investigation.html)
