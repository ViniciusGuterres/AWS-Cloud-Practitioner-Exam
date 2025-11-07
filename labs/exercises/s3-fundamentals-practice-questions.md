# AWS CLF-C02 Practice Questions: Amazon S3 Fundamentals

## Section 1: CLF-C02 Practice Questions

### Question 1
What is the maximum size of a single object that can be stored in Amazon S3?

A) 5 GB
B) 5 TB
C) 100 GB
D) 1 TB

### Question 2
Which of the following are characteristics of Amazon S3? (Select TWO)

A) Block-level storage service
B) Object-level storage service
C) Provides 99.999999999% (11 9's) durability
D) Requires pre-provisioning of storage capacity
E) Limited to storing only text files

### Question 3
A company wants to host a static website using Amazon S3. Which S3 feature should they enable?

A) S3 Transfer Acceleration
B) S3 Static Website Hosting
C) S3 Cross-Region Replication
D) S3 Versioning

### Question 4
What is the purpose of an S3 bucket policy?

A) To define lifecycle rules for objects
B) To control access permissions to the bucket and its objects
C) To configure cross-region replication
D) To set up event notifications

### Question 5
A user accidentally deletes an important file from an S3 bucket. Which S3 feature could help recover the file?

A) S3 Transfer Acceleration
B) S3 Cross-Region Replication
C) S3 Versioning
D) S3 Storage Classes

### Question 6
Which statement about S3 bucket names is CORRECT?

A) Bucket names must be unique within your AWS account
B) Bucket names must be globally unique across all AWS accounts
C) Bucket names can contain uppercase letters
D) Bucket names can be changed after creation

### Question 7
What is the default access level for newly created S3 buckets and objects?

A) Public read access
B) Public read/write access
C) Private access
D) Authenticated users only

### Question 8
Which AWS service can be used to distribute S3 content globally with low latency?

A) AWS Direct Connect
B) Amazon CloudFront
C) AWS Global Accelerator
D) Amazon Route 53

### Question 9
A company needs to ensure their S3 data is protected against accidental deletion and corruption. Which S3 features should they implement? (Select TWO)

A) S3 Transfer Acceleration
B) S3 Versioning
C) S3 MFA Delete
D) S3 Storage Classes
E) S3 Cross-Origin Resource Sharing (CORS)

### Question 10
What is the consistency model for Amazon S3?

A) Eventual consistency for all operations
B) Strong consistency for all operations
C) Strong consistency for read operations only
D) Eventual consistency for write operations only

---

## Section 2: Answers and Justifications

### Question 1: Answer B - 5 TB

**Correct Answer Justification:**
The maximum size for a single object in Amazon S3 is 5 TB (terabytes). For objects larger than 100 MB, AWS recommends using multipart upload for better performance and reliability.

**Why other options are incorrect:**
- A) 5 GB: This is the maximum size for a single PUT operation, not the object limit
- C) 100 GB: This is the recommended threshold for using multipart upload
- D) 1 TB: This is smaller than the actual 5 TB limit

### Question 2: Answer B and C

**Correct Answers Justification:**
- B) S3 is an object-level storage service where data is stored as objects within buckets
- C) S3 provides 99.999999999% (11 9's) durability, meaning objects are highly protected against loss

**Why other options are incorrect:**
- A) S3 is object storage, not block storage (EBS provides block storage)
- D) S3 scales automatically without pre-provisioning capacity
- E) S3 can store any type of file, not just text files

### Question 3: Answer B - S3 Static Website Hosting

**Correct Answer Justification:**
S3 Static Website Hosting is the specific feature that allows S3 buckets to serve static websites directly, providing a cost-effective solution for hosting HTML, CSS, JavaScript, and other static content.

**Why other options are incorrect:**
- A) Transfer Acceleration: Speeds up uploads, not for website hosting
- C) Cross-Region Replication: For copying objects across regions
- D) Versioning: For maintaining multiple versions of objects

### Question 4: Answer B - To control access permissions to the bucket and its objects

**Correct Answer Justification:**
S3 bucket policies are JSON-based access policy language used to manage permissions for S3 buckets and objects, defining who can access what resources and under what conditions.

**Why other options are incorrect:**
- A) Lifecycle rules: Managed through lifecycle configuration, not bucket policies
- C) Cross-region replication: Configured through replication rules
- D) Event notifications: Configured through event notification settings

### Question 5: Answer C - S3 Versioning

**Correct Answer Justification:**
S3 Versioning keeps multiple versions of objects in the same bucket, allowing recovery of deleted or modified objects by accessing previous versions.

**Why other options are incorrect:**
- A) Transfer Acceleration: For faster uploads, not data recovery
- B) Cross-Region Replication: Helps with disaster recovery but doesn't address accidental deletion in the source bucket
- D) Storage Classes: For cost optimization, not data recovery

### Question 6: Answer B - Bucket names must be globally unique across all AWS accounts

**Correct Answer Justification:**
S3 bucket names must be globally unique across all AWS accounts and regions because they form part of the URL used to access the bucket.

**Why other options are incorrect:**
- A) Uniqueness is global, not just within your account
- C) Bucket names must be lowercase
- D) Bucket names cannot be changed after creation

### Question 7: Answer C - Private access

**Correct Answer Justification:**
By default, all S3 buckets and objects are private and only accessible to the AWS account owner. Public access must be explicitly granted through bucket policies, ACLs, or other access control mechanisms.

**Why other options are incorrect:**
- A) & B) Public access is not the default and must be explicitly configured
- D) Access is restricted to the account owner by default, not all authenticated users

### Question 8: Answer B - Amazon CloudFront

**Correct Answer Justification:**
Amazon CloudFront is AWS's content delivery network (CDN) service that caches and distributes S3 content from edge locations worldwide, reducing latency for global users.

**Why other options are incorrect:**
- A) Direct Connect: For dedicated network connections to AWS
- C) Global Accelerator: For improving application performance, not content distribution
- D) Route 53: DNS service, doesn't cache or distribute content

### Question 9: Answer B and C

**Correct Answers Justification:**
- B) S3 Versioning: Protects against accidental deletion and corruption by maintaining multiple versions
- C) S3 MFA Delete: Requires multi-factor authentication to delete objects, adding extra protection

**Why other options are incorrect:**
- A) Transfer Acceleration: For upload speed, not data protection
- D) Storage Classes: For cost optimization, not data protection
- E) CORS: For web browser security, not data protection

### Question 10: Answer B - Strong consistency for all operations

**Correct Answer Justification:**
As of December 2020, Amazon S3 provides strong read-after-write consistency for all operations, meaning you can immediately read an object after writing it.

**Why other options are incorrect:**
- A) S3 no longer uses eventual consistency
- C) & D) Consistency applies to all operations, not just specific types
