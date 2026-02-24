# AWS Config - CLF-C02 Study Notes

## 💡 Simple Analogy
AWS Config is like a **security camera system with instant replay for your AWS account**. It continuously records what your resources look like, tracks every change made, and can alert you when something doesn't match your company's rules (like "all doors must be locked after 6 PM"). You can rewind the tape to see exactly when someone changed a setting and what it looked like before.

## 🔍 Service Overview
- **One-Sentence Pitch:** AWS Config continuously monitors and records your AWS resource configurations and allows you to automate compliance checking against desired configurations.
- **The "Why":** Executives need to prove to auditors that their cloud infrastructure meets regulatory requirements (HIPAA, PCI-DSS, SOC 2). AWS Config provides the audit trail and automated compliance reporting that turns a 3-month manual audit into a one-click report.

## 🚀 Key Benefits (The 6 Advantages Link)

- **Stop Guessing Capacity (for Compliance):** Automatically discover all resources in your account—no more manual spreadsheets tracking what exists. Config knows what you have, even if your team doesn't.

- **Increase Speed/Agility:** Deploy faster with confidence. Config Rules act as guardrails, automatically flagging non-compliant resources within minutes instead of waiting for quarterly security reviews.

- **Variable Expense:** Pay only for the configuration items recorded and rules evaluated. No upfront investment in compliance monitoring infrastructure or third-party audit tools.

## 🛡️ Security & Shared Responsibility

- **AWS is responsible for:**
  - The Config service infrastructure and availability
  - Securing the underlying systems that record configuration data
  - Maintaining the managed Config Rules library

- **The Customer is responsible for:**
  - Enabling AWS Config in their accounts and regions
  - Defining which resources to track
  - Creating and managing Config Rules (compliance policies)
  - Securing the S3 bucket where configuration history is stored
  - Acting on compliance notifications and remediating non-compliant resources

## 💰 Billing & Pricing Models

- **Primary Model:** Pay-per-use based on two dimensions:
  - **Configuration Items Recorded:** Charged per configuration item recorded (each time a resource state is captured)
  - **Config Rules Evaluations:** Charged per rule evaluation (when Config checks if a resource complies with a rule)

- **Cost Drivers:** 
  - Number of resources being tracked (more EC2 instances = more config items)
  - Frequency of changes (rapidly changing environments generate more recordings)
  - Number of active Config Rules
  - S3 storage costs for configuration history retention

## 🏗️ Well-Architected Framework Mapping

- **Primary Pillar:** **Security** & **Operational Excellence**

- **Reasoning:** 
  - **Security:** Config provides continuous compliance monitoring, configuration drift detection, and audit trails—essential for maintaining security posture and meeting regulatory requirements.
  - **Operational Excellence:** Enables automated compliance checking, reduces manual audit effort, and provides visibility into resource relationships and change history for faster troubleshooting.

## 🎯 Exam Scenarios ("Which service should you use if...")

- **Scenario A:** "Your company needs to ensure all S3 buckets have encryption enabled and receive alerts when non-compliant buckets are created." 
  - **Solution:** AWS Config with a managed rule (s3-bucket-server-side-encryption-enabled) that continuously evaluates buckets and triggers SNS notifications for violations.

- **Scenario B:** "An auditor asks for proof that your EC2 instances have always had approved security groups attached over the past 12 months."
  - **Solution:** AWS Config's configuration history provides a timeline showing all security group changes for each instance, with timestamps and who made the change.

- **Scenario C:** "You need to track which IAM user deleted a critical RDS database last week."
  - **Solution:** AWS Config records resource configuration changes and integrates with CloudTrail (which logs the API call and user identity). Config shows the "what changed," CloudTrail shows the "who did it."

- **Scenario D:** "Automatically remediate non-compliant resources, like stopping EC2 instances without required tags."
  - **Solution:** AWS Config Rules with automatic remediation actions using Systems Manager Automation documents.

## ⚠️ Comparison Note (Avoid the Trap)

- **AWS Config vs. AWS CloudTrail:**
  - **Config:** Answers "What does my resource look like NOW?" and "Is it compliant with my rules?" Focuses on resource STATE and COMPLIANCE.
  - **CloudTrail:** Answers "Who made this API call?" and "When did it happen?" Focuses on USER ACTIVITY and API EVENTS.
  - **Exam Tip:** If the question asks about compliance, configuration history, or resource relationships → Config. If it asks about user actions, API logging, or security forensics → CloudTrail. They work together: CloudTrail logs WHO changed something, Config records WHAT was changed.

- **AWS Config vs. AWS Trusted Advisor:**
  - **Config:** Customizable compliance rules YOU define. Continuous monitoring with detailed history. Requires you to enable and configure it.
  - **Trusted Advisor:** Pre-built AWS best practice checks across 5 categories. Provides recommendations but limited historical tracking. Some checks require Business/Enterprise Support.
  - **Exam Tip:** Trusted Advisor = AWS's recommendations for optimization. Config = Your organization's compliance requirements enforcement.

- **AWS Config vs. AWS Systems Manager (Session Manager/Patch Manager):**
  - **Config:** Monitors and records configuration state (read-only observation with compliance checking).
  - **Systems Manager:** Actively manages and modifies resources (patching, running commands, changing configurations).
  - **Exam Tip:** Config watches and reports. Systems Manager acts and changes.

---

## 📝 CLF-C02 Exam Quick Facts

**Remember These for the Exam:**
- Config is **REGIONAL** (must enable per region, but can aggregate across regions)
- Stores configuration history in **S3** (you choose the bucket)
- Uses **Config Rules** to evaluate compliance (AWS Managed or Custom)
- Can trigger **automatic remediation** via Systems Manager
- Integrates with **CloudTrail** for complete audit trail (who + what)
- Supports **multi-account, multi-region** aggregation via AWS Organizations

**Common Exam Keywords:**
- "Compliance monitoring"
- "Configuration drift"
- "Audit trail for resource changes"
- "Continuous assessment"
- "Resource inventory"
- "Relationship between resources"

---

**Official Documentation:** https://docs.aws.amazon.com/config/
