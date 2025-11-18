# AWS DocumentDB - CLF-C02 Practice Questions

## Section 1: CLF-C02 Practice Questions

### 1) AnyCompany E-commerce is building a product catalog system that needs to store diverse product information with varying attributes. Electronics have specifications like screen size and processor type, while clothing has attributes like fabric and size charts. They want a database solution that can handle this flexible data structure without requiring schema changes for new product types.

Which AWS database service BEST meets these requirements?

a) Amazon RDS for MySQL
b) Amazon DynamoDB
c) Amazon DocumentDB
d) Amazon Redshift

### 2) A startup is migrating their MongoDB application to AWS and wants a fully managed solution that maintains compatibility with their existing MongoDB drivers and tools. They need automatic scaling, backup management, and high availability without managing database infrastructure.

Which AWS service should they choose?

a) Amazon RDS with MongoDB engine
b) MongoDB on Amazon EC2 instances
c) Amazon DocumentDB
d) Amazon DynamoDB with MongoDB compatibility layer

### 3) According to the AWS Shared Responsibility Model, which of the following are customer responsibilities when using Amazon DocumentDB? (Select TWO)

a) Database software patching and updates
b) Network security group configuration
c) Physical security of data centers
d) Database user access management
e) Infrastructure monitoring and threat detection

### 4) AnyCompany Social Media needs to store user profiles with varying information fields. Some users have extensive professional backgrounds, while others have minimal profile data. The application frequently queries user data by different attributes like location, interests, and connections.

What makes Amazon DocumentDB suitable for this use case?

a) It provides fixed schema enforcement for consistent data structure
b) It stores data as flexible JSON-like documents that can vary in structure
c) It automatically creates relational tables for different user types
d) It only supports simple key-value data storage

### 5) A company wants to understand the cost structure of Amazon DocumentDB before implementation. Which factors directly impact DocumentDB pricing? (Select TWO)

a) Number of database schemas created
b) Database instance compute capacity
c) Storage space consumed by data
d) Number of MongoDB compatibility features used
e) Geographic location of database administrators

### 6) AnyCompany Content Management is building a system to store articles, blog posts, and multimedia content. Each content type has different metadata requirements, and they need to perform complex queries across various content attributes.

Which database approach would be MOST cost-effective and scalable for this scenario?

a) Create separate Amazon RDS instances for each content type
b) Use Amazon DocumentDB to store all content as flexible documents
c) Implement a data warehouse solution with Amazon Redshift
d) Store all content in Amazon S3 with metadata in separate databases

### 7) Which statement BEST describes the high availability features of Amazon DocumentDB?

a) It requires manual configuration of backup and restore procedures
b) It automatically replicates data across multiple Availability Zones with continuous backup
c) It only provides high availability within a single Availability Zone
d) It requires customers to manage failover procedures manually

### 8) AnyCompany Analytics wants to integrate their DocumentDB database with other AWS services for monitoring and access control. Which AWS services commonly work with DocumentDB to provide comprehensive cloud solutions? (Select TWO)

a) AWS IAM for user authentication and authorization
b) Amazon Route 53 for database load balancing
c) Amazon CloudWatch for performance monitoring and alerting
d) AWS CodeDeploy for database schema deployment
e) Amazon SES for database notification emails

### 9) A development team is comparing database options for their new application. They need to store product reviews with varying structures - some reviews include ratings, photos, and detailed comments, while others are simple text feedback.

What is the PRIMARY advantage of choosing Amazon DocumentDB over a traditional relational database for this use case?

a) DocumentDB provides better performance for all types of queries
b) DocumentDB eliminates the need for data backup and recovery
c) DocumentDB allows flexible document structures without predefined schemas
d) DocumentDB automatically translates data into multiple languages

### 10) AnyCompany Financial Services is evaluating Amazon DocumentDB for storing customer transaction histories and account information. They are concerned about data security and compliance requirements.

Which security feature is automatically provided by Amazon DocumentDB?

a) Application-level user authentication
b) Encryption of data at rest and in transit
c) Automatic data anonymization for compliance
d) Built-in fraud detection algorithms

## Section 2: Answers and Justifications

### 1) Correct Answer: C - Amazon DocumentDB

**Why C is correct:** Amazon DocumentDB is specifically designed for flexible, document-based data storage where different records can have varying structures. This makes it ideal for product catalogs where electronics, clothing, and other product types have completely different attributes without requiring schema modifications.

**Why other options are incorrect:**
- A) Amazon RDS for MySQL requires fixed table schemas, making it difficult to handle varying product attributes
- B) Amazon DynamoDB is a key-value/document database but is not MongoDB-compatible and has different use case optimization
- D) Amazon Redshift is a data warehouse service designed for analytics, not operational document storage

### 2) Correct Answer: C - Amazon DocumentDB

**Why C is correct:** Amazon DocumentDB is specifically designed to be MongoDB-compatible, allowing existing MongoDB applications, drivers, and tools to work with minimal changes while providing full AWS management of infrastructure, scaling, and backups.

**Why other options are incorrect:**
- A) Amazon RDS does not offer a MongoDB engine option
- B) MongoDB on EC2 requires manual infrastructure management, defeating the purpose of wanting a fully managed solution
- D) Amazon DynamoDB does not provide MongoDB compatibility and would require application rewrites

### 3) Correct Answers: B - Network security group configuration, D - Database user access management

**Why B and D are correct:** Under the AWS Shared Responsibility Model, customers are responsible for configuring network security (security groups, VPCs) and managing database-level access (user accounts, permissions, authentication).

**Why other options are incorrect:**
- A) AWS manages database software patching and updates as part of the managed service
- C) AWS is responsible for physical security of data centers
- E) AWS handles infrastructure monitoring and threat detection at the service level

### 4) Correct Answer: B - It stores data as flexible JSON-like documents that can vary in structure

**Why B is correct:** DocumentDB's core strength is storing documents with flexible schemas, allowing user profiles to have different fields and structures without requiring database schema changes for each variation.

**Why other options are incorrect:**
- A) DocumentDB specifically avoids fixed schema enforcement to provide flexibility
- C) DocumentDB is a document database, not a relational database that creates tables
- D) DocumentDB supports complex document structures, not just simple key-value pairs

### 5) Correct Answers: B - Database instance compute capacity, C - Storage space consumed by data

**Why B and C are correct:** DocumentDB pricing is primarily based on the compute resources (instance types and sizes) and the amount of data stored, following AWS's pay-for-what-you-use model.

**Why other options are incorrect:**
- A) The number of schemas doesn't directly impact pricing in DocumentDB
- D) MongoDB compatibility features are included in the service without separate charges
- E) Administrator location has no impact on DocumentDB pricing

### 6) Correct Answer: B - Use Amazon DocumentDB to store all content as flexible documents

**Why B is correct:** DocumentDB can efficiently store different content types (articles, blogs, multimedia metadata) as documents with varying structures, providing cost-effective storage and flexible querying capabilities in a single managed service.

**Why other options are incorrect:**
- A) Multiple RDS instances would be more expensive and complex to manage
- C) Redshift is designed for analytics/data warehousing, not operational content management
- D) Splitting content and metadata across services adds complexity and potential consistency issues

### 7) Correct Answer: B - It automatically replicates data across multiple Availability Zones with continuous backup

**Why B is correct:** DocumentDB automatically provides high availability through multi-AZ replication and continuous backup to S3, ensuring data durability and availability without manual intervention.

**Why other options are incorrect:**
- A) DocumentDB automates backup and restore procedures as a managed service feature
- C) DocumentDB specifically provides multi-AZ availability, not single-AZ limitation
- D) DocumentDB handles failover automatically without requiring manual customer intervention

### 8) Correct Answers: A - AWS IAM for user authentication and authorization, C - Amazon CloudWatch for performance monitoring and alerting

**Why A and C are correct:** IAM integrates with DocumentDB to control access permissions, while CloudWatch automatically monitors DocumentDB performance metrics and can trigger alerts, representing core AWS service integrations.

**Why other options are incorrect:**
- B) Route 53 is for DNS routing, not database load balancing
- D) CodeDeploy is for application deployment, not database schema management
- E) SES is for email services, not a core DocumentDB integration

### 9) Correct Answer: C - DocumentDB allows flexible document structures without predefined schemas

**Why C is correct:** The primary advantage of DocumentDB over relational databases is schema flexibility, allowing reviews with different structures (ratings, photos, text) to be stored without defining rigid table schemas upfront.

**Why other options are incorrect:**
- A) Performance depends on specific use cases and query patterns, not universally better
- B) All AWS database services provide backup and recovery capabilities
- D) Language translation is not a database feature but an application-level concern

### 10) Correct Answer: B - Encryption of data at rest and in transit

**Why B is correct:** Amazon DocumentDB automatically provides encryption capabilities for data protection, which is crucial for financial services compliance and is managed by AWS as part of the service.

**Why other options are incorrect:**
- A) Application-level authentication is a customer responsibility, not automatically provided
- C) Data anonymization requires custom application logic, not automatic database features
- D) Fraud detection algorithms are application-specific and not built into the database service
