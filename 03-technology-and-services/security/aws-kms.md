# AWS Key Management Service (KMS)

## Service Overview

AWS Key Management Service (KMS) is a fully managed service that enables you to create, manage, and control cryptographic keys used to encrypt and decrypt data across AWS services and applications.

### 💡 Foundational Concepts

**What Problem Does It Solve?**

Encryption is essential for protecting sensitive data, but managing encryption keys is complex and risky:
- **Key storage:** Where do you securely store encryption keys?
- **Key rotation:** How do you regularly change keys without breaking applications?
- **Access control:** Who should be allowed to use which keys?
- **Compliance:** How do you prove keys are managed securely for audits?
- **Key lifecycle:** How do you create, disable, and delete keys safely?

If encryption keys are compromised, all encrypted data becomes vulnerable. Traditional key management requires specialized hardware (HSMs), dedicated staff, and complex processes.

**Core Value Proposition:**

AWS KMS eliminates the complexity of key management by providing a centralized, secure service for creating and controlling encryption keys. You can encrypt data across AWS services (S3, EBS, RDS) with a few clicks, and KMS handles all the underlying key management, rotation, and security. Keys never leave KMS unencrypted, and all key usage is logged for compliance.

**Simple Analogy:** Think of KMS as a secure bank vault for your encryption keys. Instead of keeping keys under your mattress (in your code or on servers), you store them in a professionally managed vault. When you need to encrypt or decrypt data, you ask the vault to do it for you—the keys never leave the vault, and every access is recorded.

### 🌐 Key Benefits & Value Proposition

**1. Centralized Key Management (Operational Excellence)**
- Single service to create, manage, and control all encryption keys
- Unified view of key usage across all AWS services
- Simplified key lifecycle management (create, rotate, disable, delete)
- **Cloud Advantage:** *Centralized management* - No need to manage separate key systems per service

**2. Integrated with AWS Services (Security at Scale)**
- Seamless encryption for S3, EBS, RDS, DynamoDB, Lambda, and 100+ AWS services
- Enable encryption with a single click in most AWS services
- Automatic encryption/decryption handled by AWS services
- **Cloud Advantage:** *Built-in security* - Encryption integrated into AWS infrastructure

**3. Automatic Key Rotation**
- Automatic annual rotation for AWS-managed keys
- Optional automatic rotation for customer-managed keys
- Maintains old key versions for decrypting existing data
- **Cloud Advantage:** *Automation* - Eliminates manual, error-prone key rotation

**4. Compliance and Audit Support**
- FIPS 140-2 validated cryptographic modules
- CloudTrail integration logs all key usage
- Supports compliance with HIPAA, PCI-DSS, GDPR, FedRAMP
- **Cloud Advantage:** *Built-in compliance* - Meets regulatory requirements out-of-the-box

**5. Fine-Grained Access Control**
- IAM policies control who can manage keys
- Key policies control who can use keys for encryption/decryption
- Grant temporary access without sharing keys
- **Cloud Advantage:** *Granular security* - Separate key management from key usage permissions

**6. Cost-Effective Encryption**
- Pay only for keys you create and API requests
- No upfront costs or hardware investments
- Eliminates need for on-premises HSM hardware
- **Cloud Advantage:** *Pay-as-you-go* - No capital expenditure on encryption infrastructure

### 🔒 Security and Compliance (CLF-C02 Focus)

**AWS Shared Responsibility Model:**

| **AWS Responsibility (Security OF the Cloud)** | **Customer Responsibility (Security IN the Cloud)** |
|---|---|
| ✅ Physical security of KMS infrastructure | ✅ Create and manage KMS keys |
| ✅ FIPS 140-2 validated cryptographic modules | ✅ Define key policies and IAM permissions |
| ✅ Hardware security modules (HSMs) | ✅ Enable key rotation |
| ✅ Service availability and durability | ✅ Decide which data to encrypt |
| ✅ Key material protection (never leaves KMS unencrypted) | ✅ Monitor key usage via CloudTrail |
| ✅ Automatic key replication across AZs | ✅ Disable or delete keys when no longer needed |
| ✅ Service patching and maintenance | ✅ Configure grants for temporary access |
| ✅ Encryption of keys at rest | ✅ Use appropriate key types for use cases |

**Key Security Features:**

- **Keys Never Leave KMS Unencrypted:** All encryption/decryption operations happen within KMS
- **Hardware Security Modules (HSMs):** Keys protected by FIPS 140-2 validated HSMs
- **Automatic Key Replication:** Keys automatically replicated across multiple AZs for durability
- **Key Policies:** Resource-based policies control key access
- **IAM Integration:** Fine-grained access control using IAM policies
- **CloudTrail Logging:** All key usage logged for audit and compliance
- **Key Deletion Protection:** Mandatory waiting period (7-30 days) before key deletion

**Types of KMS Keys:**

**1. AWS Managed Keys (Free)**
- Created and managed automatically by AWS services
- Named format: `aws/service-name` (e.g., `aws/s3`, `aws/rds`)
- Automatic rotation every year
- Cannot be deleted or modified
- **Use Case:** Default encryption for AWS services

**2. Customer Managed Keys (CMKs)**
- Created and fully controlled by you
- You define key policies and IAM permissions
- Optional automatic rotation (every year)
- Can be disabled or scheduled for deletion
- **Use Case:** When you need full control over key policies and rotation

**3. AWS Owned Keys**
- Owned and managed by AWS (not in your account)
- Used by AWS services for internal operations
- No visibility or control
- No charges
- **Use Case:** Background AWS service operations

**Compliance Certifications:**
- **FIPS 140-2** Level 2 (Level 3 for CloudHSM)
- **PCI-DSS** - Payment card data encryption
- **HIPAA** - Healthcare data protection
- **GDPR** - EU data privacy
- **FedRAMP** - US government compliance
- **SOC 1, 2, 3** - Service organization controls
- **ISO 27001** - Information security

### 💰 Billing, Pricing, and Support

**Pricing Model: Pay-As-You-Go**

**1. KMS Key Storage:**
- **Customer Managed Keys:** $1.00 per key per month
- **AWS Managed Keys:** Free (no charge)
- **AWS Owned Keys:** Free (no charge)
- Prorated for partial months

**2. API Request Charges:**
- **Free Tier:** 20,000 requests per month (for AWS managed keys)
- **After Free Tier:**
  - Symmetric key requests: $0.03 per 10,000 requests
  - Asymmetric key requests: $0.15 per 10,000 requests (RSA)
  - ECC requests: $0.10 per 10,000 requests

**3. Optional: Custom Key Store (CloudHSM)**
- Additional charges for CloudHSM cluster
- $1.60 per hour per HSM
- For customers requiring dedicated HSMs

**Pricing Examples:**

**Example 1: Small Business**
- 5 customer managed keys
- 50,000 API requests per month
- **Cost:** (5 × $1.00) + ((50,000 - 20,000) / 10,000 × $0.03) = $5.00 + $0.09 = **$5.09/month**

**Example 2: Enterprise**
- 100 customer managed keys
- 1,000,000 API requests per month
- **Cost:** (100 × $1.00) + ((1,000,000 - 20,000) / 10,000 × $0.03) = $100 + $2.94 = **$102.94/month**

**Example 3: Using AWS Managed Keys Only**
- 0 customer managed keys (using aws/s3, aws/rds, etc.)
- 100,000 API requests per month
- **Cost:** $0 (keys are free) + ((100,000 - 20,000) / 10,000 × $0.03) = **$0.24/month**

**Cost Optimization Tips:**
- Use AWS managed keys when you don't need custom key policies (free)
- Cache data keys in applications to reduce API calls
- Use envelope encryption to minimize KMS API requests
- Delete unused customer managed keys
- Monitor usage with CloudWatch and Cost Explorer

**Free Tier:**
- AWS managed keys are always free
- 20,000 API requests per month free (applies to AWS managed keys)

**Support:**
- Available under all AWS Support Plans
- 24/7 support for Business and Enterprise plans
- Extensive documentation and best practices guides

### 🎯 Common Use Cases (Scenario-Based)

**1. Encrypting Data at Rest in S3**
- **Scenario:** A company stores customer documents in S3 and must encrypt all data to meet compliance requirements.
- **Solution:** Enable S3 default encryption using KMS keys. All objects automatically encrypted when uploaded.
- **Benefit:** Compliance with data protection regulations, centralized key management, audit trail via CloudTrail.
- **Key Type:** AWS managed key (`aws/s3`) for simplicity, or customer managed key for custom policies.

**2. Database Encryption (RDS/DynamoDB)**
- **Scenario:** A healthcare application stores patient records in RDS and must comply with HIPAA encryption requirements.
- **Solution:** Enable RDS encryption using KMS when creating the database. All data, backups, and snapshots automatically encrypted.
- **Benefit:** HIPAA compliance, automatic encryption/decryption, no application code changes required.
- **Key Type:** Customer managed key for full control and audit capabilities.

**3. EBS Volume Encryption**
- **Scenario:** A financial services company runs applications on EC2 with sensitive data on EBS volumes and needs encryption.
- **Solution:** Enable EBS encryption by default in the AWS account. All new EBS volumes automatically encrypted with KMS.
- **Benefit:** Protects data at rest, encrypts snapshots, meets PCI-DSS requirements.
- **Key Type:** AWS managed key (`aws/ebs`) or customer managed key.

**4. Application-Level Encryption**
- **Scenario:** A SaaS application needs to encrypt sensitive customer data before storing it in a database, with each customer having separate encryption keys.
- **Solution:** Use KMS API to generate data encryption keys (DEKs) for each customer. Encrypt data in application code using DEKs.
- **Benefit:** Customer-specific encryption, centralized key management, separation of duties.
- **Key Type:** Customer managed keys with grants for application access.

**5. Secrets and Configuration Encryption**
- **Scenario:** A development team stores database passwords and API keys in AWS Secrets Manager and Systems Manager Parameter Store.
- **Solution:** Both services automatically use KMS to encrypt stored secrets and parameters.
- **Benefit:** Secure storage of credentials, automatic encryption, integration with IAM for access control.
- **Key Type:** AWS managed keys or customer managed keys for additional control.

**6. Cross-Region Data Replication**
- **Scenario:** A global application replicates S3 data across multiple regions and needs consistent encryption.
- **Solution:** Use multi-region KMS keys to encrypt data in multiple regions with the same key ID.
- **Benefit:** Simplified key management for global applications, consistent encryption policies.
- **Key Type:** Multi-region customer managed keys.

### 🔗 Related Core Services

**1. Amazon S3 (Simple Storage Service)**
- **Relationship:** S3 uses KMS to encrypt objects at rest
- **Integration:** S3 server-side encryption with KMS (SSE-KMS) encrypts objects automatically
- **CLF-C02 Context:** S3 stores data; KMS provides encryption keys for protecting that data

**2. Amazon EBS (Elastic Block Store)**
- **Relationship:** EBS uses KMS to encrypt volumes and snapshots
- **Integration:** Enable EBS encryption to automatically encrypt all volumes with KMS keys
- **CLF-C02 Context:** EBS provides block storage; KMS encrypts data on those volumes

**3. Amazon RDS (Relational Database Service)**
- **Relationship:** RDS uses KMS to encrypt databases, backups, and snapshots
- **Integration:** Enable encryption when creating RDS instances; KMS handles all encryption operations
- **CLF-C02 Context:** RDS stores database data; KMS protects that data with encryption

**4. AWS Secrets Manager**
- **Relationship:** Secrets Manager uses KMS to encrypt stored secrets
- **Integration:** All secrets automatically encrypted with KMS keys
- **CLF-C02 Context:** Secrets Manager stores credentials; KMS encrypts those credentials

**5. AWS Systems Manager Parameter Store**
- **Relationship:** Parameter Store uses KMS to encrypt secure string parameters
- **Integration:** SecureString parameters automatically encrypted with KMS
- **CLF-C02 Context:** Parameter Store stores configuration; KMS encrypts sensitive parameters

**6. AWS Identity and Access Management (IAM)**
- **Relationship:** IAM controls who can manage and use KMS keys
- **Integration:** IAM policies define permissions for KMS operations; key policies control key usage
- **CLF-C02 Context:** IAM provides access control; KMS provides encryption capabilities

**7. AWS CloudTrail**
- **Relationship:** CloudTrail logs all KMS API calls for audit and compliance
- **Integration:** Automatic logging of key creation, usage, deletion, and policy changes
- **CLF-C02 Context:** CloudTrail provides audit trail; KMS provides encryption operations to audit

**8. AWS Lambda**
- **Relationship:** Lambda uses KMS to encrypt environment variables and function code
- **Integration:** Lambda automatically encrypts environment variables using KMS
- **CLF-C02 Context:** Lambda runs code; KMS protects sensitive configuration data

### 📊 KMS Key Types Comparison

**Quick Reference for CLF-C02:**

| Feature | AWS Managed Keys | Customer Managed Keys | AWS Owned Keys |
|---------|------------------|----------------------|----------------|
| **Cost** | Free | $1/key/month | Free |
| **Who Creates** | AWS service | You | AWS |
| **Visibility** | ✅ Visible in your account | ✅ Visible in your account | ❌ Not visible |
| **Key Policy Control** | ❌ No | ✅ Yes | ❌ No |
| **Automatic Rotation** | ✅ Every year | ✅ Optional (every year) | ✅ Varies |
| **Can Delete** | ❌ No | ✅ Yes (7-30 day wait) | ❌ No |
| **CloudTrail Logging** | ✅ Yes | ✅ Yes | ❌ No |
| **Use Case** | Default service encryption | Custom policies, compliance | AWS internal operations |
| **Example** | `aws/s3`, `aws/rds` | `my-app-key` | DynamoDB table keys |

### 📋 Envelope Encryption Concept

**What is Envelope Encryption?** (CLF-C02 Foundational Concept)

Instead of encrypting large amounts of data directly with KMS (expensive and slow), envelope encryption uses a two-layer approach:

1. **Data Encryption Key (DEK):** KMS generates a plaintext DEK to encrypt your data locally
2. **Encrypted DEK:** KMS encrypts the DEK using your KMS key and returns both versions
3. **Storage:** Store encrypted data + encrypted DEK together
4. **Decryption:** Send encrypted DEK to KMS to decrypt it, then use plaintext DEK to decrypt data

**Benefits:**
- Reduces KMS API calls (cost savings)
- Faster encryption/decryption (local operations)
- Better performance for large datasets

**Exam Tip:** You don't need to implement envelope encryption manually—AWS services like S3, EBS, and RDS do this automatically.

### ✅ Key Exam Points

**Remember for CLF-C02:**

✅ **Primary Purpose:** Create, manage, and control encryption keys for AWS services and applications  
✅ **Integrated Encryption:** Works with 100+ AWS services (S3, EBS, RDS, DynamoDB, Lambda, etc.)  
✅ **Key Types:** AWS managed (free), Customer managed ($1/month), AWS owned (free, not visible)  
✅ **Automatic Rotation:** AWS managed keys rotate annually; customer managed keys optional  
✅ **Pricing:** $1 per customer managed key/month + $0.03 per 10,000 API requests  
✅ **Security:** Keys never leave KMS unencrypted; FIPS 140-2 validated HSMs  
✅ **Compliance:** Supports HIPAA, PCI-DSS, GDPR, FedRAMP, SOC, ISO 27001  
✅ **Audit:** CloudTrail logs all key usage for compliance  
✅ **Shared Responsibility:** AWS manages infrastructure; customer manages key policies and usage  
✅ **Use Case Keywords:** "encrypt data at rest," "key management," "compliance," "encryption keys"

### 🎓 Practice Scenarios

**Scenario 1:** A company needs to encrypt all S3 objects at rest to meet compliance requirements with minimal management overhead.  
**Answer:** Enable S3 default encryption with AWS managed KMS key (`aws/s3`) - free and automatic

**Scenario 2:** A healthcare organization must encrypt RDS databases and maintain full control over encryption key policies for HIPAA compliance.  
**Answer:** Use customer managed KMS key with custom key policies - $1/month per key

**Scenario 3:** A business wants to automatically rotate encryption keys every year without manual intervention.  
**Answer:** Enable automatic key rotation for customer managed KMS keys (or use AWS managed keys which rotate automatically)

**Scenario 4:** A development team needs to encrypt Lambda function environment variables containing database passwords.  
**Answer:** Lambda automatically encrypts environment variables using KMS (AWS managed key or customer managed key)

**Scenario 5:** A company needs to prove to auditors that encryption keys are managed securely and track all key usage.  
**Answer:** Use KMS with CloudTrail integration - provides complete audit trail of key operations

**Scenario 6:** An application encrypts large files (100 GB+) and needs cost-effective encryption without excessive KMS API calls.  
**Answer:** Use envelope encryption (automatically implemented by AWS services like S3)

---

## Official AWS Documentation

- [AWS KMS Official Documentation](https://docs.aws.amazon.com/kms/)
- [AWS KMS FAQs](https://aws.amazon.com/kms/faqs/)
- [AWS KMS Pricing](https://aws.amazon.com/kms/pricing/)
- [AWS KMS Developer Guide](https://docs.aws.amazon.com/kms/latest/developerguide/)
- [AWS KMS Best Practices](https://docs.aws.amazon.com/kms/latest/developerguide/best-practices.html)
- [AWS KMS Key Policies](https://docs.aws.amazon.com/kms/latest/developerguide/key-policies.html)
- [AWS KMS Cryptographic Details](https://docs.aws.amazon.com/kms/latest/cryptographic-details/)
