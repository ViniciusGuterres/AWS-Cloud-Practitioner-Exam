# AWS EFS (Elastic File System)

## What is AWS EFS?

AWS Elastic File System (EFS) is a **fully managed, scalable, and elastic NFS (Network File System)** that can be used with AWS cloud services and on-premises resources. EFS provides shared file storage that can be accessed concurrently by multiple EC2 instances across multiple Availability Zones.

**Key Concept:** EFS provides a simple, scalable file system that grows and shrinks automatically as you add and remove files, eliminating the need to provision and manage capacity to accommodate growth.

## Core Components

### 1. File Systems
**Definition:** The primary resource in EFS that provides a file system interface and file system semantics

**File System Characteristics:**
- **Elastic scaling** - Automatically grows and shrinks as files are added/removed
- **Multi-AZ access** - Can be accessed from multiple Availability Zones simultaneously
- **POSIX-compliant** - Standard file system interface with full file system semantics
- **Concurrent access** - Thousands of EC2 instances can access simultaneously
- **Petabyte scale** - Can scale to petabytes of data

### 2. Mount Targets
**Definition:** Network endpoints that provide access to EFS file systems from EC2 instances

**Mount Target Features:**
- **AZ specific** - One mount target per Availability Zone
- **IP address** - Each mount target has an IP address in the subnet
- **Security groups** - Control access using security group rules
- **DNS names** - Automatically assigned DNS names for easy mounting

### 3. Access Points
**Definition:** Application-specific entry points into EFS file systems that enforce user identity and path

**Access Point Benefits:**
- **User identity enforcement** - Enforce specific POSIX user and group IDs
- **Path enforcement** - Restrict access to specific directories
- **Root directory creation** - Automatically create root directories
- **Application isolation** - Isolate different applications using the same file system

## Key Features ⭐ **EXAM FOCUS**

### Scalability and Performance
- **Automatic scaling** - No capacity planning required
- **High throughput** - Supports high levels of aggregate throughput
- **Low latency** - Consistent, low-latency performance
- **Concurrent access** - Multiple instances can access simultaneously

### Availability and Durability
- **Multi-AZ storage** - Data stored redundantly across multiple AZs
- **99.999999999% durability** - Designed for 11 9's of durability
- **High availability** - No single points of failure
- **Regional service** - Spans multiple Availability Zones

### Security and Compliance
- **Encryption** - Data encrypted in transit and at rest
- **Access control** - Integration with IAM, security groups, and NFS permissions
- **VPC integration** - Secure access within your VPC
- **Compliance** - Meets various compliance standards

## Storage Classes

### 1. Standard Storage Class
**Use Case:** Frequently accessed files requiring the lowest latency

**Characteristics:**
- **Performance** - Lowest latency per operation
- **Availability** - Highest level of availability
- **Cost** - Higher storage cost, no retrieval fees
- **Access pattern** - Frequent access (multiple times per day)

### 2. Infrequent Access (IA) Storage Class
**Use Case:** Files not accessed every day with cost optimization

**Characteristics:**
- **Performance** - Slightly higher latency than Standard
- **Cost savings** - Up to 92% lower storage costs than Standard
- **Retrieval fees** - Per-GB retrieval fees apply
- **Access pattern** - Infrequent access (few times per month)

### 3. Archive Storage Class
**Use Case:** Long-term archival with rarely accessed files

**Characteristics:**
- **Performance** - Higher latency for file access
- **Cost savings** - Up to 50% lower storage costs than IA
- **Retrieval fees** - Higher per-GB retrieval fees
- **Access pattern** - Rarely accessed (few times per year)

## Performance Modes

### 1. General Purpose Mode
**Default mode** optimized for latency-sensitive workloads

**Characteristics:**
- **Latency** - Lowest latency per operation
- **Throughput** - Up to 7,000 file operations per second
- **Use cases** - Web serving, content management, general file serving
- **Recommendation** - Use unless you need higher performance

### 2. Max I/O Mode
**Higher performance** mode for applications needing higher levels of aggregate throughput

**Characteristics:**
- **Latency** - Slightly higher latency per operation
- **Throughput** - Can scale to higher levels of aggregate throughput and IOPS
- **Use cases** - Applications with higher performance requirements
- **Trade-off** - Higher performance at the cost of increased latency

## Throughput Modes

### 1. Provisioned Throughput Mode
**Definition:** Specify the throughput independent of the amount of data stored

**Features:**
- **Predictable performance** - Consistent throughput regardless of file system size
- **Higher throughput** - Can provision throughput higher than baseline
- **Additional cost** - Pay for provisioned throughput above baseline
- **Use case** - Applications requiring consistent high throughput

### 2. Bursting Throughput Mode
**Definition:** Throughput scales with file system size (default mode)

**Features:**
- **Baseline throughput** - 50 MiB/s per TiB of storage
- **Burst capability** - Can burst to higher throughput levels
- **Burst credits** - Accumulate credits when below baseline
- **Cost effective** - No additional throughput charges

## Common Use Cases ⭐ **EXAM FOCUS**

### Content Management and Web Serving
- **Shared content** - Multiple web servers accessing shared content
- **Media files** - Storing and serving images, videos, documents
- **Static websites** - Shared storage for static website assets
- **Content distribution** - Distributing content across multiple instances

### Big Data and Analytics
- **Data lakes** - Centralized repository for structured and unstructured data
- **Analytics workloads** - Shared access to datasets for analysis
- **Machine learning** - Training data accessible by multiple ML instances
- **Log aggregation** - Centralized storage for application and system logs

### Application Data Sharing
- **Microservices** - Shared storage between containerized applications
- **Development environments** - Shared code repositories and build artifacts
- **Configuration files** - Centralized configuration management
- **Database backups** - Shared storage for database backup files

### Backup and Archival
- **File system backups** - Backup destination for on-premises file systems
- **Long-term archival** - Cost-effective storage for rarely accessed data
- **Disaster recovery** - Backup storage accessible from multiple AZs
- **Compliance** - Long-term retention for regulatory requirements

## Integration with AWS Services

### Amazon EC2
- **Native integration** - Mount EFS directly on EC2 instances
- **Cross-AZ access** - Access from instances in different AZs
- **Auto Scaling** - Shared storage scales with Auto Scaling groups
- **Container support** - Use with containerized applications

### AWS Lambda
- **Serverless file access** - Lambda functions can access EFS
- **Persistent storage** - Maintain state between Lambda invocations
- **Shared libraries** - Store shared code and dependencies
- **Data processing** - Process files stored in EFS

### Amazon ECS and EKS
- **Container storage** - Persistent storage for containerized applications
- **Shared volumes** - Multiple containers can access the same files
- **Stateful applications** - Support for stateful containerized workloads
- **Data persistence** - Data survives container restarts

### AWS Backup
- **Automated backups** - Schedule automatic backups of EFS file systems
- **Point-in-time recovery** - Restore file systems to specific points in time
- **Cross-region backup** - Backup EFS to different AWS regions
- **Compliance** - Meet backup and retention requirements

## Security Features

### Encryption
- **Encryption in transit** - Data encrypted during transfer using TLS
- **Encryption at rest** - Data encrypted when stored using AWS KMS
- **Key management** - Integration with AWS Key Management Service
- **Performance** - Minimal impact on file system performance

### Access Control
- **IAM policies** - Control who can create and manage file systems
- **Security groups** - Control network access to mount targets
- **NFS permissions** - Standard POSIX file permissions
- **Access points** - Application-specific access control

### Network Security
- **VPC integration** - File systems accessible only within your VPC
- **Private connectivity** - No internet gateway required
- **Network ACLs** - Additional network-level security controls
- **VPC endpoints** - Private connectivity to EFS API

## Pricing Model ⭐ **EXAM FOCUS**

### Storage Pricing
- **Pay for what you use** - Only pay for storage actually used
- **No minimum fees** - No minimum file system size requirements
- **Storage classes** - Different pricing for Standard, IA, and Archive
- **Automatic tiering** - Intelligent Tiering can optimize costs automatically

### Throughput Pricing
- **Provisioned throughput** - Additional charges for provisioned throughput above baseline
- **Bursting throughput** - No additional charges for baseline throughput
- **Regional variations** - Pricing varies by AWS region
- **Free tier** - 5 GB of Standard storage for 12 months

### Request Pricing
- **IA and Archive** - Per-GB retrieval fees for accessing files
- **Standard class** - No retrieval fees for frequently accessed files
- **API requests** - Charges for EFS API calls
- **Data transfer** - Standard AWS data transfer charges apply

## Best Practices

### Performance Optimization
- **Use General Purpose mode** - Unless you specifically need Max I/O
- **Optimize file operations** - Minimize small, synchronous operations
- **Use multiple threads** - Parallelize file operations when possible
- **Monitor performance** - Use CloudWatch metrics to track performance

### Cost Optimization
- **Use Intelligent Tiering** - Automatically move files to lower-cost storage classes
- **Monitor usage patterns** - Understand access patterns to choose appropriate storage classes
- **Right-size throughput** - Use Provisioned mode only when necessary
- **Regular cleanup** - Remove unnecessary files to reduce storage costs

### Security Best Practices
- **Enable encryption** - Use encryption in transit and at rest
- **Least privilege access** - Grant minimum necessary permissions
- **Use Access Points** - Implement application-specific access controls
- **Monitor access** - Use CloudTrail to audit file system access

### Backup and Recovery
- **Regular backups** - Use AWS Backup for automated backup scheduling
- **Test recovery** - Regularly test backup restoration procedures
- **Cross-region backups** - Consider cross-region backups for disaster recovery
- **Retention policies** - Implement appropriate backup retention policies

## Monitoring and Troubleshooting

### CloudWatch Metrics
- **Performance metrics** - Monitor throughput, IOPS, and latency
- **Storage metrics** - Track total file system size and object count
- **Client connections** - Monitor number of connected clients
- **Burst credit balance** - Track burst credits for bursting throughput mode

### Common Issues
- **Mount failures** - Check security groups and network connectivity
- **Performance issues** - Monitor burst credits and consider Provisioned mode
- **Access denied** - Verify IAM permissions and NFS permissions
- **High costs** - Review storage class usage and access patterns

## Exam Tips ⭐ **CLF-C02 FOCUS**

### Key Concepts to Remember
- **Shared file storage** - Multiple instances can access simultaneously
- **Elastic scaling** - Automatically grows and shrinks
- **Multi-AZ availability** - Accessible across multiple Availability Zones
- **POSIX-compliant** - Standard file system interface

### Common Exam Scenarios
- **Shared storage needs** - When multiple EC2 instances need shared file access
- **Scalable file systems** - When you need storage that grows automatically
- **Cross-AZ access** - When instances in different AZs need shared storage
- **Container storage** - Persistent storage for containerized applications

### Service Comparisons
- **EFS vs EBS** - EFS is shared, EBS is single-instance
- **EFS vs S3** - EFS is file system, S3 is object storage
- **EFS vs FSx** - EFS is Linux-based, FSx supports Windows and high-performance workloads
- **EFS vs Instance Store** - EFS is persistent, Instance Store is temporary

### Cost Considerations
- **Pay for usage** - Only pay for storage actually used
- **Storage classes** - IA and Archive provide cost savings for infrequent access
- **No capacity planning** - Eliminates need to provision storage capacity
- **Intelligent Tiering** - Automatically optimizes costs based on access patterns
