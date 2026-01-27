# AWS Artifact CLF-C02 Practice Questions

## Section 1: CLF-C02 Practice Questions (10 questions)

**Question 1:**
AnyCompany Healthcare is building a new patient management system on AWS and needs to ensure HIPAA compliance. Their compliance officer requires a signed Business Associate Addendum (BAA) with AWS before storing any protected health information (PHI). Which AWS service provides the ability to review and accept this agreement?

A) AWS Organizations
B) AWS Artifact
C) AWS Certificate Manager
D) AWS Compliance Center

**Question 2:**
A financial services company is undergoing a SOC 2 Type II audit. Their external auditors have requested documentation proving that AWS meets specific security and compliance standards. Where can the company obtain official AWS SOC 2 reports to provide to their auditors?

A) AWS Support Center by opening a support ticket
B) AWS Trusted Advisor compliance dashboard
C) AWS Artifact self-service portal
D) AWS Security Hub compliance reports

**Question 3:**
Which statement BEST describes the primary purpose of AWS Artifact?

A) A service that automatically ensures all AWS resources comply with industry regulations
B) A self-service portal providing on-demand access to AWS compliance reports and agreements
C) A monitoring tool that generates compliance reports based on customer resource configurations
D) A backup service that stores compliance documentation across multiple AWS Regions

**Question 4:**
AnyCompany is expanding their e-commerce platform to process credit card payments directly. They need to demonstrate PCI DSS compliance to their payment processor. What is the MOST efficient way to obtain AWS's PCI DSS compliance documentation?

A) Contact AWS sales team and request the documentation via email
B) Wait for AWS to mail physical copies of PCI DSS attestation documents
C) Download the PCI DSS Attestation of Compliance from AWS Artifact
D) Hire a third-party auditor to assess AWS's PCI DSS compliance

**Question 5:**
Under the AWS Shared Responsibility Model for AWS Artifact, which of the following are customer responsibilities? (Select TWO)

A) Maintaining AWS's compliance certifications and conducting audits
B) Downloading appropriate compliance reports relevant to their use case
C) Creating and updating AWS SOC and ISO compliance reports
D) Executing necessary agreements like the Business Associate Addendum
E) Ensuring AWS Artifact portal infrastructure is secure and available

**Question 6:**
A startup company with a limited budget needs to access AWS compliance documentation for their first security audit. They are concerned about additional costs. What is the pricing model for AWS Artifact?

A) Free for the first 12 months, then $99 per month
B) $0.10 per compliance report downloaded
C) Completely free with no charges for accessing documentation
D) Included only with Business or Enterprise AWS Support plans

**Question 7:**
AnyCompany operates in multiple AWS accounts under AWS Organizations and needs to execute a HIPAA Business Associate Addendum that applies to all accounts. How can they efficiently manage this requirement using AWS Artifact?

A) Download the BAA from AWS Artifact and manually sign it for each account separately
B) Accept the agreement once in the management account, and it applies to all organization accounts
C) Contact AWS Support to execute the BAA on behalf of all accounts
D) Use AWS Config to automatically distribute the BAA across all accounts

**Question 8:**
A compliance manager wants to track who in their organization has accessed AWS compliance reports and when they downloaded specific documents. Which AWS service integration with AWS Artifact provides this audit capability?

A) Amazon CloudWatch Metrics
B) AWS CloudTrail
C) AWS Config
D) Amazon Inspector

**Question 9:**
Which of the following compliance frameworks and certifications can customers access documentation for through AWS Artifact? (Select TWO)

A) ISO 27001 certification reports
B) Customer-specific compliance assessments
C) PCI DSS Attestation of Compliance
D) Third-party vendor security audits
E) Customer application vulnerability scans

**Question 10:**
AnyCompany's security team wants to ensure that only authorized personnel in their organization can access and download sensitive compliance reports from AWS Artifact. Which AWS service should they use to control access to AWS Artifact?

A) AWS WAF (Web Application Firewall)
B) AWS Shield
C) AWS IAM (Identity and Access Management)
D) Amazon GuardDuty

---

## Section 2: Answers and Justifications

**Question 1: Correct Answer - B) AWS Artifact**

**Justification:**
- **Why B is correct:** AWS Artifact is the designated self-service portal where customers can review, accept, and manage legal agreements with AWS, including the Business Associate Addendum (BAA) required for HIPAA compliance. This is a fundamental CLF-C02 concept about AWS Artifact's role in compliance. Healthcare organizations must execute the BAA through AWS Artifact before storing PHI in AWS services.

- **Why A is wrong:** AWS Organizations is for managing multiple AWS accounts centrally, not for accessing compliance agreements. While Organizations can help manage agreements across accounts, it's not where you initially access and execute the BAA.

- **Why C is wrong:** AWS Certificate Manager is for provisioning and managing SSL/TLS certificates for secure communications, not for compliance agreements or documentation.

- **Why D is wrong:** There is no service called "AWS Compliance Center." This is a distractor that sounds plausible but doesn't exist as an AWS service.

**Question 2: Correct Answer - C) AWS Artifact self-service portal**

**Justification:**
- **Why C is correct:** AWS Artifact provides immediate, self-service access to AWS compliance reports including SOC 1, SOC 2, and SOC 3 reports. This eliminates the need to wait for AWS support responses and allows customers to download official audit reports instantly to provide to their own auditors. This is a core use case for AWS Artifact that's frequently tested in CLF-C02.

- **Why A is wrong:** While AWS Support can help with questions about compliance, AWS Artifact is specifically designed for self-service access to compliance reports without needing to open support tickets. Using support tickets would be slower and unnecessary.

- **Why B is wrong:** AWS Trusted Advisor provides recommendations for cost optimization, performance, security, and fault tolerance, but it doesn't provide access to official AWS compliance reports like SOC 2.

- **Why D is wrong:** AWS Security Hub aggregates security findings from AWS services and partner products, but it doesn't provide access to official third-party audit reports like SOC 2 that AWS Artifact offers.

**Question 3: Correct Answer - B) A self-service portal providing on-demand access to AWS compliance reports and agreements**

**Justification:**
- **Why B is correct:** This accurately describes AWS Artifact's primary purpose as defined in AWS documentation. AWS Artifact is fundamentally a self-service portal that provides immediate access to compliance documentation (reports from third-party auditors) and legal agreements (like BAA and NDA). This aligns with CLF-C02's focus on understanding core service purposes.

- **Why A is wrong:** AWS Artifact doesn't automatically ensure compliance or configure resources. It provides documentation about AWS's compliance, but customers are responsible for configuring their own resources to meet compliance requirements.

- **Why C is wrong:** This describes services like AWS Config or AWS Security Hub that monitor customer resources. AWS Artifact provides AWS's compliance reports, not reports generated from customer configurations.

- **Why D is wrong:** AWS Artifact is not a backup service. It's a documentation portal. While compliance documents are stored durably, that's not its primary purpose.

**Question 4: Correct Answer - C) Download the PCI DSS Attestation of Compliance from AWS Artifact**

**Justification:**
- **Why C is correct:** AWS Artifact provides immediate, self-service access to AWS's PCI DSS Attestation of Compliance (AOC) and related documentation. This is the most efficient method as it's available 24/7, requires no waiting, and provides official documentation that payment processors and auditors will accept. This demonstrates understanding of AWS Artifact's practical business value.

- **Why A is wrong:** Contacting the sales team would be slower and unnecessary since AWS Artifact provides self-service access. This approach would delay the compliance process and involve unnecessary steps.

- **Why B is wrong:** AWS doesn't mail physical compliance documents. AWS Artifact provides digital access to all compliance documentation, which is faster and more efficient than physical mail.

- **Why D is wrong:** Hiring a third-party auditor to assess AWS would be extremely expensive and redundant since AWS already undergoes regular PCI DSS audits. AWS Artifact provides the results of these official audits.

**Question 5: Correct Answer - B) Downloading appropriate compliance reports relevant to their use case, D) Executing necessary agreements like the Business Associate Addendum**

**Justification:**
- **Why B and D are correct:** Under the shared responsibility model, customers are responsible for accessing and using AWS Artifact appropriately. This includes downloading the compliance reports they need for their specific regulatory requirements and executing legal agreements like the BAA for HIPAA compliance. These are "security IN the cloud" responsibilities.

- **Why A is wrong:** AWS is responsible for maintaining its own compliance certifications and undergoing audits. This is "security OF the cloud" and falls entirely under AWS's responsibility, not the customer's.

- **Why C is wrong:** AWS creates and updates all compliance reports through third-party audits. Customers don't create AWS's compliance documentation; they only access and use it.

- **Why E is wrong:** AWS is responsible for the infrastructure security and availability of the AWS Artifact portal itself. This is part of AWS's responsibility to maintain the service infrastructure.

**Question 6: Correct Answer - C) Completely free with no charges for accessing documentation**

**Justification:**
- **Why C is correct:** AWS Artifact is completely free to use with no charges for accessing compliance reports or executing agreements. This is a critical CLF-C02 exam point about AWS Artifact pricing. All AWS customers can access AWS Artifact at no cost, regardless of their usage or support plan level.

- **Why A is wrong:** AWS Artifact doesn't have a free trial period followed by charges. It's permanently free for all AWS customers with no time limitations or subscription fees.

- **Why B is wrong:** There are no per-report download charges for AWS Artifact. Customers can download compliance reports as many times as needed at no cost.

- **Why D is wrong:** AWS Artifact is available to all AWS customers regardless of their support plan level. You don't need Business or Enterprise support to access compliance documentation.

**Question 7: Correct Answer - B) Accept the agreement once in the management account, and it applies to all organization accounts**

**Justification:**
- **Why B is correct:** AWS Organizations integration with AWS Artifact allows customers to accept agreements like the BAA once in the management (master) account, and the agreement automatically applies to all member accounts in the organization. This simplifies compliance management for organizations with multiple AWS accounts and is an important integration pattern for CLF-C02.

- **Why A is wrong:** This approach would be inefficient and unnecessary. AWS Artifact's integration with AWS Organizations specifically eliminates the need to sign agreements separately for each account.

- **Why C is wrong:** AWS Support doesn't execute agreements on behalf of customers. Customers must accept agreements themselves through AWS Artifact, though the Organizations integration simplifies this for multiple accounts.

- **Why D is wrong:** AWS Config is for tracking resource configurations and compliance rules, not for distributing legal agreements. This is not the correct service for managing AWS Artifact agreements.

**Question 8: Correct Answer - B) AWS CloudTrail**

**Justification:**
- **Why B is correct:** AWS CloudTrail logs all API calls and user activities in AWS, including access to AWS Artifact. CloudTrail records who accessed AWS Artifact, which compliance reports were downloaded, when agreements were accepted, and other audit-relevant activities. This integration provides the audit trail needed for compliance and security monitoring.

- **Why A is wrong:** CloudWatch Metrics tracks numerical performance data like CPU utilization or request counts, not detailed audit logs of user activities and document access in AWS Artifact.

- **Why C is wrong:** AWS Config tracks resource configuration changes and compliance with configuration rules, but it doesn't provide detailed audit logs of who accessed specific compliance reports in AWS Artifact.

- **Why D is wrong:** Amazon Inspector is for security vulnerability assessments of EC2 instances and container images, not for auditing access to compliance documentation.

**Question 9: Correct Answer - A) ISO 27001 certification reports, C) PCI DSS Attestation of Compliance**

**Justification:**
- **Why A and C are correct:** AWS Artifact provides access to AWS's compliance reports from third-party auditors, including ISO certifications (ISO 27001, ISO 27017, ISO 27018, ISO 9001) and PCI DSS Attestation of Compliance. These are official AWS compliance documents that customers can download and provide to their own auditors.

- **Why B is wrong:** AWS Artifact provides AWS's compliance documentation, not customer-specific assessments. Customers are responsible for their own compliance assessments based on how they use AWS services.

- **Why D is wrong:** AWS Artifact contains AWS's compliance reports, not third-party vendor security audits. Customers would need to obtain security audits from their other vendors separately.

- **Why E is wrong:** AWS Artifact doesn't provide vulnerability scans of customer applications. Services like Amazon Inspector perform vulnerability assessments, but those results aren't stored in AWS Artifact.

**Question 10: Correct Answer - C) AWS IAM (Identity and Access Management)**

**Justification:**
- **Why C is correct:** AWS IAM is used to control access to all AWS services, including AWS Artifact. Organizations can create IAM policies that specify which users or roles can access AWS Artifact, download compliance reports, or execute agreements. This allows fine-grained access control to ensure only authorized compliance and security personnel can access sensitive documentation.

- **Why A is wrong:** AWS WAF is a web application firewall that protects web applications from common exploits, not an access control service for AWS resources like AWS Artifact.

- **Why B is wrong:** AWS Shield provides DDoS protection for applications, not access control for AWS services. It doesn't control who can access AWS Artifact.

- **Why D is wrong:** Amazon GuardDuty is a threat detection service that monitors for malicious activity, not an access control mechanism. While it might detect suspicious access patterns, it doesn't control who can access AWS Artifact.