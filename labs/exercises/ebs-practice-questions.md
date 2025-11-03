# AWS EBS - CLF-C02 Practice Questions

## Section 1: CLF-C02 Practice Questions (10 questions)

### Question 1
A company needs persistent storage for their EC2 instances that will survive instance termination. Which AWS service should they use?

A) Amazon S3
B) Amazon EBS (Elastic Block Store)
C) Instance Store
D) Amazon EFS

### Question 2
Which EBS volume type would be MOST appropriate for a critical production database that requires consistent, high IOPS performance?

A) General Purpose SSD (gp3)
B) Provisioned IOPS SSD (io2)
C) Throughput Optimized HDD (st1)
D) Cold HDD (sc1)

### Question 3
A startup wants to minimize storage costs for their development environment while maintaining reasonable performance. Which EBS volume type offers the best balance of cost and performance?

A) Provisioned IOPS SSD (io1)
B) Throughput Optimized HDD (st1)
C) General Purpose SSD (gp3)
D) Cold HDD (sc1)

### Question 4
What happens to an EBS volume when the EC2 instance it's attached to is terminated?

A) The EBS volume is always deleted
B) The EBS volume is preserved by default
C) The behavior depends on the "Delete on Termination" setting
D) The EBS volume is moved to S3 automatically

### Question 5
A company processes large datasets sequentially and needs high throughput storage at a lower cost. Which EBS volume type is MOST suitable?

A) General Purpose SSD (gp3)
B) Provisioned IOPS SSD (io2)
C) Throughput Optimized HDD (st1)
D) Cold HDD (sc1)

### Question 6
Which statement about EBS snapshots is correct?

A) Snapshots are stored locally on the EC2 instance
B) Snapshots are incremental and stored in Amazon S3
C) Snapshots can only be taken when the instance is stopped
D) Snapshots are automatically deleted when the volume is deleted

### Question 7
An organization wants to ensure their sensitive data stored on EBS volumes is encrypted. What is the EASIEST way to achieve this?

A) Use third-party encryption software on the EC2 instance
B) Enable EBS encryption when creating the volume
C) Manually encrypt files before storing them on EBS
D) Use AWS CloudHSM for all encryption needs

### Question 8
Which of the following is a key difference between EBS and Instance Store?

A) EBS is faster than Instance Store
B) Instance Store is more expensive than EBS
C) EBS data persists when the instance is stopped, Instance Store data does not
D) Instance Store can be attached to multiple instances simultaneously

### Question 9
A company needs to copy an EBS snapshot to another AWS region for disaster recovery purposes. Is this possible?

A) No, EBS snapshots cannot be copied between regions
B) Yes, but only for encrypted snapshots
C) Yes, snapshots can be copied to any AWS region
D) No, you must create a new volume in the target region first

### Question 10
What is the primary benefit of using EBS Multi-Attach feature?

A) It reduces storage costs by sharing volumes
B) It allows a single EBS volume to be attached to multiple EC2 instances simultaneously
C) It automatically creates backups across multiple Availability Zones
D) It increases the performance of individual EC2 instances

---

## Section 2: Answers and Justifications

### Question 1: **Answer B - Amazon EBS (Elastic Block Store)**

**Correct Answer Justification:**
Amazon EBS provides persistent block storage that survives EC2 instance termination (unless "Delete on Termination" is enabled). EBS volumes are network-attached storage that can be detached from one instance and attached to another, making them ideal for persistent storage needs.

**Why other options are incorrect:**
- **A) Amazon S3:** While S3 provides persistent storage, it's object storage, not block storage suitable for operating systems and databases that EC2 instances typically require.
- **C) Instance Store:** This is ephemeral storage that is lost when the instance stops or terminates, making it unsuitable for persistent storage requirements.
- **D) Amazon EFS:** While EFS provides persistent storage, it's a file system service, not block storage, and is typically used for shared file storage across multiple instances.

### Question 2: **Answer B - Provisioned IOPS SSD (io2)**

**Correct Answer Justification:**
Provisioned IOPS SSD (io2) is specifically designed for critical business applications and databases that require consistent, high IOPS performance. It allows you to provision specific IOPS levels (up to 64,000 IOPS) and guarantees that performance level, making it ideal for production databases.

**Why other options are incorrect:**
- **A) General Purpose SSD (gp3):** While gp3 offers good performance, it uses a burst model and may not provide the consistent high IOPS required for critical production databases.
- **C) Throughput Optimized HDD (st1):** This is optimized for sequential workloads and throughput, not the random I/O patterns typical of databases.
- **D) Cold HDD (sc1):** This is the lowest-cost option designed for infrequently accessed data, not suitable for production databases requiring high performance.

### Question 3: **Answer C - General Purpose SSD (gp3)**

**Correct Answer Justification:**
General Purpose SSD (gp3) offers the best balance of cost and performance for most workloads, including development environments. It provides good baseline performance with the ability to burst, and it's more cost-effective than Provisioned IOPS while offering better performance than HDD options.

**Why other options are incorrect:**
- **A) Provisioned IOPS SSD (io1):** This is more expensive and designed for high-performance production workloads, not cost-conscious development environments.
- **B) Throughput Optimized HDD (st1):** While cheaper per GB, it's optimized for sequential workloads and may not provide adequate performance for general development tasks.
- **D) Cold HDD (sc1):** This is the lowest cost but also lowest performance option, suitable only for infrequently accessed data, not active development work.

### Question 4: **Answer C - The behavior depends on the "Delete on Termination" setting**

**Correct Answer Justification:**
EBS volumes have a "Delete on Termination" attribute that determines whether the volume is deleted when the instance terminates. By default, root volumes are set to delete on termination (true), while additional EBS volumes are set to persist (false). This setting can be modified when launching instances or after launch.

**Why other options are incorrect:**
- **A) Always deleted:** This is incorrect because the behavior is configurable and depends on the "Delete on Termination" setting.
- **B) Preserved by default:** This is partially incorrect because root volumes are deleted by default, while additional volumes are preserved by default.
- **D) Moved to S3 automatically:** EBS volumes are not automatically moved to S3; they either persist as EBS volumes or are deleted based on the termination setting.

### Question 5: **Answer C - Throughput Optimized HDD (st1)**

**Correct Answer Justification:**
Throughput Optimized HDD (st1) is specifically designed for frequently accessed, throughput-intensive workloads that require high sequential I/O performance, such as big data processing, data warehouses, and log processing. It offers high throughput at a lower cost per GB compared to SSD options.

**Why other options are incorrect:**
- **A) General Purpose SSD (gp3):** While it offers good performance, it's more expensive per GB and optimized for general-purpose workloads rather than high-throughput sequential processing.
- **B) Provisioned IOPS SSD (io2):** This is the most expensive option and optimized for random I/O, not sequential throughput workloads.
- **D) Cold HDD (sc1):** This is designed for infrequently accessed data and provides the lowest throughput performance, unsuitable for active data processing.

### Question 6: **Answer B - Snapshots are incremental and stored in Amazon S3**

**Correct Answer Justification:**
EBS snapshots are incremental backups stored in Amazon S3. After the initial snapshot, subsequent snapshots only store the changed blocks, making them space and cost-efficient. They leverage S3's durability and can be used to create new volumes or copy to other regions.

**Why other options are incorrect:**
- **A) Stored locally on EC2 instance:** Snapshots are stored in S3, not locally on EC2 instances, which provides better durability and availability.
- **C) Only taken when instance is stopped:** Snapshots can be taken while the instance is running, though stopping the instance ensures data consistency.
- **D) Automatically deleted when volume is deleted:** Snapshots persist independently of the source volume and must be manually deleted or managed through lifecycle policies.

### Question 7: **Answer B - Enable EBS encryption when creating the volume**

**Correct Answer Justification:**
EBS provides built-in encryption that can be enabled when creating a volume. This encrypts data at rest using AWS KMS keys and also encrypts data in transit between the EC2 instance and EBS volume. It's the easiest and most integrated approach for EBS encryption.

**Why other options are incorrect:**
- **A) Third-party encryption software:** While possible, this adds complexity and overhead compared to native EBS encryption.
- **C) Manually encrypt files:** This is application-level encryption and doesn't provide the comprehensive protection of volume-level encryption.
- **D) AWS CloudHSM:** While CloudHSM can be used for key management, EBS encryption with KMS is simpler and sufficient for most use cases.

### Question 8: **Answer C - EBS data persists when the instance is stopped, Instance Store data does not**

**Correct Answer Justification:**
The key difference is data persistence. EBS volumes are network-attached storage that persists independently of the EC2 instance lifecycle, while Instance Store provides ephemeral storage that is lost when the instance stops, hibernates, or terminates.

**Why other options are incorrect:**
- **A) EBS is faster:** Actually, Instance Store typically provides higher performance due to direct physical attachment to the host.
- **B) Instance Store is more expensive:** Instance Store is included with certain instance types at no additional charge, while EBS has separate storage costs.
- **D) Instance Store can be attached to multiple instances:** Instance Store is tied to a specific instance and cannot be shared, while some EBS volumes support Multi-Attach.

### Question 9: **Answer C - Yes, snapshots can be copied to any AWS region**

**Correct Answer Justification:**
EBS snapshots can be copied to any AWS region, making them useful for disaster recovery, data migration, and compliance requirements. The copy operation transfers the snapshot data to the target region where it can be used to create new volumes.

**Why other options are incorrect:**
- **A) Cannot be copied between regions:** This is incorrect; cross-region snapshot copying is a standard EBS feature.
- **B) Only for encrypted snapshots:** Both encrypted and unencrypted snapshots can be copied between regions.
- **D) Must create new volume first:** You copy the snapshot first, then create volumes from the copied snapshot in the target region.

### Question 10: **Answer B - It allows a single EBS volume to be attached to multiple EC2 instances simultaneously**

**Correct Answer Justification:**
EBS Multi-Attach enables a single Provisioned IOPS SSD (io1 or io2) volume to be attached to multiple EC2 instances simultaneously within the same Availability Zone. This is useful for applications that need shared storage across multiple instances, such as clustered databases or distributed file systems.

**Why other options are incorrect:**
- **A) Reduces storage costs:** Multi-Attach doesn't reduce costs; you still pay for the full volume capacity regardless of how many instances access it.
- **C) Automatic backups across AZs:** Multi-Attach doesn't provide backup functionality; it's about concurrent access within a single AZ.
- **D) Increases individual instance performance:** Multi-Attach is about sharing access, not improving individual instance performance, and may actually require coordination between instances to avoid conflicts.
