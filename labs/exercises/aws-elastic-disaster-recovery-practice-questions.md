# AWS Elastic Disaster Recovery - CLF-C02 Practice Questions

## Section 1: CLF-C02 Practice Questions

### Question 1
A company wants to protect their on-premises servers by replicating them to AWS for disaster recovery purposes. They need a solution that provides continuous data replication with minimal downtime during recovery. Which AWS service should they use?

A) AWS Backup
B) AWS Elastic Disaster Recovery
C) AWS Storage Gateway
D) AWS DataSync

### Question 2
What is the primary benefit of AWS Elastic Disaster Recovery's continuous replication feature?

A) It reduces storage costs by compressing data
B) It provides low Recovery Point Objectives (RPO) measured in seconds
C) It automatically scales compute resources during normal operations
D) It eliminates the need for backup strategies

### Question 3
A financial services company needs to meet regulatory requirements for disaster recovery testing. They want to test their recovery procedures without disrupting their production environment. Which AWS Elastic Disaster Recovery feature addresses this requirement?

A) Multi-site active/active deployment
B) Automated failback capabilities
C) Non-disruptive recovery testing
D) Cross-region replication

### Question 4
Which disaster recovery strategy provides the fastest recovery time but at the highest cost?

A) Pilot Light
B) Warm Standby
C) Multi-Site Active/Active
D) Backup and Restore

### Question 5
A company is using AWS Elastic Disaster Recovery to protect their on-premises servers. During a disaster recovery event, what type of AWS resources are launched to restore their applications?

A) AWS Lambda functions
B) Amazon ECS containers
C) Amazon EC2 instances
D) AWS Fargate tasks

### Question 6
Which components are part of AWS Elastic Disaster Recovery architecture? (Select TWO)

A) Source servers
B) Distribution points
C) Replication servers
D) Content delivery networks
E) API gateways

### Question 7
A manufacturing company wants to implement disaster recovery for their on-premises VMware environment. They need a solution that can replicate their virtual machines to AWS with minimal changes to their existing infrastructure. What does AWS Elastic Disaster Recovery support?

A) Only physical servers
B) Only AWS EC2 instances
C) Both physical servers and virtual machines
D) Only containerized applications

### Question 8
What is the purpose of the "staging area" in AWS Elastic Disaster Recovery?

A) To store backup copies of production data
B) To provide an isolated environment for replication servers and testing
C) To cache frequently accessed data for better performance
D) To distribute content globally through edge locations

### Question 9
A company is concerned about the cost of implementing AWS Elastic Disaster Recovery. Which pricing components should they expect? (Select TWO)

A) Monthly charge per replicated server
B) Charges based on the number of users
C) EC2 instance costs during recovery events
D) Licensing fees for disaster recovery software
E) Charges for the number of applications protected

### Question 10
A retail company needs to ensure their e-commerce platform can recover quickly from disasters while maintaining data consistency. Which AWS Elastic Disaster Recovery feature ensures applications start correctly after recovery?

A) Load balancing across multiple regions
B) Application-consistent snapshots
C) Automatic scaling of resources
D) Content caching at edge locations

---

## Section 2: Answers and Justifications

### Question 1: Answer B - AWS Elastic Disaster Recovery

**Correct Answer Justification:**
AWS Elastic Disaster Recovery (DRS) is specifically designed for protecting on-premises and cloud-based servers by providing continuous data replication to AWS. It enables quick recovery with minimal downtime by maintaining real-time replicas of source servers that can be launched as EC2 instances during disaster events.

**Why other options are incorrect:**
- **A) AWS Backup**: A backup service that creates point-in-time backups, but doesn't provide continuous replication or the fast recovery capabilities of DRS
- **C) AWS Storage Gateway**: A hybrid storage service for connecting on-premises to AWS storage, not specifically designed for disaster recovery of entire servers
- **D) AWS DataSync**: A data transfer service for one-time or scheduled data transfers, not for continuous replication and disaster recovery

### Question 2: Answer B - It provides low Recovery Point Objectives (RPO) measured in seconds

**Correct Answer Justification:**
The continuous replication feature of AWS Elastic Disaster Recovery synchronizes data changes in real-time, resulting in Recovery Point Objectives (RPO) measured in seconds. This means minimal data loss during disaster events, as the replicated data is nearly current with the source systems.

**Why other options are incorrect:**
- **A) Reduces storage costs by compressing data**: While compression may occur, the primary benefit of continuous replication is data protection and low RPO, not cost reduction
- **C) Automatically scales compute resources**: DRS focuses on disaster recovery, not auto-scaling during normal operations
- **D) Eliminates the need for backup strategies**: DRS complements but doesn't replace comprehensive backup strategies

### Question 3: Answer C - Non-disruptive recovery testing

**Correct Answer Justification:**
AWS Elastic Disaster Recovery allows organizations to perform recovery testing without affecting their production environment. This feature enables regular testing of disaster recovery procedures to ensure compliance with regulatory requirements while maintaining business operations.

**Why other options are incorrect:**
- **A) Multi-site active/active deployment**: This is a deployment strategy, not specifically for testing without disruption
- **B) Automated failback capabilities**: This helps with returning to normal operations, not testing without disruption
- **D) Cross-region replication**: This provides geographic separation but doesn't address non-disruptive testing requirements

### Question 4: Answer C - Multi-Site Active/Active

**Correct Answer Justification:**
Multi-Site Active/Active strategy runs full production environments in multiple locations simultaneously, providing immediate failover capability with zero downtime. However, this approach has the highest cost because it requires maintaining full duplicate infrastructure continuously.

**Why other options are incorrect:**
- **A) Pilot Light**: Lower cost but slower recovery time as it maintains only core components
- **B) Warm Standby**: Moderate cost and recovery time with scaled-down environment
- **D) Backup and Restore**: Lowest cost but longest recovery time, not typically considered a disaster recovery strategy in the context of DRS

### Question 5: Answer C - Amazon EC2 instances

**Correct Answer Justification:**
During a disaster recovery event, AWS Elastic Disaster Recovery launches the protected servers as Amazon EC2 instances. The service automatically provisions EC2 instances based on the replicated data and configurations from the source servers.

**Why other options are incorrect:**
- **A) AWS Lambda functions**: Serverless compute service, not used for recovering full server environments
- **B) Amazon ECS containers**: Container service, not the primary recovery mechanism for traditional server workloads
- **D) AWS Fargate tasks**: Serverless container platform, not used for traditional server disaster recovery

### Question 6: Answer A and C - Source servers and Replication servers

**Correct Answer Justification:**
- **Source servers**: The original physical or virtual servers being protected by the disaster recovery solution
- **Replication servers**: Lightweight EC2 instances that receive and process the replicated data from source servers

**Why other options are incorrect:**
- **B) Distribution points**: Part of content delivery networks, not disaster recovery architecture
- **D) Content delivery networks**: Used for content distribution, not disaster recovery
- **E) API gateways**: Used for API management, not part of DRS architecture

### Question 7: Answer C - Both physical servers and virtual machines

**Correct Answer Justification:**
AWS Elastic Disaster Recovery supports protection of both physical servers and virtual machines from various platforms including VMware, Hyper-V, and other virtualization technologies. This flexibility allows organizations to protect their existing infrastructure regardless of the deployment model.

**Why other options are incorrect:**
- **A) Only physical servers**: DRS supports virtual machines as well as physical servers
- **B) Only AWS EC2 instances**: DRS is designed to protect on-premises infrastructure, not just EC2 instances
- **D) Only containerized applications**: DRS focuses on server-level protection, not specifically containerized applications

### Question 8: Answer B - To provide an isolated environment for replication servers and testing

**Correct Answer Justification:**
The staging area in AWS Elastic Disaster Recovery is an isolated AWS subnet where replication servers operate and where recovery testing can be performed without affecting production systems. It provides a safe environment for replication activities and validation testing.

**Why other options are incorrect:**
- **A) Store backup copies of production data**: The staging area hosts replication infrastructure, not data storage
- **C) Cache frequently accessed data**: This describes caching mechanisms, not the staging area function
- **D) Distribute content globally**: This describes content delivery networks, not the DRS staging area

### Question 9: Answer A and C - Monthly charge per replicated server and EC2 instance costs during recovery events

**Correct Answer Justification:**
- **Monthly charge per replicated server**: AWS DRS charges a monthly fee for each server being replicated
- **EC2 instance costs during recovery events**: When recovery instances are launched, standard EC2 pricing applies

**Why other options are incorrect:**
- **B) Charges based on number of users**: DRS pricing is not based on user count
- **D) Licensing fees for disaster recovery software**: DRS is a managed service with no separate software licensing fees
- **E) Charges for number of applications**: Pricing is based on servers, not individual applications

### Question 10: Answer B - Application-consistent snapshots

**Correct Answer Justification:**
Application-consistent snapshots ensure that applications and their data are in a consistent state when recovery occurs. This feature coordinates with the operating system and applications to create snapshots at points where data integrity is maintained, ensuring applications start correctly after recovery.

**Why other options are incorrect:**
- **A) Load balancing across multiple regions**: This provides availability but doesn't ensure application consistency during recovery
- **C) Automatic scaling of resources**: This addresses capacity management, not application consistency
- **D) Content caching at edge locations**: This is a content delivery feature, not related to application consistency during disaster recovery
