# AWS Lambda CLF-C02 Practice Questions

## Section 1: CLF-C02 Practice Questions (5 questions)

**Question 1:**
A company wants to process images automatically whenever they are uploaded to an Amazon S3 bucket. The processing should happen without managing any servers and only when images are uploaded. Which AWS service combination would be most appropriate for this use case?

A) Amazon EC2 with Auto Scaling Groups and Amazon S3
B) AWS Lambda triggered by S3 events and Amazon S3
C) Amazon ECS with Fargate and Amazon S3
D) AWS Batch with Amazon S3

**Question 2:**
What is the maximum execution time limit for an AWS Lambda function?

A) 5 minutes
B) 15 minutes
C) 30 minutes
D) 1 hour

**Question 3:**
A startup is building a web application that experiences unpredictable traffic patterns, ranging from zero requests to thousands of requests per minute. They want to minimize costs and avoid managing infrastructure. Which compute service would be most cost-effective for their API backend?

A) Amazon EC2 Reserved Instances
B) Amazon EC2 Spot Instances
C) AWS Lambda
D) Amazon ECS on EC2

**Question 4:**
How does AWS Lambda pricing work?

A) Fixed monthly fee regardless of usage
B) Pay per hour for provisioned capacity
C) Pay per request and compute time consumed
D) Pay only for data transfer costs

**Question 5:**
A company needs to run a function every day at 2 AM to generate daily reports. The function takes about 3 minutes to complete and doesn't require any servers to be running continuously. Which AWS service would be the most appropriate and cost-effective solution?

A) Amazon EC2 instance running 24/7
B) AWS Lambda triggered by Amazon CloudWatch Events
C) Amazon ECS task running continuously
D) AWS Batch job running on a dedicated EC2 instance

---

## Section 2: Answers and Justifications

**Question 1: Correct Answer - B) AWS Lambda triggered by S3 events and Amazon S3**

**Justification:**
- **Why B is correct:** AWS Lambda is designed for event-driven, serverless computing. S3 can directly trigger Lambda functions when objects are uploaded, making this the perfect serverless solution. Lambda automatically scales to handle multiple uploads simultaneously without any server management. This is a classic Lambda use case that demonstrates the service's core value proposition.

- **Why A is wrong:** EC2 with Auto Scaling requires managing servers, configuring scaling policies, and would be running continuously even when no images are being uploaded. This is inefficient, costly, and goes against the requirement of "without managing any servers."

- **Why C is wrong:** While ECS with Fargate is serverless for containers, it's more complex than needed for simple image processing. It doesn't have the same seamless, native S3 event integration as Lambda, and would require additional configuration for event handling.

- **Why D is wrong:** AWS Batch is designed for large-scale batch processing jobs that run for extended periods, not real-time event-driven processing of individual file uploads. It's overkill for this use case and doesn't provide the immediate response needed.

**Question 2: Correct Answer - B) 15 minutes**

**Justification:**
- **Why B is correct:** AWS Lambda has a maximum execution timeout of 15 minutes (900 seconds). This is a fundamental service limit that CLF-C02 candidates must know, as it determines whether Lambda is suitable for specific workloads.

- **Why A is wrong:** 5 minutes was the previous limit for Lambda functions before AWS increased it. This is outdated information that might appear on practice tests to test current knowledge.

- **Why C is wrong:** 30 minutes exceeds Lambda's maximum execution time limit. Functions requiring longer execution times would need alternative services.

- **Why D is wrong:** 1 hour far exceeds Lambda's capabilities. For longer-running tasks, other services like ECS, EC2, or AWS Batch would be more appropriate choices.

**Question 3: Correct Answer - C) AWS Lambda**

**Justification:**
- **Why C is correct:** Lambda is ideal for unpredictable traffic patterns because it automatically scales from zero to thousands of concurrent executions based on demand. Its pay-per-use model means you only pay when requests are being processed, making it extremely cost-effective for variable workloads. There's no infrastructure to manage, and it can handle sudden traffic spikes without pre-provisioning.

- **Why A is wrong:** Reserved Instances require upfront commitment and are cost-effective only for predictable, steady workloads running 24/7. They would be wasteful for unpredictable traffic since you'd pay for unused capacity during low-traffic periods.

- **Why B is wrong:** While Spot Instances are cheaper than On-Demand, they can be terminated unexpectedly when AWS needs the capacity back. They still require managing infrastructure, capacity planning, and aren't suitable for unpredictable web application traffic.

- **Why D is wrong:** ECS on EC2 still requires managing underlying EC2 instances, capacity planning, and scaling configurations. You'd pay for the EC2 instances even during periods of no traffic, making it less cost-effective than Lambda's pay-per-use model.

**Question 4: Correct Answer - C) Pay per request and compute time consumed**

**Justification:**
- **Why C is correct:** Lambda uses a pay-per-use pricing model with two main components: 
  1. Number of requests ($0.20 per 1 million requests after the free tier)
  2. Compute time measured in GB-seconds (based on memory allocation and actual execution duration)
  This aligns perfectly with Lambda's serverless nature where you only pay for what you actually use.

- **Why A is wrong:** Lambda doesn't have fixed monthly fees; it's entirely usage-based. Fixed fees would contradict the serverless pay-per-use model that makes Lambda attractive for variable workloads.

- **Why B is wrong:** This describes traditional EC2 pricing where you pay for provisioned capacity regardless of utilization. Lambda doesn't require provisioning capacity in advance.

- **Why D is wrong:** While data transfer costs may apply for Lambda functions that transfer data outside AWS, the primary Lambda charges are for requests and compute time. Data transfer is not the main pricing component.

**Question 5: Correct Answer - B) AWS Lambda triggered by Amazon CloudWatch Events**

**Justification:**
- **Why B is correct:** Lambda with CloudWatch Events (now called Amazon EventBridge) is perfect for scheduled tasks. You can create a cron-like schedule (e.g., `cron(0 2 * * ? *)`) to trigger the function daily at 2 AM. Since the task runs only once per day for 3 minutes, Lambda's pay-per-use model is extremely cost-effective. There's no infrastructure to manage, no servers running idle, and automatic scaling if needed.

- **Why A is wrong:** Running an EC2 instance 24/7 for a 3-minute daily task is extremely wasteful and expensive. You'd pay for 1,437 minutes of unused time daily (99.8% waste). This violates cost optimization principles fundamental to cloud computing.

- **Why C is wrong:** ECS tasks running continuously would also be wasteful for a task that only needs to run 3 minutes per day. You'd still be paying for compute resources that sit idle 99.8% of the time.

- **Why D is wrong:** AWS Batch with a dedicated EC2 instance involves unnecessary complexity and ongoing costs for a simple scheduled task. Batch is better suited for large-scale, compute-intensive jobs that require significant resources and coordination.
