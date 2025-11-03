# AWS EBS (Elastic Block Store)

## What is AWS EBS?

AWS Elastic Block Store (EBS) is a **high-performance block storage service** designed for use with Amazon EC2 instances. EBS provides persistent, durable storage that can be attached to EC2 instances and persists independently of the instance lifecycle.

**Key Concept:** EBS volumes are network-attached storage that can be attached to any EC2 instance in the same Availability Zone. Unlike instance store volumes, EBS volumes persist even when the EC2 instance is stopped or terminated.

## Core Components

### 1. EBS Volumes
**Definition:** Virtual hard drives that can be attached to EC2 instances for persistent storage

**Volume Characteristics:**
- **Persistent storage** - Data survives instance stops, starts, and terminations
- **Network attached** - Connected over the network, not physically attached
- **AZ specific** - Volumes exist in a single Availability Zone
- **Resizable** - Can increase size and modify performance while in use
- **Backup capable** - Can create point-in-time snapshots

### 2. EBS Snapshots
**Definition:** Point-in-time backups of EBS volumes stored in Amazon S3

**Snapshot Features:**
- **Incremental backups** - Only changed blocks are saved after the first snapshot
- **Cross-region copying** - Snapshots can be copied to other AWS regions
- **Volume restoration** - Create new volumes from snapshots
- **Automated scheduling** - Can be automated using AWS Backup or lifecycle policies

### 3. Volume Types
**Definition:** Different EBS volume types optimized for specific use cases and performance requirements

**General Purpose SSD (gp3/gp2):**
- **Use case** - Boot volumes, small to medium databases, development environments
- **Performance** - Baseline performance with burst capability
- **Cost** - Balance of price and performance

**Provisioned IOPS SSD (io2/io1):**
- **Use case** - Critical business applications, large databases
- **Performance** - Consistent, high IOPS performance
- **Cost** - Higher cost for guaranteed performance

**Throughput Optimized HDD (st1):**
- **Use case** - Big data, data warehouses, log processing
- **Performance** - High throughput for sequential workloads
- **Cost** - Lower cost per GB

**Cold HDD (sc1):**
- **Use case** - Infrequently accessed data, archival storage
- **Performance** - Lowest cost storage for infrequent access
- **Cost** - Lowest cost per GB

## Key Features ⭐ **EXAM FOCUS**

### High Availability and Durability
- **99.999% availability** - Designed for high availability within an AZ
- **Automatic replication** - Data is replicated within the Availability Zone
- **Snapshot backups** - Point-in-time backups stored in S3
- **Cross-AZ recovery** - Restore volumes in different AZs from snapshots

### Scalability and Performance
- **Dynamic scaling** - Increase size and performance without downtime
- **Multiple attachment** - Multi-Attach feature for specific volume types
- **Performance monitoring** - CloudWatch metrics for volume performance
- **Encryption support** - Data encryption at rest and in transit

### Flexibility and Integration
- **Multiple volume types** - Choose optimal storage for your workload
- **EC2 integration** - Seamless attachment to EC2 instances
- **AWS Backup integration** - Centralized backup management
- **Lifecycle management** - Automated snapshot creation and deletion

## Common Use Cases 🎯 **EXAM SCENARIOS**

### 1. Database Storage
**Scenario:** Running a production database that requires consistent performance
- **Solution:** Use Provisioned IOPS SSD (io2) for guaranteed performance
- **Benefits:** Consistent IOPS, high durability, snapshot backups
- **Exam tip:** Choose io2/io1 for databases requiring consistent performance

### 2. Boot Volumes
**Scenario:** Operating system storage for EC2 instances
- **Solution:** Use General Purpose SSD (gp3) for boot volumes
- **Benefits:** Good performance, cost-effective, reliable
- **Exam tip:** gp3 is typically the default choice for boot volumes

### 3. Big Data Analytics
**Scenario:** Processing large datasets with sequential access patterns
- **Solution:** Use Throughput Optimized HDD (st1) for cost-effective throughput
- **Benefits:** High throughput, lower cost per GB
- **Exam tip:** st1 is optimized for sequential workloads, not random access

### 4. Backup and Archival
**Scenario:** Long-term storage of infrequently accessed data
- **Solution:** Use Cold HDD (sc1) for lowest cost storage
- **Benefits:** Lowest cost per GB, suitable for archival
- **Exam tip:** sc1 is for infrequently accessed data with cost optimization

### 5. Development and Testing
**Scenario:** Development environments requiring flexible storage
- **Solution:** Use General Purpose SSD (gp3) with snapshot capabilities
- **Benefits:** Balanced performance, easy to snapshot and restore
- **Exam tip:** gp3 provides flexibility for dev/test environments

## Security and Compliance 🔒

### Encryption
- **Encryption at rest** - AES-256 encryption using AWS KMS
- **Encryption in transit** - Data encrypted between EC2 and EBS
- **Key management** - Integration with AWS Key Management Service (KMS)
- **Snapshot encryption** - Encrypted volumes create encrypted snapshots

### Access Control
- **IAM policies** - Control who can create, attach, and manage volumes
- **Resource-based policies** - Fine-grained access control
- **VPC integration** - Network-level security controls
- **CloudTrail logging** - API call logging for compliance

## Pricing Model 💰 **EXAM FOCUS**

### Volume Pricing
- **Provisioned storage** - Pay for allocated storage capacity (GB/month)
- **Provisioned IOPS** - Additional cost for guaranteed IOPS (io2/io1)
- **Throughput** - Additional cost for provisioned throughput (gp3)
- **No data transfer charges** - Between EBS and EC2 in same AZ

### Snapshot Pricing
- **Storage cost** - Pay for actual data stored in snapshots
- **Incremental billing** - Only pay for changed data after first snapshot
- **Cross-region transfer** - Data transfer charges for copying snapshots
- **Lifecycle policies** - Automated deletion to control costs

### Cost Optimization Tips
- **Right-size volumes** - Choose appropriate volume type and size
- **Delete unused snapshots** - Implement lifecycle policies
- **Use gp3 over gp2** - Better price/performance ratio
- **Monitor usage** - Use CloudWatch to optimize performance and cost

## Best Practices 📋

### Performance Optimization
- **Pre-warm volumes** - Initialize volumes from snapshots for consistent performance
- **Use appropriate volume type** - Match volume type to workload requirements
- **Monitor metrics** - Use CloudWatch to track volume performance
- **Optimize instance type** - Ensure EC2 instance can utilize EBS performance

### Backup and Recovery
- **Regular snapshots** - Create consistent backup schedules
- **Cross-region copies** - Copy critical snapshots to other regions
- **Test restores** - Regularly test snapshot restoration procedures
- **Automate backups** - Use AWS Backup for centralized backup management

### Security Best Practices
- **Enable encryption** - Encrypt sensitive data at rest
- **Use IAM policies** - Implement least privilege access
- **Monitor access** - Use CloudTrail for audit logging
- **Network security** - Implement proper VPC security groups

## Integration with Other AWS Services 🔗

### Amazon EC2
- **Primary integration** - EBS volumes attach to EC2 instances
- **Boot volumes** - EC2 instances can boot from EBS volumes
- **Multiple attachments** - Some volume types support multi-attach
- **Instance store comparison** - EBS provides persistence vs. instance store

### AWS Backup
- **Centralized backup** - Manage EBS snapshots with other AWS backups
- **Cross-service policies** - Unified backup policies across services
- **Compliance reporting** - Centralized backup compliance monitoring
- **Automated scheduling** - Policy-based backup automation

### Amazon S3
- **Snapshot storage** - EBS snapshots are stored in S3
- **Cross-region replication** - Snapshots can be copied between regions
- **Lifecycle management** - Automated snapshot deletion policies
- **Durability** - Inherits S3's 99.999999999% (11 9's) durability

### AWS CloudFormation
- **Infrastructure as Code** - Define EBS volumes in CloudFormation templates
- **Automated provisioning** - Create volumes as part of stack deployment
- **Dependency management** - Ensure proper resource creation order
- **Stack updates** - Modify volume configurations through stack updates

## Monitoring and Troubleshooting 📊

### CloudWatch Metrics
- **Volume metrics** - IOPS, throughput, queue depth, latency
- **Performance monitoring** - Track volume performance over time
- **Alerting** - Set up alarms for performance thresholds
- **Cost monitoring** - Track storage costs and usage patterns

### Common Issues and Solutions
- **Performance issues** - Check volume type, instance type, and workload patterns
- **Attachment problems** - Verify AZ compatibility and instance state
- **Snapshot failures** - Check permissions and available storage space
- **Encryption errors** - Verify KMS key permissions and policies

## Exam Tips 🎓

### Key Points to Remember
- **EBS volumes are AZ-specific** - Cannot attach across AZs
- **Snapshots are region-specific** - But can be copied to other regions
- **Root volumes can be EBS or instance store** - EBS root volumes persist
- **gp3 is newer than gp2** - Better price/performance ratio
- **io2 is newer than io1** - Higher durability and IOPS/GB ratio

### Common Exam Scenarios
- **Database storage** → Choose io2/io1 for consistent performance
- **Boot volumes** → Choose gp3 for balanced performance and cost
- **Big data processing** → Choose st1 for high throughput workloads
- **Archival storage** → Choose sc1 for lowest cost per GB
- **Cross-AZ backup** → Use snapshots to restore in different AZ

### Comparison Points
- **EBS vs Instance Store** - Persistence vs. performance
- **gp3 vs gp2** - Independent IOPS and throughput provisioning
- **io2 vs io1** - Higher durability and better IOPS/GB ratio
- **HDD vs SSD** - Cost vs. performance trade-offs
