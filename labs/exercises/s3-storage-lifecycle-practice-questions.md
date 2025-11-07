# AWS CLF-C02 Practice Questions: S3 Storage Classes and Lifecycle

## Section 1: CLF-C02 Practice Questions

### Question 1
A company needs to store backup files that are accessed once per year for compliance purposes. Which Amazon S3 storage class would be the MOST cost-effective option?

A) S3 Standard
B) S3 Standard-Infrequent Access (S3 Standard-IA)
C) S3 Glacier Flexible Retrieval
D) S3 Intelligent-Tiering

### Question 2
Which of the following are benefits of using S3 Lifecycle policies? (Select TWO)

A) Automatically encrypt objects after a specified time period
B) Reduce storage costs by transitioning objects to cheaper storage classes
C) Automatically delete objects after a specified retention period
D) Increase data transfer speeds for frequently accessed objects
E) Provide real-time monitoring of object access patterns

### Question 3
A startup company stores user-uploaded photos that are frequently accessed for the first 30 days, then rarely accessed afterward. What is the MOST cost-effective S3 storage strategy?

A) Store all photos in S3 Standard permanently
B) Use S3 Intelligent-Tiering for automatic optimization
C) Manually move photos to S3 Glacier after 30 days
D) Store all photos in S3 One Zone-Infrequent Access

### Question 4
What is the minimum storage duration for objects stored in S3 Standard-Infrequent Access (S3 Standard-IA)?

A) 7 days
B) 30 days
C) 90 days
D) 180 days

### Question 5
A company wants to archive log files that may need to be retrieved within 12 hours for legal investigations. Which S3 storage class meets this requirement at the lowest cost?

A) S3 Standard
B) S3 Glacier Instant Retrieval
C) S3 Glacier Flexible Retrieval
D) S3 Glacier Deep Archive

### Question 6
Which statement about S3 Intelligent-Tiering is CORRECT?

A) It requires manual configuration of lifecycle rules
B) It automatically moves objects between access tiers based on usage patterns
C) It only works with objects larger than 128 KB
D) It charges retrieval fees for all object access

### Question 7
A media company needs to store video files that are accessed unpredictably. Sometimes files are accessed daily, other times they sit unused for months. Which S3 storage class would be MOST appropriate?

A) S3 Standard
B) S3 Standard-IA
C) S3 Intelligent-Tiering
D) S3 Glacier Flexible Retrieval

### Question 8
What happens when you delete an object from S3 Glacier Flexible Retrieval before the minimum storage duration?

A) The deletion is blocked and returns an error
B) You are charged for the remaining minimum storage duration
C) The object is moved to S3 Standard for the remaining duration
D) AWS automatically extends the storage duration

### Question 9
Which S3 storage class provides the FASTEST retrieval time for archived data?

A) S3 Glacier Flexible Retrieval (Standard retrieval)
B) S3 Glacier Flexible Retrieval (Expedited retrieval)
C) S3 Glacier Instant Retrieval
D) S3 Glacier Deep Archive

### Question 10
A company wants to automatically transition objects from S3 Standard to S3 Standard-IA after 30 days, then to S3 Glacier Flexible Retrieval after 90 days. What AWS feature should they use?

A) S3 Cross-Region Replication
B) S3 Lifecycle configuration
C) S3 Transfer Acceleration
D) S3 Event Notifications

---

## Section 2: Answers and Justifications

### Question 1: Answer C - S3 Glacier Flexible Retrieval

**Correct Answer Justification:**
S3 Glacier Flexible Retrieval is designed for long-term archival of data that is accessed infrequently (once or twice per year). It offers significant cost savings compared to other storage classes for this use case, with retrieval times of minutes to hours.

**Why other options are incorrect:**
- A) S3 Standard: Most expensive option, designed for frequently accessed data
- B) S3 Standard-IA: More expensive than Glacier for rarely accessed data, designed for monthly access
- D) S3 Intelligent-Tiering: Has monitoring fees and is better for unpredictable access patterns

### Question 2: Answer B and C

**Correct Answers Justification:**
- B) Lifecycle policies can automatically transition objects to cheaper storage classes based on age
- C) Lifecycle policies can automatically delete objects after specified retention periods

**Why other options are incorrect:**
- A) Encryption is configured separately, not through lifecycle policies
- D) Lifecycle policies don't affect transfer speeds
- E) Monitoring is handled by CloudWatch, not lifecycle policies

### Question 3: Answer B - S3 Intelligent-Tiering

**Correct Answer Justification:**
S3 Intelligent-Tiering automatically moves objects between frequent and infrequent access tiers based on usage patterns, making it ideal for data with changing access patterns without operational overhead.

**Why other options are incorrect:**
- A) S3 Standard: Expensive for data that becomes infrequently accessed
- C) Manual management: Adds operational overhead and potential for human error
- D) S3 One Zone-IA: Lower durability and doesn't address the access pattern change

### Question 4: Answer B - 30 days

**Correct Answer Justification:**
S3 Standard-IA has a minimum storage duration of 30 days. Objects deleted before 30 days are charged for the full 30-day period.

**Why other options are incorrect:**
- A) 7 days: This is the minimum for S3 Intelligent-Tiering
- C) 90 days: This is the minimum for S3 Glacier Flexible Retrieval
- D) 180 days: This is the minimum for S3 Glacier Deep Archive

### Question 5: Answer C - S3 Glacier Flexible Retrieval

**Correct Answer Justification:**
S3 Glacier Flexible Retrieval can retrieve data within 1-5 minutes (expedited), 3-5 hours (standard), or 5-12 hours (bulk), meeting the 12-hour requirement at the lowest archival cost.

**Why other options are incorrect:**
- A) S3 Standard: Much more expensive for archival use case
- B) S3 Glacier Instant Retrieval: More expensive than Flexible Retrieval, designed for millisecond access
- D) S3 Glacier Deep Archive: Retrieval takes 12+ hours, may not meet the requirement

### Question 6: Answer B - It automatically moves objects between access tiers based on usage patterns

**Correct Answer Justification:**
S3 Intelligent-Tiering monitors access patterns and automatically moves objects between frequent and infrequent access tiers without performance impact or operational overhead.

**Why other options are incorrect:**
- A) It works automatically without manual lifecycle rules
- C) It works with objects 128 KB and larger, but this isn't the main feature
- D) There are no retrieval fees for the frequent access tier

### Question 7: Answer C - S3 Intelligent-Tiering

**Correct Answer Justification:**
S3 Intelligent-Tiering is specifically designed for data with unknown or changing access patterns, automatically optimizing costs without operational overhead.

**Why other options are incorrect:**
- A) S3 Standard: Expensive when files aren't accessed for months
- B) S3 Standard-IA: Not optimal for frequently accessed files due to retrieval charges
- D) S3 Glacier: Not suitable for daily access due to retrieval times and costs

### Question 8: Answer B - You are charged for the remaining minimum storage duration

**Correct Answer Justification:**
When objects are deleted before meeting the minimum storage duration, AWS charges for the remaining time to meet the minimum commitment.

**Why other options are incorrect:**
- A) Deletion is allowed, not blocked
- C) Objects aren't moved to other storage classes
- D) AWS doesn't extend storage duration

### Question 9: Answer C - S3 Glacier Instant Retrieval

**Correct Answer Justification:**
S3 Glacier Instant Retrieval provides millisecond retrieval times, the fastest among all Glacier storage classes.

**Why other options are incorrect:**
- A) Standard retrieval: 3-5 hours
- B) Expedited retrieval: 1-5 minutes
- D) Deep Archive: 12+ hours

### Question 10: Answer B - S3 Lifecycle configuration

**Correct Answer Justification:**
S3 Lifecycle configuration allows you to define rules for automatically transitioning objects between storage classes based on age or other criteria.

**Why other options are incorrect:**
- A) Cross-Region Replication: For copying objects across regions
- C) Transfer Acceleration: For faster uploads
- D) Event Notifications: For triggering actions on object events, not automatic transitions
