# AWS EFS - CLF-C02 Practice Questions

## Section 1: CLF-C02 Practice Questions

### Question 1
A company needs shared file storage that can be accessed simultaneously by multiple EC2 instances across different Availability Zones. Which AWS service would be the MOST appropriate solution?

A) Amazon EBS (Elastic Block Store)
B) Amazon EFS (Elastic File System)
C) Amazon S3 (Simple Storage Service)
D) AWS Instance Store

### Question 2
What is a key characteristic of Amazon EFS that differentiates it from Amazon EBS?

A) EFS provides block-level storage while EBS provides file-level storage
B) EFS can only be accessed by one EC2 instance at a time
C) EFS can be accessed concurrently by multiple EC2 instances
D) EFS is less expensive than EBS for all use cases

### Question 3
A startup wants to implement a file storage solution that automatically scales up and down based on usage without requiring capacity planning. Which feature of Amazon EFS addresses this requirement?

A) Provisioned throughput mode
B) Elastic scaling
C) Multi-AZ replication
D) Encryption at rest

### Question 4
Which storage classes are available in Amazon EFS? (Select TWO)

A) Standard
B) Glacier
X C) Infrequent Access (IA)
D) Deep Archive
E) Reduced Redundancy

### Question 5
A company is concerned about the cost of their Amazon EFS usage. 
They have files that are accessed frequently during business hours but rarely accessed on weekends. Which EFS feature would help optimize costs?

A) Provisioned Throughput mode
B) Max I/O performance mode
C) Intelligent Tiering
D) Burst credits

### Question 6
What type of file system interface does Amazon EFS provide?

A) SMB (Server Message Block)
B) NFS (Network File System)
C) iSCSI (Internet Small Computer Systems Interface)
D) FTP (File Transfer Protocol)

### Question 7
A development team needs to share code repositories and build artifacts across multiple EC2 instances in their development environment. Which AWS storage service would be MOST suitable for this use case?

A) Amazon S3
B) Amazon EBS
C) Amazon EFS
D) AWS Instance Store

### Question 8
How does Amazon EFS ensure high availability and durability?

A) Data is stored in a single Availability Zone with local backups
B) Data is automatically replicated across multiple Availability Zones within a region
C) Data is stored only in memory for faster access
D) Data is manually backed up to Amazon S3

### Question 9
Which of the following statements about Amazon EFS security is correct?

A) EFS does not support encryption of data
B) EFS only supports encryption at rest, not in transit
C) EFS supports both encryption at rest and encryption in transit
D) EFS encryption requires a third-party solution

### Question 10
A company wants to use Amazon EFS with their containerized applications running on Amazon ECS. Which statement about this integration is TRUE?

A) EFS cannot be used with containerized applications
B) EFS can provide persistent storage for containers across multiple tasks
C) EFS requires special container runtime modifications
D) EFS only works with EC2 instances, not containers

---

## Section 2: Answers and Justifications

### Question 1: Answer B - Amazon EFS (Elastic File System)

**Correct Answer Justification:**
Amazon EFS is specifically designed for shared file storage that can be accessed simultaneously by multiple EC2 instances across different Availability Zones. EFS provides a fully managed NFS (Network File System) that supports concurrent access from thousands of EC2 instances.

**Why other options are incorrect:**
- **A) Amazon EBS:** EBS volumes can only be attached to one EC2 instance at a time (except for Multi-Attach volumes which have limitations and are not suitable for general shared file access).
- **C) Amazon S3:** S3 is object storage, not a file system, and doesn't provide the POSIX-compliant file system interface needed for traditional file sharing.
- **D) AWS Instance Store:** Instance Store provides temporary storage that's physically attached to the host computer and cannot be shared between instances.

### Question 2: Answer C - EFS can be accessed concurrently by multiple EC2 instances

**Correct Answer Justification:**
The key differentiator of Amazon EFS is its ability to provide shared file storage that can be accessed concurrently by multiple EC2 instances. This is fundamentally different from EBS, which typically provides block storage for single-instance access.

**Why other options are incorrect:**
- **A) EFS provides block-level storage while EBS provides file-level storage:** This is backwards. EFS provides file-level storage (NFS), while EBS provides block-level storage.
- **B) EFS can only be accessed by one EC2 instance at a time:** This is incorrect. Concurrent access is EFS's primary feature.
- **D) EFS is less expensive than EBS for all use cases:** Cost comparison depends on usage patterns, access frequency, and storage requirements. This is not universally true.

### Question 3: Answer B - Elastic scaling

**Correct Answer Justification:**
Amazon EFS automatically scales storage capacity up and down as files are added and removed, eliminating the need for capacity planning. This elastic scaling feature means you only pay for the storage you actually use, and the file system grows and shrinks automatically.

**Why other options are incorrect:**
- **A) Provisioned throughput mode:** This is about performance throughput, not automatic capacity scaling.
- **C) Multi-AZ replication:** This is about availability and durability, not automatic scaling.
- **D) Encryption at rest:** This is a security feature, not related to automatic scaling.

### Question 4: Answer A and C - Standard and Infrequent Access (IA)

**Correct Answer Justification:**
Amazon EFS offers multiple storage classes: Standard (for frequently accessed files), Infrequent Access (IA) for files accessed less frequently, and Archive for long-term archival. The question asks for two options, and Standard and IA are the two primary storage classes commonly referenced in CLF-C02 materials.

**Why other options are incorrect:**
- **B) Glacier and D) Deep Archive:** These are Amazon S3 storage classes, not EFS storage classes.
- **E) Reduced Redundancy:** This was an S3 storage class that has been deprecated.

### Question 5: Answer C - Intelligent Tiering

**Correct Answer Justification:**
EFS Intelligent Tiering automatically moves files between storage classes based on access patterns. Files that aren't accessed for a certain period are automatically moved to the lower-cost Infrequent Access (IA) storage class, helping optimize costs for varying access patterns.

**Why other options are incorrect:**
- **A) Provisioned Throughput mode:** This affects performance throughput costs, not storage costs based on access patterns.
- **B) Max I/O performance mode:** This is about performance characteristics, not cost optimization.
- **D) Burst credits:** This relates to throughput performance in Bursting mode, not cost optimization for access patterns.

### Question 6: Answer B - NFS (Network File System)

**Correct Answer Justification:**
Amazon EFS provides a standard NFS (Network File System) interface, making it compatible with existing applications and tools that use standard file system operations. EFS is POSIX-compliant and supports standard file system semantics.

**Why other options are incorrect:**
- **A) SMB (Server Message Block):** SMB is used by Amazon FSx for Windows File Server, not EFS.
- **C) iSCSI:** This is a block-level protocol used by services like EBS, not the file-level protocol used by EFS.
- **D) FTP:** FTP is a file transfer protocol, not a file system interface.

### Question 7: Answer C - Amazon EFS

**Correct Answer Justification:**
Amazon EFS is ideal for development environments where multiple EC2 instances need shared access to code repositories and build artifacts. EFS provides the shared file system capabilities needed for collaborative development work, allowing multiple instances to read and write to the same files simultaneously.

**Why other options are incorrect:**
- **A) Amazon S3:** While S3 can store files, it doesn't provide the file system interface needed for development tools and doesn't support concurrent file-level operations like a traditional file system.
- **B) Amazon EBS:** EBS volumes can typically only be attached to one instance at a time, making them unsuitable for shared access scenarios.
- **D) AWS Instance Store:** Instance Store is temporary storage that's lost when instances are stopped, making it unsuitable for persistent shared storage.

### Question 8: Answer B - Data is automatically replicated across multiple Availability Zones within a region

**Correct Answer Justification:**
Amazon EFS automatically stores data redundantly across multiple Availability Zones within an AWS region. This multi-AZ storage provides high availability and durability, ensuring that data remains accessible even if one Availability Zone becomes unavailable.

**Why other options are incorrect:**
- **A) Data is stored in a single Availability Zone with local backups:** EFS stores data across multiple AZs, not in a single AZ.
- **C) Data is stored only in memory for faster access:** EFS provides persistent storage, not in-memory storage.
- **D) Data is manually backed up to Amazon S3:** While you can backup EFS to S3, the high availability and durability come from the automatic multi-AZ replication, not manual backups.

### Question 9: Answer C - EFS supports both encryption at rest and encryption in transit

**Correct Answer Justification:**
Amazon EFS supports comprehensive encryption capabilities including both encryption at rest (using AWS KMS keys) and encryption in transit (using TLS). This provides end-to-end encryption for data security.

**Why other options are incorrect:**
- **A) EFS does not support encryption of data:** This is incorrect. EFS supports multiple encryption options.
- **B) EFS only supports encryption at rest, not in transit:** This is incorrect. EFS supports both types of encryption.
- **D) EFS encryption requires a third-party solution:** This is incorrect. EFS provides native encryption capabilities integrated with AWS KMS.

### Question 10: Answer B - EFS can provide persistent storage for containers across multiple tasks

**Correct Answer Justification:**
Amazon EFS integrates well with containerized applications on Amazon ECS (and EKS). EFS can provide persistent, shared storage that survives container restarts and can be accessed by multiple containers across different tasks, making it ideal for stateful containerized applications.

**Why other options are incorrect:**
- **A) EFS cannot be used with containerized applications:** This is incorrect. EFS has native support for container integration.
- **C) EFS requires special container runtime modifications:** This is incorrect. EFS can be mounted in containers using standard NFS mounting procedures.
- **D) EFS only works with EC2 instances, not containers:** This is incorrect. EFS works with both EC2 instances and containerized applications running on services like ECS and EKS.
