# AWS Aurora - CLF-C02 Practice Questions

## Section 1: CLF-C02 Practice Questions

### Question 1
AnyCompany Financial is migrating their MySQL database to AWS and needs a solution that provides high availability across multiple Availability Zones with automatic failover. They want to minimize database administration overhead while maintaining compatibility with their existing MySQL applications.

Which AWS service BEST meets these requirements?

a) Amazon RDS for MySQL with Multi-AZ deployment
b) Amazon Aurora MySQL
c) Amazon DynamoDB with global tables
d) Amazon EC2 instances with MySQL installed across multiple AZs

### Question 2
A startup company is evaluating database options for their new web application. They expect rapid growth and need a database that can automatically scale storage capacity without downtime. The application uses standard SQL queries and they want to minimize operational overhead.

Which AWS database service characteristic makes Aurora MOST suitable for this scenario?

a) Aurora automatically scales storage from 10 GB to 128 TB in 10 GB increments
b) Aurora requires manual storage provisioning like traditional databases
c) Aurora only supports NoSQL workloads for better scalability
d) Aurora requires application code changes to enable auto-scaling

### Question 3
AnyCompany E-commerce runs a MySQL database on Amazon Aurora and wants to improve read performance for their reporting workloads without affecting their primary database performance. They need a solution that automatically stays synchronized with the primary database.

What Aurora feature should they implement?

a) Create Aurora Serverless to handle read workloads
b) Set up Aurora read replicas
c) Enable Aurora Multi-Master configuration
d) Configure Aurora Global Database

### Question 4
A company is comparing database costs between running MySQL on EC2 instances versus using Amazon Aurora. The database administrator wants to understand Aurora's cost optimization benefits.

Which TWO factors make Aurora cost-effective compared to self-managed databases on EC2? (Select TWO)

a) Aurora eliminates the need for database software licensing fees
b) Aurora automatically manages database backups without additional storage costs
c) Aurora reduces administrative overhead by automating routine database tasks
d) Aurora requires fewer EC2 instances due to its serverless architecture
e) Aurora provides built-in monitoring without additional CloudWatch charges

### Question 5
AnyCompany Global needs to deploy their Aurora database across multiple AWS Regions to serve customers worldwide with low latency. They want to maintain a single primary database for writes while enabling fast local reads in each region.

Which Aurora feature BEST addresses this requirement?

a) Aurora Multi-AZ deployment
b) Aurora Global Database
c) Aurora Serverless v2
d) Aurora read replicas in the same region

### Question 6
A development team is building a new application with unpredictable traffic patterns. They need a database solution that can automatically scale compute capacity up and down based on demand to optimize costs during low-usage periods.

Which Aurora configuration is MOST appropriate for this use case?

a) Aurora Provisioned with manual scaling
b) Aurora Serverless v1
c) Aurora with scheduled scaling policies
d) Aurora Multi-Master cluster

### Question 7
According to the AWS Shared Responsibility Model, which database management tasks are AWS's responsibility when using Amazon Aurora? (Select TWO)

a) Database schema design and optimization
b) Operating system patching and updates
c) Application-level security configurations
d) Hardware maintenance and replacement
e) Database user access management

### Question 8
AnyCompany Healthcare needs to ensure their Aurora database meets compliance requirements for data encryption. They want to understand what encryption options are available without impacting application performance.

Which statement about Aurora encryption is CORRECT?

a) Aurora only supports encryption for data at rest, not in transit
b) Aurora encryption can be enabled after database creation without downtime
c) Aurora supports encryption at rest and in transit with minimal performance impact
d) Aurora encryption requires application code changes to implement

### Question 9
A company is migrating from Oracle Database to AWS and evaluating Aurora PostgreSQL. They want to understand the key differences between Aurora and standard Amazon RDS for PostgreSQL.

Which feature is UNIQUE to Aurora compared to standard RDS for PostgreSQL?

a) Automated backups and point-in-time recovery
b) Multi-AZ deployment for high availability
c) Storage that automatically grows up to 128 TB
d) Integration with AWS Identity and Access Management (IAM)

### Question 10
AnyCompany Analytics runs complex reporting queries that sometimes impact their production Aurora database performance. They need a solution to isolate analytical workloads while maintaining data consistency.

What is the MOST cost-effective approach to address this requirement?

a) Create a separate Aurora cluster and manually sync data
b) Use Aurora read replicas for analytical workloads
c) Migrate analytical workloads to Amazon Redshift
d) Increase the instance size of the primary Aurora cluster

---

## Section 2: Answers and Justifications

### Question 1: Correct Answer - B) Amazon Aurora MySQL

**Why B is correct:**
Aurora MySQL provides native high availability across multiple AZs with automatic failover, typically completing failover in under 30 seconds. It's fully compatible with MySQL applications and significantly reduces administrative overhead through automated patching, backups, and monitoring. Aurora's architecture is specifically designed for cloud-native high availability.

**Why other options are incorrect:**
- A) RDS Multi-AZ provides high availability but requires more administrative overhead and has longer failover times compared to Aurora
- C) DynamoDB is a NoSQL service and wouldn't be compatible with existing MySQL applications
- D) EC2 with MySQL requires significant administrative overhead for setup, maintenance, and high availability configuration

### Question 2: Correct Answer - A) Aurora automatically scales storage from 10 GB to 128 TB in 10 GB increments

**Why A is correct:**
Aurora's storage auto-scaling is a key differentiator. Storage automatically grows as needed without downtime or performance impact, eliminating the need to provision storage capacity upfront. This is particularly valuable for rapidly growing applications where storage requirements are unpredictable.

**Why other options are incorrect:**
- B) Incorrect - Aurora's automatic storage scaling is a key feature that eliminates manual provisioning
- C) Incorrect - Aurora supports SQL workloads, not NoSQL
- D) Incorrect - Aurora's storage auto-scaling works transparently without requiring application changes

### Question 3: Correct Answer - B) Set up Aurora read replicas

**Why B is correct:**
Aurora read replicas are specifically designed for read-heavy workloads like reporting. They automatically stay synchronized with the primary database using Aurora's shared storage architecture, providing consistent data while offloading read traffic from the primary instance.

**Why other options are incorrect:**
- A) Aurora Serverless is for variable workloads, not specifically for read scaling
- C) Multi-Master is for write scaling across multiple instances, not read optimization
- D) Global Database is for cross-region replication, not local read scaling

### Question 4: Correct Answers - A) Aurora eliminates the need for database software licensing fees, C) Aurora reduces administrative overhead by automating routine database tasks

**Why A and C are correct:**
- A) Aurora is included in the service cost without separate MySQL/PostgreSQL licensing fees, unlike some commercial databases
- C) Aurora automates patching, backups, monitoring, and scaling, reducing operational costs and administrative time

**Why other options are incorrect:**
- B) Aurora backups do consume storage, though they're more efficient than traditional backups
- D) Aurora is not serverless by default; it uses provisioned instances
- E) CloudWatch integration may have associated costs for detailed monitoring

### Question 5: Correct Answer - B) Aurora Global Database

**Why B is correct:**
Aurora Global Database enables cross-region replication with a single primary region for writes and up to 5 secondary regions for fast local reads. It provides sub-second data replication and enables disaster recovery across regions.

**Why other options are incorrect:**
- A) Multi-AZ deployment only works within a single region
- C) Serverless v2 is about compute scaling, not geographic distribution
- D) Read replicas in the same region don't address the global latency requirement

### Question 6: Correct Answer - B) Aurora Serverless v1

**Why B is correct:**
Aurora Serverless automatically scales compute capacity based on application demand and can scale down to zero during idle periods, making it ideal for unpredictable workloads. It eliminates the need to provision specific instance sizes.

**Why other options are incorrect:**
- A) Provisioned instances require manual scaling and don't automatically scale to zero
- C) Scheduled scaling doesn't adapt to unpredictable traffic patterns
- D) Multi-Master is for write scaling, not automatic compute scaling based on demand

### Question 7: Correct Answers - B) Operating system patching and updates, D) Hardware maintenance and replacement

**Why B and D are correct:**
Under the shared responsibility model, AWS manages the underlying infrastructure including OS patching and hardware maintenance for managed services like Aurora.

**Why other options are incorrect:**
- A) Database schema design is the customer's responsibility
- C) Application-level security configurations are managed by the customer
- E) Database user access management is the customer's responsibility

### Question 8: Correct Answer - C) Aurora supports encryption at rest and in transit with minimal performance impact

**Why C is correct:**
Aurora supports both encryption at rest (using AWS KMS) and encryption in transit (using SSL/TLS) with minimal performance overhead. This comprehensive encryption approach meets most compliance requirements.

**Why other options are incorrect:**
- A) Aurora supports both at-rest and in-transit encryption
- B) Encryption must be enabled at cluster creation time and cannot be added later
- D) Aurora encryption is transparent to applications and doesn't require code changes

### Question 9: Correct Answer - C) Storage that automatically grows up to 128 TB

**Why C is correct:**
Aurora's automatic storage scaling up to 128 TB is unique to Aurora. Standard RDS requires manual storage provisioning and has lower maximum storage limits depending on the instance type.

**Why other options are incorrect:**
- A) Both Aurora and RDS support automated backups and point-in-time recovery
- B) Both Aurora and RDS support Multi-AZ deployments
- D) Both Aurora and RDS integrate with IAM for authentication and authorization

### Question 10: Correct Answer - B) Use Aurora read replicas for analytical workloads

**Why B is correct:**
Aurora read replicas provide an isolated environment for analytical queries without impacting the primary database. They're cost-effective because they share the same underlying storage as the primary instance and automatically stay synchronized.

**Why other options are incorrect:**
- A) A separate Aurora cluster would be more expensive and require manual data synchronization
- C) Redshift migration would be complex and expensive for this use case
- D) Increasing instance size doesn't isolate workloads and may be unnecessarily expensive
