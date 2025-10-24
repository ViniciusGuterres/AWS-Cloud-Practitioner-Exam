# AWS ECS CLF-C02 Practice Questions

## Section 1: CLF-C02 Practice Questions (5 questions)

**Question 1:**
A company wants to run containerized applications on AWS without managing the underlying infrastructure. They need the containers to automatically scale based on demand and integrate with other AWS services. Which AWS service would be most appropriate?

A) Amazon EC2 with Docker installed
B) AWS Lambda with container images
C) Amazon ECS with Fargate launch type
D) Amazon EKS with self-managed nodes

**Question 2:**
What are the two main launch types available in Amazon ECS?

A) On-Demand and Reserved
B) EC2 and Fargate
C) Standard and Spot
D) Public and Private

**Question 3:**
A development team needs to deploy a web application that consists of multiple containers (web server, database, cache) that need to work together. In Amazon ECS, what component would define how these containers should be configured and deployed together?

A) ECS Cluster
B) ECS Service
C) ECS Task Definition
D) ECS Container Instance

**Question 4:**
What is the primary difference between the EC2 launch type and Fargate launch type in Amazon ECS?

A) EC2 launch type is more expensive than Fargate
B) Fargate launch type requires you to manage EC2 instances, while EC2 launch type is serverless
C) EC2 launch type requires you to manage EC2 instances, while Fargate launch type is serverless
D) There is no functional difference between the two launch types

**Question 5:**
A company is running a web application on Amazon ECS and wants to ensure that exactly 5 copies of their application are always running and healthy. If one container fails, it should be automatically replaced. Which ECS component provides this functionality?

A) ECS Task Definition
B) ECS Service
C) ECS Cluster
D) ECS Container Agent

---

## Section 2: Answers and Justifications

**Question 1: Correct Answer - C) Amazon ECS with Fargate launch type**

**Justification:**
- **Why C is correct:** Amazon ECS (Elastic Container Service) with Fargate launch type provides a fully managed container orchestration service where AWS handles all the underlying infrastructure. Fargate eliminates the need to provision, configure, or scale clusters of virtual machines. It automatically scales containers based on demand and integrates seamlessly with other AWS services like ALB, CloudWatch, and IAM. This perfectly matches the requirement of running containerized applications without managing infrastructure.

- **Why A is wrong:** EC2 with Docker requires managing the underlying EC2 instances, including patching, scaling, and maintenance. This doesn't meet the requirement of "without managing the underlying infrastructure."

- **Why B is wrong:** While Lambda supports container images, it's designed for short-running, event-driven functions with a 15-minute execution limit. It's not suitable for long-running containerized applications that need continuous availability.

- **Why D is wrong:** EKS (Elastic Kubernetes Service) with self-managed nodes requires managing the worker nodes (EC2 instances), which contradicts the requirement of not managing underlying infrastructure. Additionally, EKS is more complex than needed for basic container orchestration.

**Question 2: Correct Answer - B) EC2 and Fargate**

**Justification:**
- **Why B is correct:** Amazon ECS offers two launch types: EC2 launch type (where you manage EC2 instances that host your containers) and Fargate launch type (where AWS manages the underlying infrastructure in a serverless manner). This is fundamental ECS knowledge required for the CLF-C02 exam.

- **Why A is wrong:** On-Demand and Reserved refer to EC2 pricing models, not ECS launch types. While you can use Reserved Instances with ECS EC2 launch type, these are not the launch type categories.

- **Why C is wrong:** Standard and Spot refer to EC2 instance types/pricing models. While you can use Spot instances with ECS, these are not the primary launch type classifications for ECS.

- **Why D is wrong:** Public and Private refer to network configurations or repository types (like ECR), not ECS launch types.

**Question 3: Correct Answer - C) ECS Task Definition**

**Justification:**
- **Why C is correct:** An ECS Task Definition is a blueprint that describes how containers should run together. It specifies which Docker images to use, CPU and memory requirements, networking configuration, port mappings, environment variables, and how containers are linked together. For a multi-container application (web server, database, cache), the task definition defines all containers and their relationships in a single JSON document.

- **Why A is wrong:** An ECS Cluster is a logical grouping of compute resources (EC2 instances or Fargate capacity) where tasks run. It doesn't define how containers are configured or how they work together.

- **Why B is wrong:** An ECS Service ensures a specified number of task instances are running and healthy, and can integrate with load balancers. However, it doesn't define the container configuration - it uses a task definition for that purpose.

- **Why D is wrong:** ECS Container Instance refers to an EC2 instance that's part of an ECS cluster (only relevant for EC2 launch type). It doesn't define container configurations or relationships.

**Question 4: Correct Answer - C) EC2 launch type requires you to manage EC2 instances, while Fargate launch type is serverless**

**Justification:**
- **Why C is correct:** This accurately describes the fundamental difference between the two launch types. With EC2 launch type, you provision and manage EC2 instances that join your ECS cluster - you're responsible for patching, scaling, and maintaining these instances. With Fargate launch type, AWS manages all the underlying infrastructure in a serverless model - you only define your container requirements and AWS handles the rest.

- **Why A is wrong:** Pricing depends on usage patterns and requirements. Fargate can be more expensive for consistent, high-utilization workloads, while EC2 launch type might be more expensive for variable workloads due to unused capacity. The cost difference is not the primary distinguishing factor.

- **Why B is wrong:** This reverses the correct relationship. Fargate is the serverless option, while EC2 launch type requires managing instances.

- **Why D is wrong:** There are significant functional and operational differences between the launch types, particularly in terms of infrastructure management responsibilities and operational overhead.

**Question 5: Correct Answer - B) ECS Service**

**Justification:**
- **Why B is correct:** An ECS Service is responsible for maintaining a desired number of running tasks (containers) and ensuring they remain healthy. It monitors the health of tasks and automatically replaces failed tasks to maintain the desired count. Services can also integrate with load balancers to distribute traffic and provide service discovery. The scenario describes exactly what an ECS Service does - maintain exactly 5 running copies and replace failed containers.

- **Why A is wrong:** A Task Definition is a blueprint that describes how containers should be configured (image, CPU, memory, etc.), but it doesn't manage the lifecycle or ensure a specific number of running instances. It's a static configuration template.

- **Why C is wrong:** An ECS Cluster is the underlying compute infrastructure where tasks run, but it doesn't manage the desired state or health of specific applications. It's just the resource pool.

- **Why D is wrong:** The ECS Container Agent runs on EC2 instances (in EC2 launch type) and communicates with the ECS service, but it doesn't manage application-level desired state or automatic replacement of failed containers. It's a low-level infrastructure component.
