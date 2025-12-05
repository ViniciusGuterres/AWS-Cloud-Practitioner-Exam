# AWS ECR (Elastic Container Registry)

## What is AWS ECR?

AWS Elastic Container Registry (ECR) is a **fully managed container registry service** that makes it easy to store, manage, and deploy Docker container images. ECR is integrated with Amazon ECS, EKS, and AWS Fargate, simplifying your development to production workflow.

**Key Concept:** ECR provides a secure, scalable, and reliable registry to store your container images. It eliminates the need to operate your own container repositories or worry about scaling the underlying infrastructure.

## Core Components

### 1. Repositories
**Definition:** Named collections where you store your Docker images

**Repository Features:**
- **Image storage** - Store multiple versions of container images
- **Tagging system** - Organize images with meaningful tags
- **Lifecycle policies** - Automatically manage image retention
- **Access control** - Fine-grained permissions per repository

### 2. Images
**Definition:** Docker container images stored in repositories

**Image Characteristics:**
- **Immutable tags** - Optional immutable tagging for security
- **Multi-architecture** - Support for x86_64 and ARM64 images
- **Layer deduplication** - Efficient storage through layer sharing
- **Compression** - Automatic image compression for faster transfers

### 3. Registry
**Definition:** The ECR service endpoint where repositories are hosted

**Registry Types:**
- **Private registry** - Default, requires authentication
- **Public registry** - Amazon ECR Public for open-source images
- **Cross-region replication** - Replicate images across regions
- **Cross-account access** - Share images between AWS accounts

## Key Features ⭐ **EXAM FOCUS**

### Fully Managed Service
- **No infrastructure management** - AWS handles all underlying infrastructure
- **High availability** - Built-in redundancy and fault tolerance
- **Automatic scaling** - Scales to handle any number of images
- **Integrated security** - Built-in encryption and access controls

### Security and Compliance
- **Encryption at rest** - Images encrypted using AWS KMS
- **Encryption in transit** - HTTPS for all API calls and image transfers
- **Vulnerability scanning** - Automated security scanning of images
- **IAM integration** - Fine-grained access control using AWS IAM

### AWS Service Integration
- **ECS integration** - Native integration with Amazon ECS
- **EKS integration** - Seamless integration with Amazon EKS
- **Fargate support** - Works with AWS Fargate out of the box
- **CodeBuild integration** - Build and push images from CI/CD pipelines

## ECR Public vs Private

### ECR Private (Default)
**When to Use:**
- Storing proprietary or internal applications
- Need fine-grained access control
- Require integration with AWS services
- Want to keep images within your AWS account

**Characteristics:**
- **Authentication required** - Must authenticate to pull images
- **IAM-based access** - Use AWS IAM for access control
- **Cross-account sharing** - Share with specific AWS accounts
- **Pricing** - Pay for storage and data transfer

### ECR Public
**When to Use:**
- Sharing open-source container images
- Public distribution of applications
- Community contributions
- Reducing bandwidth costs for public images

**Characteristics:**
- **No authentication** - Anyone can pull public images
- **Global distribution** - Available worldwide without AWS account
- **Free tier** - Generous free tier for public repositories
- **Bandwidth optimization** - Reduced data transfer costs

## Usage Examples

### Example 1: Basic Docker Commands
```bash
# Authenticate Docker to ECR
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 123456789012.dkr.ecr.us-east-1.amazonaws.com

# Tag your image
docker tag my-app:latest 123456789012.dkr.ecr.us-east-1.amazonaws.com/my-app:latest

# Push image to ECR
docker push 123456789012.dkr.ecr.us-east-1.amazonaws.com/my-app:latest

# Pull image from ECR
docker pull 123456789012.dkr.ecr.us-east-1.amazonaws.com/my-app:latest
```

### Example 2: ECS Task Definition with ECR
```json
{
  "family": "web-app",
  "networkMode": "awsvpc",
  "requiresCompatibilities": ["FARGATE"],
  "cpu": "256",
  "memory": "512",
  "executionRoleArn": "arn:aws:iam::123456789012:role/ecsTaskExecutionRole",
  "containerDefinitions": [
    {
      "name": "web-server",
      "image": "123456789012.dkr.ecr.us-east-1.amazonaws.com/my-web-app:v1.2.3",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp"
        }
      ],
      "essential": true,
      "logConfiguration": {
        "logDriver": "awslogs",
        "options": {
          "awslogs-group": "/ecs/web-app",
          "awslogs-region": "us-east-1"
        }
      }
    }
  ]
}
```

### Example 3: Lifecycle Policy
```json
{
  "rules": [
    {
      "rulePriority": 1,
      "description": "Keep last 10 production images",
      "selection": {
        "tagStatus": "tagged",
        "tagPrefixList": ["prod"],
        "countType": "imageCountMoreThan",
        "countNumber": 10
      },
      "action": {
        "type": "expire"
      }
    },
    {
      "rulePriority": 2,
      "description": "Delete untagged images older than 1 day",
      "selection": {
        "tagStatus": "untagged",
        "countType": "sinceImagePushed",
        "countUnit": "days",
        "countNumber": 1
      },
      "action": {
        "type": "expire"
      }
    }
  ]
}
```

## Image Management Features

### Lifecycle Policies
- **Automatic cleanup** - Remove old or unused images automatically
- **Cost optimization** - Reduce storage costs by managing image retention
- **Rule-based** - Define rules based on age, count, or tags
- **Preview mode** - Test policies before applying them

### Image Scanning
- **Vulnerability detection** - Scan for known security vulnerabilities
- **CVE database** - Uses Common Vulnerabilities and Exposures database
- **Scan on push** - Automatically scan images when pushed
- **Scan results** - Detailed reports with severity levels

### Immutable Tags
- **Tag protection** - Prevent overwriting of specific image tags
- **Security enhancement** - Ensure image integrity and traceability
- **Compliance** - Meet regulatory requirements for image management
- **Deployment safety** - Prevent accidental overwrites of production images

## Pricing ⭐ **EXAM FOCUS**

### ECR Private Pricing
- **Storage** - $0.10 per GB per month for images
- **Data transfer** - Standard AWS data transfer rates
- **No additional charges** - No charges for API calls or image layers
- **Free tier** - 500 MB of storage per month for 12 months

### ECR Public Pricing
- **Storage** - 50 GB free per month, then $0.10 per GB
- **Bandwidth** - 500 GB free per month, then $0.09 per GB
- **Anonymous pulls** - Free for public repositories
- **Authenticated pulls** - Free up to limits, then standard rates

### Example Cost Calculation
```
Private ECR Repository:
- 10 GB of images stored: 10 × $0.10 = $1.00/month
- 100 GB data transfer out: 100 × $0.09 = $9.00/month
Total: $10.00/month

Public ECR Repository (within free tier):
- 30 GB storage: Free (under 50 GB limit)
- 200 GB bandwidth: Free (under 500 GB limit)
Total: $0.00/month
```

## Integration with Other Services

### Amazon ECS
- **Native integration** - ECS can pull images directly from ECR
- **Task definitions** - Reference ECR images in task definitions
- **Automatic authentication** - ECS handles ECR authentication
- **Image updates** - Deploy new versions by updating task definitions

### Amazon EKS
- **Kubernetes integration** - Use ECR images in Kubernetes deployments
- **Image pull secrets** - Automatic authentication for private repositories
- **Multi-architecture** - Support for ARM64 and x86_64 images
- **Helm charts** - Store and deploy Helm charts alongside images

### AWS CodeBuild
- **CI/CD integration** - Build and push images in build pipelines
- **Automated builds** - Trigger builds on code changes
- **Multi-stage builds** - Support for complex Docker builds
- **Build caching** - Cache layers for faster builds

### AWS CodePipeline
- **Deployment pipelines** - Automate image deployment workflows
- **Source integration** - Trigger pipelines on image pushes
- **Cross-region deployment** - Deploy images across multiple regions
- **Approval gates** - Manual approval steps for production deployments

## Best Practices

### Security Best Practices
1. **Image scanning** - Enable vulnerability scanning for all repositories
2. **Least privilege access** - Use IAM policies for minimal required access
3. **Immutable tags** - Use immutable tags for production images
4. **Regular updates** - Keep base images updated with security patches

### Cost Optimization
1. **Lifecycle policies** - Implement policies to clean up old images
2. **Image optimization** - Use multi-stage builds to reduce image size
3. **Layer sharing** - Leverage Docker layer caching and sharing
4. **Monitor usage** - Track storage and transfer costs regularly

### Operational Excellence
1. **Tagging strategy** - Use consistent and meaningful image tags
2. **Repository organization** - Organize repositories by application or team
3. **Monitoring** - Set up CloudWatch alarms for repository metrics
4. **Backup strategy** - Consider cross-region replication for critical images

### Performance Optimization
1. **Regional placement** - Store images close to compute resources
2. **Image size** - Optimize images for faster pull times
3. **Parallel pulls** - Use multi-stage builds for parallel layer downloads
4. **Caching strategies** - Implement appropriate caching at build and runtime

## Common Use Cases ⭐ **EXAM FOCUS**

### 1. Application Deployment
- **Microservices** - Store and deploy individual service images
- **Web applications** - Deploy containerized web applications
- **API services** - Manage API backend container images
- **Batch processing** - Store images for batch job processing

### 2. CI/CD Pipelines
- **Automated builds** - Build and store images in CI/CD workflows
- **Testing environments** - Deploy test versions of applications
- **Staging deployments** - Manage staging environment images
- **Production releases** - Store and deploy production-ready images

### 3. Multi-Environment Management
- **Development** - Store development and feature branch images
- **Testing** - Manage test environment specific images
- **Production** - Store stable, production-ready images
- **Disaster recovery** - Cross-region image replication

### 4. Third-Party Integration
- **Vendor images** - Store customized third-party application images
- **Base images** - Manage organization-standard base images
- **Security scanning** - Scan all images for vulnerabilities
- **Compliance** - Meet regulatory requirements for image management

## Security Features

### Encryption
- **Encryption at rest** - All images encrypted using AWS KMS
- **Encryption in transit** - HTTPS for all data transfers
- **Key management** - Use AWS managed or customer managed KMS keys
- **Cross-region encryption** - Maintain encryption during replication

### Access Control
- **IAM integration** - Use AWS IAM for fine-grained access control
- **Resource-based policies** - Repository-level access policies
- **Cross-account access** - Securely share images between accounts
- **Temporary credentials** - Use IAM roles for secure access

### Vulnerability Management
- **Automated scanning** - Continuous vulnerability assessment
- **CVE tracking** - Track Common Vulnerabilities and Exposures
- **Severity classification** - Categorize vulnerabilities by severity
- **Remediation guidance** - Recommendations for fixing vulnerabilities

## Limitations and Considerations

### Service Limits
- **Repository limit** - 10,000 repositories per region per account
- **Image size** - Maximum 10 GB per image layer
- **Lifecycle rules** - Maximum 100 rules per repository
- **API rate limits** - Throttling on API calls during high usage

### Regional Considerations
- **Regional service** - Repositories are region-specific
- **Cross-region access** - Additional latency and data transfer costs
- **Replication** - Manual setup required for cross-region replication
- **Disaster recovery** - Plan for regional outages

### Cost Considerations
- **Storage costs** - Costs accumulate with image storage over time
- **Data transfer** - Charges for pulling images across regions/internet
- **Lifecycle management** - Important for controlling storage costs
- **Public vs private** - Consider cost implications of repository type

## Key Exam Points

✅ **Fully managed** - AWS handles all infrastructure for container registry  
✅ **Private by default** - Requires authentication unless using ECR Public  
✅ **Integrated with ECS/EKS** - Native integration with AWS container services  
✅ **Vulnerability scanning** - Built-in security scanning capabilities  
✅ **Lifecycle policies** - Automatic image cleanup and retention management  
✅ **Encryption** - Images encrypted at rest and in transit  
✅ **IAM integration** - Fine-grained access control using AWS IAM  

## Common Exam Scenarios

**Scenario:** "Need to store Docker images for ECS applications securely"  
**Answer:** Use Amazon ECR private repositories with IAM access control

**Scenario:** "Want to automatically clean up old container images to reduce costs"  
**Answer:** Implement ECR lifecycle policies to automatically delete old images

**Scenario:** "Need to scan container images for security vulnerabilities"  
**Answer:** Enable ECR vulnerability scanning to automatically scan images

**Scenario:** "Application requires sharing container images with another AWS account"  
**Answer:** Use ECR cross-account access policies to share repositories

**Scenario:** "Want to distribute open-source container images publicly"  
**Answer:** Use Amazon ECR Public to share images without authentication

## Practice Questions

**Q: What is Amazon ECR?**  
A: A fully managed container registry service for storing Docker images

**Q: What are the two types of ECR repositories?**  
A: Private repositories (default) and Public repositories

**Q: How are ECR images encrypted?**  
A: Encrypted at rest using AWS KMS and in transit using HTTPS

**Q: What feature helps reduce ECR storage costs?**  
A: Lifecycle policies that automatically delete old or unused images

**Q: Which AWS services integrate natively with ECR?**  
A: Amazon ECS, Amazon EKS, and AWS Fargate

**Q: What security feature does ECR provide for container images?**  
A: Vulnerability scanning to detect security issues in images

**Q: How does ECR pricing work for private repositories?**  
A: Pay for storage ($0.10 per GB per month) and data transfer

**Q: What is the benefit of ECR immutable tags?**  
A: Prevents overwriting of image tags, ensuring image integrity and traceability
