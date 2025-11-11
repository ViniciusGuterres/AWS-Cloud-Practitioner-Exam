# AWS FSx - CLF-C02 Practice Questions

## Section 1: CLF-C02 Practice Questions

### Question 1
A company is migrating their Windows-based file servers to AWS and needs a fully managed file system that supports SMB protocol and Active Directory integration. Their applications require high-performance file storage with sub-millisecond latencies.

Which AWS service would be the MOST appropriate solution?

A) Amazon EFS (Elastic File System)
B) Amazon FSx for Windows File Server
C) Amazon S3 (Simple Storage Service)
D) Amazon EBS (Elastic Block Store)

### Question 2
A media company needs high-performance file storage for their video editing workloads that require POSIX-compliant file system with high throughput and low latency. They are currently using Lustre file systems on-premises.

What AWS service should they consider for their cloud migration?

A) Amazon FSx for Lustre
B) Amazon FSx for Windows File Server
C) Amazon EFS
D) Amazon S3 Glacier

### Question 3
Which statement BEST describes the primary difference between Amazon FSx and Amazon EFS?

A) FSx is only for Windows workloads while EFS is only for Linux workloads
B) FSx provides high-performance specialized file systems while EFS provides general-purpose NFS storage
C) FSx is more expensive than EFS in all scenarios
D) FSx can only be accessed from a single Availability Zone while EFS spans multiple AZs

### Question 4
A company wants to use Amazon FSx for Windows File Server for their enterprise applications. Which features does this service provide? (Select TWO)

A) Integration with Microsoft Active Directory
B) Support for NFS protocol
C) SMB protocol support
D) Object-level storage
E) Block-level storage

### Question 5
An organization is running high-performance computing (HPC) workloads that require a file system optimized for compute-intensive applications with high throughput to Amazon S3.

Which Amazon FSx file system type would be MOST suitable for this use case?

A) Amazon FSx for Windows File Server
B) Amazon FSx for Lustre
C) Amazon FSx for NetApp ONTAP
D) Amazon FSx for OpenZFS

### Question 6
A company is concerned about the backup and recovery capabilities of their Amazon FSx file system. What backup options are available for Amazon FSx?

A) FSx does not support backups; users must implement their own backup solution
B) FSx only supports manual backups that must be initiated by users
C) FSx supports both automatic daily backups and user-initiated backups
D) FSx backups are only available for Windows File Server, not for Lustre

### Question 7
Which of the following workloads would benefit MOST from using Amazon FSx for Lustre?

A) Small business file sharing and collaboration
B) High-performance computing and machine learning training
C) Web application static content hosting
D) Database transaction log storage

### Question 8
A company wants to understand the cost structure of Amazon FSx. How is Amazon FSx typically priced?

A) Based on the number of users accessing the file system
B) Based on the amount of data transferred in and out
C) Based on storage capacity provisioned and throughput capacity
D) Based on the number of API calls made to the service

### Question 9
An enterprise needs to migrate their existing NetApp storage systems to AWS while maintaining compatibility with their current applications and management tools.

Which Amazon FSx option would be MOST appropriate?

A) Amazon FSx for Windows File Server
B) Amazon FSx for Lustre
C) Amazon FSx for NetApp ONTAP
D) Amazon FSx for OpenZFS

### Question 10
What is a key security feature available across all Amazon FSx file system types?

A) Integration with AWS Identity and Access Management (IAM) only
B) Encryption at rest and in transit capabilities
C) Built-in antivirus scanning
D) Automatic data loss prevention (DLP)

---

## Section 2: Answers and Justifications

### Question 1: Answer B - Amazon FSx for Windows File Server

**Correct Answer Justification:**
Amazon FSx for Windows File Server is specifically designed for Windows-based workloads that require SMB protocol support and Active Directory integration. It provides fully managed Windows file systems with high performance and sub-millisecond latencies, making it ideal for migrating Windows file servers to AWS while maintaining compatibility with existing applications.

**Why other options are incorrect:**
- **A) Amazon EFS:** EFS provides NFS (Network File System) protocol, not SMB, and is designed for Linux-based workloads, not Windows with Active Directory integration.
- **C) Amazon S3:** S3 is object storage, not a file system, and doesn't provide the SMB protocol or file system interface required for Windows applications.
- **D) Amazon EBS:** EBS provides block storage that attaches to individual EC2 instances, not shared file storage with SMB protocol support.

### Question 2: Answer A - Amazon FSx for Lustre

**Correct Answer Justification:**
Amazon FSx for Lustre is specifically designed for high-performance computing workloads that require high throughput and low latency. Lustre is a parallel distributed file system commonly used for HPC applications, and FSx for Lustre provides a fully managed version that's optimized for compute-intensive workloads like video processing and rendering.

**Why other options are incorrect:**
- **B) Amazon FSx for Windows File Server:** This is designed for Windows-based applications with SMB protocol, not high-performance POSIX-compliant workloads.
- **C) Amazon EFS:** While EFS is POSIX-compliant, it's designed for general-purpose use cases and doesn't provide the specialized high-performance characteristics of Lustre.
- **D) Amazon S3 Glacier:** Glacier is archival storage with retrieval times measured in minutes to hours, completely unsuitable for high-performance computing workloads.

### Question 3: Answer B - FSx provides high-performance specialized file systems while EFS provides general-purpose NFS storage

**Correct Answer Justification:**
The key difference is that Amazon FSx offers specialized, high-performance file systems (Windows File Server, Lustre, NetApp ONTAP, OpenZFS) optimized for specific workloads, while Amazon EFS provides general-purpose NFS storage that scales automatically. FSx is designed for performance-critical applications that need specialized file system features.

**Why other options are incorrect:**
- **A) FSx is only for Windows workloads while EFS is only for Linux workloads:** This is incorrect. FSx supports multiple file system types including Linux-compatible options like Lustre and OpenZFS.
- **C) FSx is more expensive than EFS in all scenarios:** Cost depends on specific use case, performance requirements, and usage patterns. This is not universally true.
- **D) FSx can only be accessed from a single Availability Zone while EFS spans multiple AZs:** This is incorrect. FSx file systems can be configured for multi-AZ deployment depending on the file system type.

### Question 4: Answer A and C - Integration with Microsoft Active Directory and SMB protocol support

**Correct Answer Justification:**
Amazon FSx for Windows File Server provides native integration with Microsoft Active Directory for authentication and authorization, and supports the SMB (Server Message Block) protocol, which is the standard protocol for Windows file sharing. These are core features that make it suitable for Windows enterprise environments.

**Why other options are incorrect:**
- **B) Support for NFS protocol:** FSx for Windows File Server uses SMB protocol, not NFS. NFS is used by Amazon EFS.
- **D) Object-level storage:** FSx provides file-level storage, not object-level storage (which is provided by Amazon S3).
- **E) Block-level storage:** FSx provides file-level storage, not block-level storage (which is provided by Amazon EBS).

### Question 5: Answer B - Amazon FSx for Lustre

**Correct Answer Justification:**
Amazon FSx for Lustre is specifically designed for high-performance computing (HPC) workloads and provides optimized integration with Amazon S3. It can seamlessly present S3 objects as files and write changed data back to S3, making it ideal for compute-intensive applications that need high throughput access to large datasets stored in S3.

**Why other options are incorrect:**
- **A) Amazon FSx for Windows File Server:** This is optimized for Windows-based applications, not HPC workloads requiring high throughput to S3.
- **C) Amazon FSx for NetApp ONTAP:** While high-performance, it's designed for enterprise applications migrating from NetApp systems, not specifically for HPC workloads with S3 integration.
- **D) Amazon FSx for OpenZFS:** This is designed for applications requiring OpenZFS features, not specifically optimized for HPC workloads with S3 integration.

### Question 6: Answer C - FSx supports both automatic daily backups and user-initiated backups

**Correct Answer Justification:**
Amazon FSx provides comprehensive backup capabilities including automatic daily backups (which can be configured with retention periods) and user-initiated backups that can be taken at any time. These backups are stored durably and can be used to restore file systems or create new file systems.

**Why other options are incorrect:**
- **A) FSx does not support backups:** This is incorrect. FSx has built-in backup capabilities.
- **B) FSx only supports manual backups:** This is incorrect. FSx supports both automatic and manual backups.
- **D) FSx backups are only available for Windows File Server:** This is incorrect. Backup capabilities are available for all FSx file system types.

### Question 7: Answer B - High-performance computing and machine learning training

**Correct Answer Justification:**
Amazon FSx for Lustre is specifically designed for workloads that require high-performance parallel file systems, such as high-performance computing (HPC), machine learning training, video processing, and financial modeling. These workloads benefit from Lustre's ability to provide high throughput and low latency access to large datasets.

**Why other options are incorrect:**
- **A) Small business file sharing and collaboration:** This use case is better served by Amazon EFS or FSx for Windows File Server, which provide more cost-effective solutions for general file sharing.
- **C) Web application static content hosting:** This is better served by Amazon S3 with CloudFront for content delivery, not a high-performance file system.
- **D) Database transaction log storage:** This typically requires block storage like Amazon EBS with specific IOPS and latency characteristics, not a parallel file system.

### Question 8: Answer C - Based on storage capacity provisioned and throughput capacity

**Correct Answer Justification:**
Amazon FSx pricing is primarily based on the storage capacity you provision (measured in GB or TB) and the throughput capacity you configure (measured in MB/s). This allows you to pay for the performance level you need. Additional charges may apply for backups and data transfer.

**Why other options are incorrect:**
- **A) Based on the number of users accessing the file system:** FSx pricing is not based on user count; it's based on provisioned resources.
- **B) Based on the amount of data transferred in and out:** While data transfer charges may apply, the primary pricing is based on provisioned capacity, not data transfer volume.
- **D) Based on the number of API calls made to the service:** FSx pricing is not based on API calls; it's based on provisioned storage and throughput capacity.

### Question 9: Answer C - Amazon FSx for NetApp ONTAP

**Correct Answer Justification:**
Amazon FSx for NetApp ONTAP is specifically designed for organizations that want to migrate their existing NetApp storage systems to AWS while maintaining compatibility with their current applications, management tools, and operational procedures. It provides the familiar NetApp ONTAP features and APIs in a fully managed AWS service.

**Why other options are incorrect:**
- **A) Amazon FSx for Windows File Server:** This is designed for Windows-based workloads with SMB protocol, not for NetApp system migration.
- **B) Amazon FSx for Lustre:** This is designed for high-performance computing workloads, not for NetApp system migration.
- **D) Amazon FSx for OpenZFS:** This is designed for workloads requiring OpenZFS features, not specifically for NetApp migration scenarios.

### Question 10: Answer B - Encryption at rest and in transit capabilities

**Correct Answer Justification:**
All Amazon FSx file system types support encryption at rest using AWS Key Management Service (KMS) keys and encryption in transit using TLS. This provides comprehensive data protection for sensitive workloads and helps meet compliance requirements across all FSx offerings.

**Why other options are incorrect:**
- **A) Integration with AWS Identity and Access Management (IAM) only:** While IAM integration is available, it's not the only security feature, and the question asks for a key feature available across all FSx types.
- **C) Built-in antivirus scanning:** This is not a standard feature provided by FSx across all file system types.
- **D) Automatic data loss prevention (DLP):** This is not a built-in feature of FSx; DLP would typically be implemented at the application or network level.
