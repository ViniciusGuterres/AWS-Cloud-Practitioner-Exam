# AWS Instance Store - CLF-C02 Practice Questions

## Section 1: CLF-C02 Practice Questions (10 questions)

### Question 1
What is the primary characteristic of AWS instance store volumes?

A) They provide persistent storage that survives instance termination
B) They are network-attached storage devices accessible from multiple instances
C) They provide temporary storage that is physically attached to the host computer
D) They automatically backup data to Amazon S3 every hour

### Question 2
Which of the following statements about instance store pricing is correct?

A) Instance store volumes are charged separately based on storage capacity used
B) Instance store volumes incur additional charges for IOPS performance
C) Instance store storage is included in the EC2 instance pricing with no additional cost
D) Instance store volumes are charged based on data transfer rates

### Question 3
What happens to data stored on instance store volumes when an EC2 instance is stopped?

A) Data is automatically backed up to Amazon EBS
B) Data is preserved and available when the instance is restarted
C) Data is lost permanently and cannot be recovered
D) Data is temporarily moved to Amazon S3 until the instance restarts

### Question 4
Which EC2 instance types typically include instance store volumes?

A) All EC2 instance types include instance store by default
B) Only compute-optimized instances like C5 and M5
C) Storage-optimized instances like I3, D2, and some compute-optimized instances
D) Only instances in the free tier

### Question 5
What is the maximum size limit for a single instance store volume?

A) 1 TB per volume
B) 10 TB per volume
C) It varies by instance type, with some supporting up to 7.5 TB per volume
D) There is no size limit for instance store volumes

### Question 6
Which use case is MOST appropriate for AWS instance store?

A) Storing critical database files that must persist across reboots
B) Temporary processing of large datasets with high I/O requirements
C) Long-term archival storage for compliance purposes
D) Shared storage accessible by multiple EC2 instances

### Question 7
How does instance store performance compare to Amazon EBS?

A) Instance store always provides lower performance than EBS
B) Instance store can provide higher I/O performance due to direct physical attachment
C) Performance is identical between instance store and EBS
D) Instance store performance varies based on network connectivity

### Question 8
What is a key limitation of instance store volumes compared to EBS volumes?

A) Instance store volumes cannot be encrypted
B) Instance store volumes have lower performance capabilities
C) Instance store volumes cannot be backed up or replicated automatically by AWS
D) Instance store volumes are more expensive than EBS volumes

### Question 9
Which AWS service should be used alongside instance store for data persistence?

A) Amazon CloudWatch for automatic backups
B) Amazon S3 or EBS for storing important data that needs to persist
C) AWS Config for data replication
D) Amazon VPC for data protection

### Question 10
When planning for high availability with instance store, what should be considered?

A) Instance store automatically replicates data across multiple Availability Zones
B) Applications must implement their own data replication and backup strategies
C) AWS automatically migrates instance store data during maintenance
D) Instance store provides built-in disaster recovery capabilities

---

## Section 2: Answers and Justifications

### Question 1 - Answer: C
**Correct Answer: C) They provide temporary storage that is physically attached to the host computer**

**Justification:**
- **Why C is correct:** Instance store volumes are temporary storage devices that are physically attached to the host computer running the EC2 instance. This direct physical connection provides high performance but makes the storage temporary.
- **Why A is wrong:** Instance store volumes are ephemeral and do NOT survive instance termination, stop, or failure.
- **Why B is wrong:** Instance store volumes are locally attached, not network-attached storage. They cannot be accessed from multiple instances.
- **Why D is wrong:** Instance store volumes do not automatically backup to S3. Users must implement their own backup strategies.

### Question 2 - Answer: C
**Correct Answer: C) Instance store storage is included in the EC2 instance pricing with no additional cost**

**Justification:**
- **Why C is correct:** Instance store volumes are included in the EC2 instance hourly rate at no additional charge, making them cost-effective for temporary storage needs.
- **Why A is wrong:** There are no separate charges for instance store capacity - it's bundled with the instance cost.
- **Why B is wrong:** IOPS performance for instance store is included in the instance pricing, not charged separately.
- **Why D is wrong:** Data transfer rates for instance store don't incur additional charges beyond standard EC2 pricing.

### Question 3 - Answer: C
**Correct Answer: C) Data is lost permanently and cannot be recovered**

**Justification:**
- **Why C is correct:** When an EC2 instance is stopped (not just rebooted), all data on instance store volumes is permanently lost. This is a fundamental characteristic of ephemeral storage.
- **Why A is wrong:** AWS does not automatically backup instance store data to EBS.
- **Why B is wrong:** Data is NOT preserved when an instance is stopped - only during reboots.
- **Why D is wrong:** AWS does not automatically move instance store data to S3 during stops.

### Question 4 - Answer: C
**Correct Answer: C) Storage-optimized instances like I3, D2, and some compute-optimized instances**

**Justification:**
- **Why C is correct:** Instance store is primarily available on storage-optimized instances (I3, D2, H1) and some compute-optimized instances that are designed for high I/O workloads.
- **Why A is wrong:** Not all EC2 instance types include instance store - many general-purpose instances only have EBS.
- **Why B is wrong:** While some compute-optimized instances have instance store, it's not limited to C5 and M5, and M5 doesn't typically include instance store.
- **Why D is wrong:** Free tier instances (t2.micro, t3.micro) do not include instance store volumes.

### Question 5 - Answer: C
**Correct Answer: C) It varies by instance type, with some supporting up to 7.5 TB per volume**

**Justification:**
- **Why C is correct:** Instance store volume sizes vary significantly by instance type. For example, I3 instances can have volumes up to 7.5 TB, while smaller instances have much smaller volumes.
- **Why A is wrong:** The 1 TB limit is too restrictive - many instance types support larger volumes.
- **Why B is wrong:** 10 TB exceeds the typical maximum for most instance store volumes.
- **Why D is wrong:** There are definite size limits that vary by instance type and configuration.

### Question 6 - Answer: B
**Correct Answer: B) Temporary processing of large datasets with high I/O requirements**

**Justification:**
- **Why B is correct:** Instance store is ideal for temporary, high-performance workloads like data processing, caching, and temporary files where high I/O is needed but persistence isn't required.
- **Why A is wrong:** Critical database files requiring persistence should use EBS, not ephemeral instance store.
- **Why C is wrong:** Long-term archival requires persistent storage like S3 or EBS, not temporary instance store.
- **Why D is wrong:** Instance store cannot be shared between instances - it's locally attached to a single instance.

### Question 7 - Answer: B
**Correct Answer: B) Instance store can provide higher I/O performance due to direct physical attachment**

**Justification:**
- **Why B is correct:** Instance store volumes are directly attached to the physical host, eliminating network latency and providing very high I/O performance, often exceeding EBS performance.
- **Why A is wrong:** Instance store typically provides higher, not lower, performance than EBS due to direct attachment.
- **Why C is wrong:** Performance is not identical - instance store generally offers superior I/O performance.
- **Why D is wrong:** Instance store performance doesn't depend on network connectivity since it's locally attached.

### Question 8 - Answer: C
**Correct Answer: C) Instance store volumes cannot be backed up or replicated automatically by AWS**

**Justification:**
- **Why C is correct:** AWS does not provide automatic backup, snapshot, or replication services for instance store volumes. Users must implement their own backup strategies.
- **Why A is wrong:** Instance store volumes can be encrypted using operating system-level encryption tools.
- **Why B is wrong:** Instance store typically has higher, not lower, performance capabilities than EBS.
- **Why D is wrong:** Instance store is included in EC2 pricing at no additional cost, making it less expensive than EBS.

### Question 9 - Answer: B
**Correct Answer: B) Amazon S3 or EBS for storing important data that needs to persist**

**Justification:**
- **Why B is correct:** Since instance store is ephemeral, important data should be regularly backed up to persistent storage like S3 or EBS to ensure data durability.
- **Why A is wrong:** CloudWatch is for monitoring and logging, not data backup or persistence.
- **Why C is wrong:** AWS Config is for configuration management and compliance, not data storage or replication.
- **Why D is wrong:** VPC provides network isolation but doesn't offer data persistence or backup capabilities.

### Question 10 - Answer: B
**Correct Answer: B) Applications must implement their own data replication and backup strategies**

**Justification:**
- **Why B is correct:** Since instance store provides no built-in redundancy or persistence, applications must implement their own replication, clustering, and backup mechanisms for high availability.
- **Why A is wrong:** Instance store does NOT automatically replicate across AZs - it's local to the host.
- **Why C is wrong:** AWS does not migrate instance store data during maintenance - the data is lost when the instance moves.
- **Why D is wrong:** Instance store provides no built-in disaster recovery - this must be implemented by the user.
