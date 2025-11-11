# AWS Storage Gateway - CLF-C02 Practice Questions

## Section 1: CLF-C02 Practice Questions

### Question 1
A company wants to gradually migrate their on-premises file shares to AWS while maintaining local access for frequently used files. They need a solution that provides NFS and SMB protocol support. Which AWS Storage Gateway type should they choose?

A) Volume Gateway - Stored Volumes
B) Volume Gateway - Cached Volumes
C) File Gateway
D) Tape Gateway

### Question 2
An organization currently uses physical tape backup infrastructure and wants to eliminate the costs and complexity of managing tapes while maintaining compatibility with their existing backup software. Which AWS service would be MOST appropriate?

A) AWS Backup
B) Amazon S3 Glacier
C) AWS Storage Gateway - Tape Gateway
D) AWS DataSync

### Question 3
What is the primary benefit of AWS Storage Gateway's local caching feature?

A) It reduces AWS storage costs by compressing data
B) It provides low-latency access to frequently accessed data
C) It automatically encrypts data before sending to AWS
D) It creates multiple copies of data for redundancy

### Question 4
A company needs to backup their on-premises block storage to AWS while keeping the primary data locally for low-latency access. Which Storage Gateway configuration should they use?

A) File Gateway
B) Volume Gateway - Stored Volumes
C) Volume Gateway - Cached Volumes
D) Tape Gateway

### Question 5
Which AWS storage services can AWS Storage Gateway integrate with? (Select TWO)

A) Amazon EFS
B) Amazon S3
C) Amazon EBS
D) AWS Instance Store
E) Amazon FSx

### Question 6
A retail company wants to move their primary storage to AWS cloud while keeping frequently accessed data cached locally for performance. Which Storage Gateway type provides this capability?

A) File Gateway
B) Volume Gateway - Stored Volumes
C) Volume Gateway - Cached Volumes
D) Tape Gateway

### Question 7
What protocol does AWS Storage Gateway Tape Gateway (VTL) use to communicate with backup applications?

A) NFS (Network File System)
B) SMB (Server Message Block)
C) iSCSI (Internet Small Computer Systems Interface)
D) HTTP/HTTPS

### Question 8
A company is concerned about the security of data transmitted between their on-premises Storage Gateway and AWS. Which security feature addresses this concern?

A) Data is automatically compressed before transmission
B) Data is encrypted in transit using SSL/TLS
C) Data is stored in multiple AWS regions automatically
D) Data is backed up to multiple storage classes

### Question 9
Which deployment options are available for AWS Storage Gateway? (Select TWO)

A) As a managed service running entirely in AWS
B) As a virtual machine in your on-premises environment
C) As a hardware appliance provided by AWS
D) As a container running on Amazon ECS
E) As a Lambda function

### Question 10
A company wants to understand the cost structure of AWS Storage Gateway. Which of the following are typical cost components? (Select TWO)

A) Monthly gateway usage charges
B) Charges for data stored in connected AWS storage services
C) Charges for the number of files stored
D) Charges for the number of users accessing the gateway
E) Charges for gateway software licensing

---

## Section 2: Answers and Justifications

### Question 1: Answer C - File Gateway

**Correct Answer Justification:**
File Gateway is specifically designed for file share scenarios and provides NFS v3/v4.1 and SMB protocol support. It stores files as objects in Amazon S3 while providing a file system interface to on-premises applications. The local cache ensures frequently accessed files are available with low latency.

**Why other options are incorrect:**
- **A) Volume Gateway - Stored Volumes**: Provides iSCSI block storage, not file shares with NFS/SMB protocols
- **B) Volume Gateway - Cached Volumes**: Also provides iSCSI block storage, not file-level access
- **D) Tape Gateway**: Designed for backup applications using Virtual Tape Library, not file shares

### Question 2: Answer C - AWS Storage Gateway - Tape Gateway

**Correct Answer Justification:**
Tape Gateway (VTL - Virtual Tape Library) is specifically designed to replace physical tape infrastructure while maintaining compatibility with existing backup software. It presents virtual tapes to backup applications and stores data in S3, with archival to Glacier/Deep Archive.

**Why other options are incorrect:**
- **A) AWS Backup**: A backup service but doesn't provide tape compatibility for existing backup software
- **B) Amazon S3 Glacier**: A storage service but doesn't provide the VTL interface needed for backup software compatibility
- **D) AWS DataSync**: A data transfer service, not a backup solution with tape compatibility

### Question 3: Answer B - It provides low-latency access to frequently accessed data

**Correct Answer Justification:**
Local caching is the key performance feature of Storage Gateway. It stores frequently accessed data locally (on-premises) while the full dataset resides in AWS. This provides the best of both worlds: cloud storage benefits with local performance for hot data.

**Why other options are incorrect:**
- **A) Reduces AWS storage costs by compressing data**: While compression may occur, the primary benefit of caching is performance, not cost reduction
- **C) Automatically encrypts data**: Encryption is a separate security feature, not the primary benefit of caching
- **D) Creates multiple copies for redundancy**: Caching is for performance, not redundancy (though AWS storage provides durability)

### Question 4: Answer B - Volume Gateway - Stored Volumes

**Correct Answer Justification:**
Stored Volumes keep the primary data locally on-premises for low-latency access while asynchronously backing up point-in-time snapshots to Amazon S3 as EBS snapshots. This configuration provides local performance with cloud backup.

**Why other options are incorrect:**
- **A) File Gateway**: Provides file-level access, not block storage backup
- **C) Volume Gateway - Cached Volumes**: Stores primary data in S3 with local caching, opposite of the requirement
- **D) Tape Gateway**: For backup applications using VTL, not block storage backup

### Question 5: Answer B and C - Amazon S3 and Amazon EBS

**Correct Answer Justification:**
- **Amazon S3**: File Gateway stores files as S3 objects, and Tape Gateway stores virtual tapes in S3
- **Amazon EBS**: Volume Gateway creates EBS snapshots for backup and recovery

**Why other options are incorrect:**
- **A) Amazon EFS**: Storage Gateway doesn't integrate with EFS
- **D) AWS Instance Store**: Ephemeral storage, not used by Storage Gateway
- **E) Amazon FSx**: Storage Gateway doesn't integrate with FSx

### Question 6: Answer C - Volume Gateway - Cached Volumes

**Correct Answer Justification:**
Cached Volumes store the primary dataset in Amazon S3 while caching frequently accessed data locally. This provides cloud-first storage with local performance for hot data, exactly matching the requirement.

**Why other options are incorrect:**
- **A) File Gateway**: Provides file access, but the question asks about primary storage migration
- **B) Volume Gateway - Stored Volumes**: Keeps primary data locally, not in the cloud
- **D) Tape Gateway**: For backup scenarios, not primary storage

### Question 7: Answer C - iSCSI (Internet Small Computer Systems Interface)

**Correct Answer Justification:**
Tape Gateway presents a Virtual Tape Library (VTL) interface to backup applications using the iSCSI protocol. This allows existing backup software to treat virtual tapes as if they were physical tapes connected via iSCSI.

**Why other options are incorrect:**
- **A) NFS**: Used by File Gateway for file shares, not Tape Gateway
- **B) SMB**: Also used by File Gateway for file shares, not Tape Gateway
- **D) HTTP/HTTPS**: Used for management and data transfer to AWS, but not the protocol for backup applications

### Question 8: Answer B - Data is encrypted in transit using SSL/TLS

**Correct Answer Justification:**
AWS Storage Gateway encrypts all data in transit between the on-premises gateway and AWS using SSL/TLS encryption. This ensures data security during transmission over the internet or AWS Direct Connect.

**Why other options are incorrect:**
- **A) Data compression**: May occur but is for efficiency, not security
- **C) Multi-region storage**: Not automatic and is for availability, not transit security
- **D) Multiple storage classes**: For cost optimization, not transit security

### Question 9: Answer B and C - Virtual machine and Hardware appliance

**Correct Answer Justification:**
- **Virtual machine**: Can be deployed on VMware ESXi, Microsoft Hyper-V, or Linux KVM in your data center
- **Hardware appliance**: AWS provides physical appliances for customers who prefer hardware solutions

**Why other options are incorrect:**
- **A) Managed service in AWS**: Storage Gateway runs on-premises to provide hybrid connectivity
- **D) Container on ECS**: Not a supported deployment option
- **E) Lambda function**: Not a supported deployment option

### Question 10: Answer A and B - Gateway usage charges and AWS storage service charges

**Correct Answer Justification:**
- **Monthly gateway usage charges**: AWS charges a monthly fee per active gateway
- **AWS storage service charges**: You pay for data stored in S3, EBS snapshots, etc., at standard AWS storage pricing

**Why other options are incorrect:**
- **C) Number of files**: AWS doesn't charge based on file count for Storage Gateway
- **D) Number of users**: User count doesn't affect Storage Gateway pricing
- **E) Software licensing**: Storage Gateway software is included in the service, no separate licensing fees
