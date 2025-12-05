# AWS EKS (Elastic Kubernetes Service)

## What is AWS EKS?

AWS Elastic Kubernetes Service (EKS) is a **fully managed Kubernetes service** that makes it easy to deploy, manage, and scale containerized applications using Kubernetes on AWS. EKS runs upstream Kubernetes and is certified Kubernetes conformant, ensuring compatibility with existing Kubernetes tooling.

**Key Concept:** EKS provides a managed Kubernetes control plane, eliminating the need to install, operate, and maintain your own Kubernetes control plane or nodes. AWS handles the availability, scalability, and security of the Kubernetes API servers and etcd persistence layer.

## Core Components

### 1. Managed Control Plane
**Definition:** AWS-managed Kubernetes API servers and etcd database that runs across multiple AZs

**Control Plane Features:**
- **High availability** - Runs across multiple Availability Zones
- **Automatic scaling** - Scales API servers based on load
- **Security patches** - AWS handles security updates and patches
- **Version management** - Managed Kubernetes version upgrades

### 2. Worker Nodes
**Definition:** EC2 instances or Fargate that run your containerized applications (pods)

**Node Types:**
- **Managed node groups** - AWS-managed EC2 instances with automatic updates
- **Self-managed nodes** - You manage EC2 instances directly
- **Fargate** - Serverless compute for pods without managing nodes
- **Spot instances** - Cost-optimized compute using EC2 Spot instances

### 3. Networking
**Definition:** VPC-native networking that integrates with AWS networking services

**Networking Components:**
- **VPC integration** - Clusters run within your VPC
- **Pod networking** - Each pod gets a VPC IP address
- **Security groups** - Control traffic to and from pods
- **Load balancers** - Integrate with ALB and NLB for ingress

### 4. Add-ons
**Definition:** Operational software that provides key functionality for Kubernetes clusters

**Common Add-ons:**
- **VPC CNI** - Networking plugin for pod IP assignment
- **CoreDNS** - DNS resolution within the cluster
- **kube-proxy** - Network proxy for Kubernetes services
- **AWS Load Balancer Controller** - Manage ALB and NLB from Kubernetes

## Key Features ⭐ **EXAM FOCUS**

### Fully Managed Kubernetes
- **No control plane management** - AWS handles Kubernetes masters
- **Automatic updates** - Managed security patches and version upgrades
- **High availability** - Multi-AZ control plane deployment
- **Kubernetes conformant** - Compatible with standard Kubernetes tools

### AWS Integration
- **IAM integration** - Use AWS IAM for authentication and authorization
- **VPC networking** - Native VPC integration with security groups
- **Load balancer integration** - Automatic ALB and NLB provisioning
- **CloudWatch monitoring** - Built-in logging and monitoring

### Flexible Compute Options
- **Multiple node types** - Managed nodes, self-managed, or Fargate
- **Instance variety** - Support for all EC2 instance types
- **Spot instances** - Cost optimization with EC2 Spot
- **ARM64 support** - Graviton processors for better price-performance

## Node Group Types Comparison

### Managed Node Groups
**When to Use:**
- Want AWS to handle node lifecycle management
- Need automatic security updates and patches
- Prefer simplified cluster operations
- Want integration with AWS services

**Characteristics:**
- **Automatic updates** - AWS handles AMI updates and node replacement
- **Scaling** - Integrated with Cluster Autoscaler
- **Launch templates** - Customizable EC2 configurations
- **Spot support** - Mix On-Demand and Spot instances

### Self-Managed Nodes
**When to Use:**
- Need full control over node configuration
- Require custom AMIs or specialized configurations
- Want to manage update schedules manually
- Need specific instance types or configurations

**Characteristics:**
- **Full control** - Complete control over EC2 instances
- **Custom AMIs** - Use custom Amazon Machine Images
- **Manual updates** - You handle security patches and updates
- **Flexible configuration** - Any EC2 instance type or configuration

### Fargate
**When to Use:**
- Want serverless pod execution
- Don't want to manage any infrastructure
- Have variable or unpredictable workloads
- Need to focus on applications, not infrastructure

**Characteristics:**
- **Serverless** - No EC2 instances to manage
- **Pay-per-pod** - Pay only for running pods
- **Automatic scaling** - AWS handles infrastructure scaling
- **Simplified operations** - Focus on Kubernetes, not nodes

## Usage Examples

### Example 1: Basic Deployment Manifest
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
  namespace: default
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web-app
  template:
    metadata:
      labels:
        app: web-app
    spec:
      containers:
      - name: web-server
        image: nginx:latest
        ports:
        - containerPort: 80
        resources:
          requests:
            memory: "128Mi"
            cpu: "100m"
          limits:
            memory: "256Mi"
            cpu: "200m"
---
apiVersion: v1
kind: Service
metadata:
  name: web-app-service
spec:
  selector:
    app: web-app
  ports:
  - port: 80
    targetPort: 80
  type: LoadBalancer
```

### Example 2: Fargate Profile Configuration
```yaml
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig

metadata:
  name: my-cluster
  region: us-east-1

fargateProfiles:
  - name: default
    selectors:
      - namespace: default
      - namespace: kube-system
        labels:
          k8s-app: kube-dns
  - name: production
    selectors:
      - namespace: production
    subnets:
      - subnet-12345
      - subnet-67890
```

### Example 3: Managed Node Group Configuration
```yaml
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig

metadata:
  name: my-cluster
  region: us-east-1

managedNodeGroups:
  - name: worker-nodes
    instanceType: m5.large
    minSize: 1
    maxSize: 10
    desiredCapacity: 3
    volumeSize: 20
    ssh:
      allow: true
    labels:
      role: worker
    tags:
      Environment: production
    iam:
      withAddonPolicies:
        autoScaler: true
        cloudWatch: true
```

## Kubernetes Concepts for CLF-C02

### Pods
- **Smallest deployable unit** - Contains one or more containers
- **Shared resources** - Containers share network and storage
- **Ephemeral** - Pods can be created, destroyed, and recreated
- **IP address** - Each pod gets a unique IP address in VPC

### Services
- **Stable networking** - Provide consistent access to pods
- **Load balancing** - Distribute traffic across multiple pods
- **Service discovery** - DNS-based service discovery
- **Types** - ClusterIP, NodePort, LoadBalancer, ExternalName

### Deployments
- **Declarative updates** - Describe desired state for pods
- **Rolling updates** - Update applications without downtime
- **Rollback capability** - Revert to previous versions
- **Scaling** - Increase or decrease number of replicas

### Namespaces
- **Resource isolation** - Logical separation of resources
- **Multi-tenancy** - Multiple teams or environments
- **Resource quotas** - Limit resource usage per namespace
- **RBAC** - Role-based access control per namespace

## Pricing ⭐ **EXAM FOCUS**

### EKS Control Plane Pricing
- **Cluster cost** - $0.10 per hour per cluster
- **Monthly cost** - Approximately $73 per cluster per month
- **No additional charges** - For control plane API calls or etcd storage
- **Multi-AZ included** - High availability at no extra cost

### Worker Node Pricing
- **EC2 instances** - Standard EC2 pricing for managed/self-managed nodes
- **Fargate** - Pay per vCPU and memory for pods
- **Spot instances** - Up to 90% savings with EC2 Spot
- **Data transfer** - Standard AWS data transfer charges

### Example Cost Calculation
```
EKS Cluster with Managed Node Group:

Control Plane: $0.10 × 24 × 30 = $73/month
Worker Nodes: 3 × m5.large × $0.096 × 24 × 30 = $207.36/month
Total: $280.36/month

EKS with Fargate (example workload):
Control Plane: $73/month
Fargate Pods: Variable based on pod resource allocation
```

## Integration with Other Services

### AWS Load Balancer Controller
- **Application Load Balancer** - Layer 7 load balancing for HTTP/HTTPS
- **Network Load Balancer** - Layer 4 load balancing for TCP/UDP
- **Ingress controller** - Kubernetes-native load balancer management
- **Target group binding** - Direct pod IP registration

### Amazon ECR
- **Container registry** - Store and manage container images
- **Image scanning** - Vulnerability scanning for container images
- **Lifecycle policies** - Automatic image cleanup
- **IAM integration** - Fine-grained access control

### AWS IAM
- **Service accounts** - Map Kubernetes service accounts to IAM roles
- **RBAC integration** - Use AWS IAM for Kubernetes authorization
- **Pod-level permissions** - Fine-grained access control for applications
- **Cross-service access** - Access other AWS services from pods

### Amazon CloudWatch
- **Container Insights** - Detailed metrics and logs for containers
- **Cluster monitoring** - Monitor cluster health and performance
- **Application logs** - Centralized logging for applications
- **Custom metrics** - Application-specific monitoring

## Best Practices

### Cluster Security
1. **Network policies** - Implement Kubernetes network policies
2. **RBAC** - Use role-based access control
3. **Pod security** - Implement pod security standards
4. **Image scanning** - Scan container images for vulnerabilities

### Cost Optimization
1. **Right-size nodes** - Choose appropriate instance types
2. **Use Spot instances** - For fault-tolerant workloads
3. **Cluster Autoscaler** - Automatically scale nodes based on demand
4. **Fargate for variable workloads** - Pay only for running pods

### Performance Optimization
1. **Resource requests/limits** - Set appropriate CPU and memory limits
2. **Node placement** - Use node selectors and affinity rules
3. **Horizontal Pod Autoscaler** - Scale pods based on metrics
4. **Vertical Pod Autoscaler** - Optimize resource allocation

### Operational Excellence
1. **Monitoring** - Implement comprehensive monitoring and alerting
2. **Logging** - Centralize logs with CloudWatch or third-party tools
3. **Backup** - Regular backups of cluster state and data
4. **Disaster recovery** - Plan for cluster recovery scenarios

## Common Use Cases ⭐ **EXAM FOCUS**

### 1. Microservices Architecture
- **Service decomposition** - Break monoliths into smaller services
- **Independent scaling** - Scale services based on individual demand
- **Technology diversity** - Use different technologies per service
- **Fault isolation** - Isolate failures to individual services

### 2. Batch Processing and ML Workloads
- **Job scheduling** - Run batch jobs using Kubernetes Jobs
- **Machine learning** - Training and inference workloads
- **Data processing** - ETL pipelines and data transformation
- **Scientific computing** - High-performance computing workloads

### 3. Web Applications and APIs
- **Scalable web apps** - Auto-scaling web applications
- **API gateways** - Microservices-based API platforms
- **Content management** - Containerized CMS platforms
- **E-commerce platforms** - Scalable online retail applications

### 4. DevOps and CI/CD
- **GitOps workflows** - Infrastructure and application deployment
- **Multi-environment management** - Dev, staging, and production clusters
- **Blue-green deployments** - Zero-downtime deployment strategies
- **Canary releases** - Gradual rollout of new application versions

## Limitations and Considerations

### Kubernetes Complexity
- **Learning curve** - Requires Kubernetes knowledge and expertise
- **Operational overhead** - More complex than simple container services
- **Resource management** - Need to understand resource allocation
- **Troubleshooting** - Debugging distributed systems can be complex

### AWS-Specific Limitations
- **Control plane access** - Limited access to Kubernetes masters
- **Version lag** - EKS may lag behind latest Kubernetes releases
- **Add-on dependencies** - Some features require specific AWS add-ons
- **Regional availability** - Not available in all AWS regions

### Cost Considerations
- **Always-on control plane** - $73/month minimum cost per cluster
- **Resource overhead** - Kubernetes system pods consume resources
- **Complexity tax** - May be overkill for simple applications
- **Monitoring costs** - Additional costs for comprehensive monitoring

## Key Exam Points

✅ **Managed Kubernetes** - AWS handles control plane management  
✅ **Multi-AZ control plane** - High availability across availability zones  
✅ **Three node types** - Managed, self-managed, and Fargate  
✅ **VPC integration** - Native VPC networking with security groups  
✅ **IAM integration** - Use AWS IAM for authentication and authorization  
✅ **$0.10/hour** - Control plane pricing per cluster  
✅ **Kubernetes conformant** - Compatible with standard Kubernetes tools  

## Common Exam Scenarios

**Scenario:** "Need to run Kubernetes workloads without managing control plane"  
**Answer:** Use Amazon EKS for managed Kubernetes control plane

**Scenario:** "Want to run Kubernetes pods without managing any infrastructure"  
**Answer:** Use EKS with Fargate profiles for serverless pod execution

**Scenario:** "Need to integrate Kubernetes with AWS services like IAM and VPC"  
**Answer:** EKS provides native AWS integration for security and networking

**Scenario:** "Application requires automatic scaling based on demand"  
**Answer:** Use EKS with Horizontal Pod Autoscaler and Cluster Autoscaler

**Scenario:** "Need to run batch processing jobs on Kubernetes"  
**Answer:** Use EKS with Kubernetes Jobs and CronJobs

## Practice Questions

**Q: What is Amazon EKS?**  
A: A fully managed Kubernetes service that runs the Kubernetes control plane

**Q: What are the three types of worker nodes supported by EKS?**  
A: Managed node groups, self-managed nodes, and Fargate

**Q: How much does the EKS control plane cost?**  
A: $0.10 per hour per cluster (approximately $73 per month)

**Q: What is the benefit of using Fargate with EKS?**  
A: Serverless pod execution without managing any EC2 instances

**Q: How does EKS integrate with AWS networking?**  
A: EKS runs in your VPC and each pod gets a VPC IP address

**Q: What AWS service provides container image storage for EKS?**  
A: Amazon ECR (Elastic Container Registry)

**Q: How does EKS handle high availability?**  
A: The control plane runs across multiple Availability Zones automatically

**Q: What is required to access other AWS services from EKS pods?**  
A: IAM roles for service accounts (IRSA) to provide appropriate permissions
