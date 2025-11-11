Act as a **Specialist AWS Cloud Architecture Professional** preparing a candidate for the **AWS Certified Cloud Practitioner (CLF-C02) exam**.

Your task is to create a set of **10 practice questions** specifically focused on **AWS SERVICE HERE**. These questions must:

1.  Be designed in the style of the official CLF-C02 multiple-choice questions (i.e., realistic difficulty and scope).
2.  Test practical knowledge relevant to the foundational-level exam (e.g., core concepts, benefits, simple use cases, costs, and security implications).

**Output Format:**

1.  **Section 1: CLF-C02 Practice Questions (10 questions)**
    * Present each question with its multiple-choice options (A, B, C, D).
    * You can add question with more than one option correct (e.g Select two options)
2.  **Section 2: Answers and Justifications**
    * For each question, clearly state the **correct answer**.
    * Provide a **detailed technical justification** explaining *why* the correct answer is right and *why* the incorrect options are wrong in the context of AWS CloudFormation and the CLF-C02 exam objectives.


Obs.: Put the output file into the folder labs/exercises

## CLF-C02 questions examples:

### 1) AnyCompany Business stores a growing amount of customer data in Amazon S3. Their manager is concerned about storage costs and asks IT to implement a solution to move older data to cheaper storage. The data is frequently accessed for the first 30 days, occasionally accessed for the next 60 days, and rarely accessed after 90 days.

What should they do in this situation to optimize costs while maintaining appropriate access to the data?


a) Create a lifecycle rule to transition objects to S3 Standard-Infrequent Access (S3 Standard-IA) after 30 days, transition to S3 Glacier after 90 days. 


b) Create a lifecycle rule to immediately transition all objects to S3 Glacier and set up a restore policy.


c) Create a lifecycle rule to delete all objects after 90 days and rely on database backups.


d) Create multiple S3 buckets with different storage classes and manually move objects between buckets as they age.

Correct: A

### 2) Which statement BEST describes S3 Lifecycle?


a) A backup service that creates copies of your S3 objects in different AWS Regions to protect against Regional failures.


b) A feature that automatically compresses Amazon S3 objects after a certain period to reduce storage costs.


c) A monitoring system that alerts administrators when Amazon S3 objects have not been accessed for a specified period.


d) A feature used to define rules to automatically transition objects between different storage classes, or delete them based on age or usage patterns.

Correct: D


### 3) AnyCompany Media wants to migrate its file shares to AWS while maintaining compatibility with existing applications. They need a solution that supports Server Message Block (SMB) protocol and integrates with Microsoft Active Directory.

a) Amazon Elastic File System (Amazon EFS)

b) Amazon S3 File Gateway

c) Amazon FSx for Windows File Server

d) Amazon Elastic Block Store (Amazon EBS)

Correct: C

### 4) AnyCompany has a large collection of files stored on-premises that needs to be backed up to the AWS Cloud. They want to maintain local access to frequently used files while using cloud storage for cost savings. They also want to minimize changes to their existing file-sharing workflows and applications. Which AWS Storage Gateway type BEST addresses these requirements?


a) Amazon S3 File Gateway

b) Volume Gateway in Cached mode

c) Volume Gateway in Stored mode

d) Tape Gateway

Correct: A