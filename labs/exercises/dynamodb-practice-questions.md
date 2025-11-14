# AWS DynamoDB - CLF-C02 Practice Questions

## Section 1: CLF-C02 Practice Questions

### 1) AnyCompany Gaming is developing a mobile game that will have millions of players worldwide. They need a database solution that can handle unpredictable traffic spikes during game events and provide single-digit millisecond response times for player data retrieval. The development team wants to focus on game features rather than database administration.

Which AWS service BEST meets these requirements?

a) Amazon RDS with Multi-AZ deployment
b) Amazon DynamoDB
c) Amazon Aurora Serverless
d) Amazon ElastiCache

### 2) A startup is building a web application and expects highly variable traffic patterns. They want a database solution where they only pay for actual usage without upfront capacity planning. The application needs to store user profiles and session data with flexible data structures.

Which DynamoDB pricing model BEST fits this scenario?

a) Provisioned capacity with Reserved Instances
b) On-demand pricing
c) Dedicated capacity reservations
d) Spot pricing for databases

### 3) AnyCompany E-commerce wants to replicate their DynamoDB tables across multiple AWS regions to provide low-latency access to customers worldwide and ensure business continuity in case of regional failures.

Which DynamoDB feature should they implement?

a) Cross-region read replicas
b) Multi-AZ deployments
c) Global Tables
d) DynamoDB Streams

### 4) According to the AWS Shared Responsibility Model for DynamoDB, which of the following are customer responsibilities? (Select TWO)

a) Database software patching and updates
b) IAM policies for table access control
c) Physical security of data centers
d) Data encryption configuration using AWS KMS
e) Hardware maintenance and replacement

### 5) AnyCompany IoT has thousands of sensors sending data continuously to their application. They need a database that can automatically scale to handle varying data ingestion rates without manual intervention and provide real-time analytics capabilities.

Which combination of AWS services BEST addresses these requirements?

a) Amazon RDS with read replicas and Amazon QuickSight
b) Amazon DynamoDB with Amazon Kinesis Data Analytics
c) Amazon Aurora with Amazon Redshift
d) Amazon ElastiCache with Amazon CloudWatch

### 6) A company is migrating from a traditional relational database to DynamoDB for their user management system. They are concerned about the learning curve and want to understand the key difference in data modeling approaches.

What is the PRIMARY difference between DynamoDB and traditional relational databases?

a) DynamoDB requires predefined table schemas while relational databases are flexible
b) DynamoDB uses SQL queries while relational databases use NoSQL
c) DynamoDB uses key-value and document data models while relational databases use structured tables with relationships
d) DynamoDB only supports read operations while relational databases support both read and write

### 7) AnyCompany Financial needs to ensure their DynamoDB tables containing sensitive customer data are encrypted and access is properly controlled. They want to use their own encryption keys for compliance requirements.

Which security features should they implement? (Select TWO)

a) Encryption at rest using AWS KMS customer-managed keys
b) VPC endpoints for private network access
c) Database-level user authentication
d) AWS CloudTrail for API logging
e) Amazon GuardDuty for threat detection

### 8) A development team is building a real-time chat application that needs to trigger notifications whenever new messages are added to their DynamoDB table. They want a serverless solution that automatically processes these events.

Which AWS service integration BEST supports this requirement?

a) Amazon SQS with DynamoDB
b) AWS Lambda with DynamoDB Streams
c) Amazon SNS with DynamoDB
d) Amazon EventBridge with DynamoDB

### 9) AnyCompany Retail has a DynamoDB table that experiences consistent traffic patterns throughout the day. They want to optimize costs while ensuring predictable performance for their production workload.

Which DynamoDB capacity and pricing approach should they choose?

a) On-demand pricing for cost optimization
b) Provisioned capacity with Reserved Capacity for cost savings
c) Auto Scaling with on-demand pricing
d) Dedicated capacity with spot pricing

### 10) A company wants to improve the performance of their DynamoDB-based application by reducing latency from milliseconds to microseconds for frequently accessed data. They need a solution that integrates seamlessly with their existing DynamoDB setup.

Which AWS service should they implement?

a) Amazon ElastiCache for Redis
b) Amazon CloudFront
c) DynamoDB Accelerator (DAX)
d) Amazon RDS Proxy

---

## Section 2: Answers and Justifications

### 1) Correct Answer: B - Amazon DynamoDB

**Why B is correct:**
DynamoDB is specifically designed for applications requiring single-digit millisecond latency at any scale. It's a fully managed NoSQL service that automatically scales to handle unpredictable traffic spikes without manual intervention, making it ideal for gaming applications with millions of users. The serverless nature eliminates database administration overhead, allowing developers to focus on application features.

**Why other options are incorrect:**
- A) Amazon RDS requires capacity planning and doesn't provide single-digit millisecond latency at massive scale
- C) Aurora Serverless is for relational workloads and doesn't match the performance requirements for gaming applications
- D) ElastiCache is a caching service, not a primary database solution

### 2) Correct Answer: B - On-demand pricing

**Why B is correct:**
DynamoDB on-demand pricing is perfect for unpredictable traffic patterns as it charges only for actual read/write requests consumed, with no upfront costs or capacity planning required. This aligns with the "trade capital expense for variable expense" cloud benefit and is ideal for startups with uncertain traffic patterns.

**Why other options are incorrect:**
- A) Provisioned capacity requires upfront capacity planning, which contradicts the variable traffic requirement
- C) Dedicated capacity reservations are for high-volume, predictable workloads
- D) Spot pricing doesn't exist for DynamoDB

### 3) Correct Answer: C - Global Tables

**Why C is correct:**
DynamoDB Global Tables provide multi-region, multi-master replication that automatically replicates data across multiple AWS regions. This ensures low-latency access for global customers and provides business continuity with automatic failover capabilities.

**Why other options are incorrect:**
- A) Cross-region read replicas don't exist as a specific DynamoDB feature
- B) Multi-AZ deployments are for RDS, not DynamoDB
- D) DynamoDB Streams capture data changes but don't provide multi-region replication

### 4) Correct Answers: B - IAM policies for table access control, D - Data encryption configuration using AWS KMS

**Why B and D are correct:**
Under the shared responsibility model, customers are responsible for configuring access controls (IAM policies) and encryption settings (AWS KMS configuration) for their DynamoDB tables. These are application-level security configurations that customers must manage.

**Why other options are incorrect:**
- A) Database software patching is AWS's responsibility in managed services
- C) Physical security is always AWS's responsibility
- E) Hardware maintenance is AWS's responsibility in managed services

### 5) Correct Answer: B - Amazon DynamoDB with Amazon Kinesis Data Analytics

**Why B is correct:**
DynamoDB automatically scales to handle varying IoT data ingestion rates without manual intervention, while Kinesis Data Analytics provides real-time analytics capabilities on streaming data. This combination is specifically designed for IoT use cases with variable traffic patterns.

**Why other options are incorrect:**
- A) RDS doesn't auto-scale for variable ingestion rates like IoT scenarios require
- C) Aurora and Redshift are for structured data warehousing, not real-time IoT ingestion
- D) ElastiCache is for caching, not primary data storage for IoT streams

### 6) Correct Answer: C - DynamoDB uses key-value and document data models while relational databases use structured tables with relationships

**Why C is correct:**
This accurately describes the fundamental difference between NoSQL (DynamoDB) and relational databases. DynamoDB uses flexible key-value and document models that don't require predefined schemas, while relational databases use structured tables with defined relationships and schemas.

**Why other options are incorrect:**
- A) This is backwards - DynamoDB is flexible, relational databases require predefined schemas
- B) This is backwards - DynamoDB uses NoSQL, relational databases use SQL
- D) DynamoDB supports both read and write operations

### 7) Correct Answers: A - Encryption at rest using AWS KMS customer-managed keys, B - VPC endpoints for private network access

**Why A and B are correct:**
Customer-managed KMS keys provide the compliance control needed for sensitive financial data encryption, and VPC endpoints ensure private network access without internet exposure, both critical for financial services security requirements.

**Why other options are incorrect:**
- C) DynamoDB uses IAM for access control, not database-level user authentication
- D) CloudTrail is for logging but not a direct security feature for data protection
- E) GuardDuty is for threat detection but not a direct DynamoDB security configuration

### 8) Correct Answer: B - AWS Lambda with DynamoDB Streams

**Why B is correct:**
DynamoDB Streams capture data modification events in real-time and can trigger Lambda functions automatically when new items are added. This provides a serverless, event-driven architecture perfect for real-time chat notifications.

**Why other options are incorrect:**
- A) SQS doesn't directly integrate with DynamoDB for automatic event triggering
- C) SNS doesn't directly integrate with DynamoDB table changes
- D) EventBridge doesn't have native DynamoDB table change integration like Streams

### 9) Correct Answer: B - Provisioned capacity with Reserved Capacity for cost savings

**Why B is correct:**
For consistent, predictable traffic patterns, provisioned capacity with Reserved Capacity provides up to 76% cost savings compared to on-demand pricing. This is the most cost-effective approach for steady-state production workloads.

**Why other options are incorrect:**
- A) On-demand pricing is more expensive for consistent traffic patterns
- C) Auto Scaling with on-demand doesn't provide the cost benefits of Reserved Capacity
- D) Spot pricing doesn't exist for DynamoDB

### 10) Correct Answer: C - DynamoDB Accelerator (DAX)

**Why C is correct:**
DAX is specifically designed as an in-memory cache for DynamoDB that reduces latency from milliseconds to microseconds. It integrates seamlessly with existing DynamoDB applications with minimal code changes and is purpose-built for DynamoDB acceleration.

**Why other options are incorrect:**
- A) ElastiCache requires application changes and isn't DynamoDB-specific
- B) CloudFront is for content delivery, not database acceleration
- D) RDS Proxy is for relational databases, not DynamoDB
