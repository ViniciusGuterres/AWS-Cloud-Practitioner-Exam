# AWS DynamoDB - CLF-C02 Practice Questions (Set 2)

## Section 1: CLF-C02 Practice Questions

### 1) AnyCompany Social Media is experiencing rapid user growth and needs a database solution that can automatically handle traffic increases without downtime or performance degradation. Their current relational database requires manual scaling and causes application slowdowns during peak usage periods.

What is the PRIMARY advantage of migrating to DynamoDB for this scenario?

a) DynamoDB provides ACID transactions for all operations
b) DynamoDB offers automatic scaling without manual intervention
c) DynamoDB supports complex SQL joins and relationships
d) DynamoDB provides cheaper storage costs than all other database options

### 2) A company is evaluating database options for their new microservices architecture. They need a solution that eliminates server management, provides consistent single-digit millisecond performance, and integrates well with serverless applications.

Which database characteristic makes DynamoDB the BEST choice for this architecture?

a) Support for complex relational queries
b) Serverless and fully managed operation
c) Built-in data warehousing capabilities
d) Automatic data compression features

### 3) AnyCompany Logistics wants to implement a solution where changes to their DynamoDB inventory table automatically trigger updates to their warehouse management system. They need real-time processing without managing infrastructure.

Which AWS services combination BEST addresses this requirement?

a) DynamoDB + Amazon SQS + Amazon EC2
b) DynamoDB + DynamoDB Streams + AWS Lambda
c) DynamoDB + Amazon Kinesis + Amazon ECS
d) DynamoDB + AWS Step Functions + Amazon RDS

### 4) According to AWS best practices, which of the following scenarios are MOST suitable for choosing DynamoDB over Amazon RDS? (Select TWO)

a) Applications requiring complex multi-table joins and transactions
b) Applications with unpredictable traffic patterns and scaling requirements
c) Applications needing single-digit millisecond response times at scale
d) Applications requiring strict ACID compliance across multiple tables
e) Applications with well-defined relational data models

### 5) AnyCompany FinTech needs to ensure their DynamoDB tables meet strict compliance requirements. They must demonstrate that all database access is logged and that data is encrypted both at rest and in transit.

Which AWS services should they implement to meet these compliance requirements? (Select TWO)

a) AWS CloudTrail for API call logging
b) Amazon Inspector for vulnerability scanning
c) AWS KMS for encryption key management
d) Amazon GuardDuty for threat detection
e) AWS Config for resource compliance monitoring

### 6) A startup is building a mobile application and wants to minimize their initial infrastructure costs while ensuring they can scale rapidly if the app becomes popular. They need a database solution with no upfront commitments.

Which DynamoDB pricing approach BEST fits their requirements?

a) Provisioned capacity with 3-year Reserved Instances
b) On-demand pricing with automatic scaling
c) Dedicated capacity reservations
d) Provisioned capacity with manual scaling

### 7) AnyCompany Healthcare is migrating patient data to AWS and needs to understand their responsibilities for securing DynamoDB tables containing protected health information (PHI).

Under the AWS Shared Responsibility Model, which security aspects are the customer's responsibility for DynamoDB?

a) Physical security of AWS data centers
b) DynamoDB software patching and updates
c) IAM user permissions and access policies
d) Network infrastructure maintenance

### 8) A development team wants to reduce the latency of their DynamoDB queries from 5-10 milliseconds to under 1 millisecond for their high-frequency trading application. They need a solution that requires minimal application code changes.

Which AWS service should they implement?

a) Amazon ElastiCache for Redis
b) Amazon CloudFront
c) DynamoDB Accelerator (DAX)
d) Amazon RDS Proxy

### 9) AnyCompany Retail operates in multiple countries and wants to provide fast database access to customers worldwide while maintaining data consistency. They need automatic replication across regions with local read/write capabilities.

Which DynamoDB feature should they implement?

a) Cross-region backup and restore
b) Multi-AZ deployments
c) Global Tables with multi-region replication
d) Read replicas in multiple regions

### 10) A company is concerned about the operational overhead of managing their current database infrastructure. They want to eliminate tasks like patching, backup management, and capacity planning while maintaining high availability.

Which statement BEST describes how DynamoDB addresses these operational concerns?

a) DynamoDB requires manual patching but automates backup management
b) DynamoDB is fully managed, eliminating all operational database tasks
c) DynamoDB automates scaling but requires manual backup configuration
d) DynamoDB eliminates patching but requires capacity planning for performance

---

## Section 2: Answers and Justifications

### 1) Correct Answer: B - DynamoDB offers automatic scaling without manual intervention

**Why B is correct:**
DynamoDB's automatic scaling capability is its primary advantage for handling rapid user growth. It can automatically adjust read and write capacity based on traffic patterns without downtime or manual intervention, directly addressing the problem of manual scaling and performance degradation during peak usage.

**Why other options are incorrect:**
- A) ACID transactions are available but not the primary advantage for scaling scenarios
- C) DynamoDB is NoSQL and doesn't support SQL joins - this is actually a limitation
- D) Cost comparison depends on usage patterns; automatic scaling is the key benefit here

### 2) Correct Answer: B - Serverless and fully managed operation

**Why B is correct:**
DynamoDB's serverless nature eliminates server management completely, which is essential for microservices architectures. The fully managed operation provides consistent performance and integrates seamlessly with other serverless services like Lambda, making it ideal for modern application architectures.

**Why other options are incorrect:**
- A) Complex relational queries are not supported in DynamoDB (NoSQL limitation)
- C) DynamoDB is not a data warehousing solution
- D) Data compression is a feature but not the primary characteristic for microservices

### 3) Correct Answer: B - DynamoDB + DynamoDB Streams + AWS Lambda

**Why B is correct:**
DynamoDB Streams capture real-time data changes and can automatically trigger Lambda functions for processing. This combination provides serverless, real-time event processing without infrastructure management, perfectly matching the requirement for automatic inventory updates.

**Why other options are incorrect:**
- A) EC2 requires infrastructure management, contradicting the serverless requirement
- C) Kinesis is for streaming analytics, not direct DynamoDB change capture
- D) Step Functions orchestrate workflows but don't directly capture DynamoDB changes

### 4) Correct Answers: B - Applications with unpredictable traffic patterns and scaling requirements, C - Applications needing single-digit millisecond response times at scale

**Why B and C are correct:**
DynamoDB excels at handling unpredictable traffic through automatic scaling and provides consistent single-digit millisecond latency regardless of scale. These are DynamoDB's core strengths that differentiate it from RDS.

**Why other options are incorrect:**
- A) Complex joins are better suited for RDS relational databases
- D) Strict ACID compliance across multiple tables is an RDS strength
- E) Well-defined relational models are better served by RDS

### 5) Correct Answers: A - AWS CloudTrail for API call logging, C - AWS KMS for encryption key management

**Why A and C are correct:**
CloudTrail logs all API calls to DynamoDB for compliance auditing, and AWS KMS manages encryption keys for both data at rest and in transit encryption. These services directly address the compliance requirements for logging and encryption.

**Why other options are incorrect:**
- B) Inspector scans for vulnerabilities but doesn't provide compliance logging or encryption
- D) GuardDuty detects threats but doesn't meet the specific logging and encryption requirements
- E) Config monitors resource compliance but doesn't provide the required logging and encryption capabilities

### 6) Correct Answer: B - On-demand pricing with automatic scaling

**Why B is correct:**
On-demand pricing requires no upfront commitments and charges only for actual usage, perfect for startups with uncertain traffic patterns. Automatic scaling ensures they can handle rapid growth without manual intervention or capacity planning.

**Why other options are incorrect:**
- A) 3-year Reserved Instances require upfront commitments, unsuitable for startups
- C) Dedicated capacity requires significant upfront investment
- D) Manual scaling contradicts the need for rapid, automatic scaling capability

### 7) Correct Answer: C - IAM user permissions and access policies

**Why C is correct:**
Under the shared responsibility model, customers are responsible for configuring access controls, including IAM policies that determine who can access DynamoDB tables and what operations they can perform. This is critical for protecting PHI data.

**Why other options are incorrect:**
- A) Physical security is always AWS's responsibility
- B) Software patching is AWS's responsibility for managed services
- D) Network infrastructure maintenance is AWS's responsibility

### 8) Correct Answer: C - DynamoDB Accelerator (DAX)

**Why C is correct:**
DAX is specifically designed to reduce DynamoDB latency to microseconds (under 1 millisecond) and requires minimal code changes. It's purpose-built for DynamoDB acceleration and is the only option that meets the sub-millisecond requirement with minimal application changes.

**Why other options are incorrect:**
- A) ElastiCache requires significant application changes and isn't DynamoDB-specific
- B) CloudFront is for content delivery, not database acceleration
- D) RDS Proxy is for relational databases, not DynamoDB

### 9) Correct Answer: C - Global Tables with multi-region replication

**Why C is correct:**
DynamoDB Global Tables provide automatic multi-region replication with local read/write capabilities in each region. This ensures fast access worldwide while maintaining eventual consistency across all regions, directly addressing the global performance and consistency requirements.

**Why other options are incorrect:**
- A) Cross-region backup doesn't provide local read/write capabilities
- B) Multi-AZ is within a single region, not global
- D) Read replicas don't exist as a specific DynamoDB feature

### 10) Correct Answer: B - DynamoDB is fully managed, eliminating all operational database tasks

**Why B is correct:**
DynamoDB is a fully managed service that handles patching, backups, scaling, and infrastructure management automatically. This eliminates the operational overhead mentioned in the question, allowing teams to focus on application development rather than database administration.

**Why other options are incorrect:**
- A) DynamoDB handles patching automatically, not manually
- C) DynamoDB can auto-scale and handles backups automatically
- D) DynamoDB provides automatic scaling options, eliminating the need for manual capacity planning
