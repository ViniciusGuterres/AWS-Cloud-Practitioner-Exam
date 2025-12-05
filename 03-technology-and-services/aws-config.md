# AWS Config

## What is AWS Config?

AWS Config is a service that enables you to **assess, audit, and evaluate the configurations** of your AWS resources. It continuously monitors and records AWS resource configurations and allows you to automate the evaluation of recorded configurations against desired configurations.

**Key Concept:** AWS Config helps you understand "What changed?" and "Is my infrastructure compliant with policies?"

## Core Components

### 1. Configuration Items (CIs)
**Definition:** Point-in-time snapshot of a resource's configuration

**Contains:**
- Resource type and ID
- Configuration details
- Relationships to other resources
- Metadata (creation time, region, etc.)
- Configuration history

### 2. Configuration History
**Definition:** Collection of configuration items for a resource over time
- Track how resource configurations change
- Identify when changes occurred
- Understand configuration drift

### 3. Configuration Recorder
**Definition:** Records configurations of supported AWS resources in your account
- **Must be enabled** to start recording
- Records resource configurations and relationships
- Stores data in S3 bucket

### 4. Delivery Channel
**Definition:** Delivers configuration snapshots and history to S3 bucket
- **Required** for Config to function
- Can also send to SNS topic for notifications
- Configurable delivery frequency

## Key Features

### Configuration Compliance
- **Config Rules** - Evaluate resource configurations against policies
- **Automatic remediation** - Fix non-compliant resources automatically
- **Compliance dashboard** - Visual overview of compliance status

### Change Tracking
- **Configuration timeline** - See when resources changed
- **Change notifications** - Get alerted when configurations change
- **Relationship tracking** - Understand resource dependencies

### Multi-Account and Multi-Region
- **Aggregators** - Collect data from multiple accounts/regions
- **Organization-wide** - Deploy rules across AWS Organizations
- **Centralized compliance** - Single pane of glass view

## Config Rules

### AWS Managed Rules
**Pre-built rules** for common compliance requirements:

- **s3-bucket-public-read-prohibited** - S3 buckets should not allow public read
- **encrypted-volumes** - EBS volumes should be encrypted
- **root-access-key-check** - Root account should not have access keys
- **required-tags** - Resources should have required tags

### Custom Rules
**User-defined rules** using AWS Lambda functions:
```python
import boto3
import json

def lambda_handler(event, context):
    # Custom rule logic
    config_client = boto3.client('config')
    
    # Evaluate resource configuration
    compliance_type = 'COMPLIANT'  # or 'NON_COMPLIANT'
    
    # Return evaluation result
    return {
        'ComplianceType': compliance_type,
        'Annotation': 'Resource meets security requirements'
    }
```

### Rule Triggers
- **Configuration changes** - Evaluate when resource changes
- **Periodic** - Evaluate on schedule (24 hours, etc.)
- **Hybrid** - Both change-triggered and periodic

## Usage Examples

### Example 1: Enable Config in a Region
```bash
# Create S3 bucket for Config
aws s3 mb s3://my-config-bucket-12345

# Create IAM role for Config
aws iam create-role --role-name ConfigRole --assume-role-policy-document file://config-trust-policy.json

# Attach policy to role
aws iam attach-role-policy --role-name ConfigRole --policy-arn arn:aws:iam::aws:policy/service-role/ConfigRole

# Create configuration recorder
aws configservice put-configuration-recorder \
  --configuration-recorder name=default,roleARN=arn:aws:iam::123456789012:role/ConfigRole \
  --recording-group allSupported=true,includeGlobalResourceTypes=true

# Create delivery channel
aws configservice put-delivery-channel \
  --delivery-channel name=default,s3BucketName=my-config-bucket-12345
```

### Example 2: Deploy Config Rule
```bash
# Deploy managed rule for S3 bucket encryption
aws configservice put-config-rule \
  --config-rule '{
    "ConfigRuleName": "s3-bucket-server-side-encryption-enabled",
    "Source": {
      "Owner": "AWS",
      "SourceIdentifier": "S3_BUCKET_SERVER_SIDE_ENCRYPTION_ENABLED"
    }
  }'
```

### Example 3: Query Configuration History
```bash
# Get configuration history for specific resource
aws configservice get-resource-config-history \
  --resource-type AWS::EC2::Instance \
  --resource-id i-1234567890abcdef0 \
  --start-time 2023-01-01T00:00:00Z \
  --end-time 2023-01-31T23:59:59Z
```

## Remediation

### Automatic Remediation
**Definition:** Automatically fix non-compliant resources using Systems Manager documents

**Example Remediation Actions:**
- **Stop non-compliant EC2 instances**
- **Enable S3 bucket encryption**
- **Remove public access from security groups**
- **Add required tags to resources**

### Remediation Configuration
```json
{
  "ConfigRuleName": "s3-bucket-public-read-prohibited",
  "RemediationConfigurations": [
    {
      "ConfigRuleName": "s3-bucket-public-read-prohibited",
      "TargetType": "SSM_DOCUMENT",
      "TargetId": "AWS-DisableS3BucketPublicReadWrite",
      "TargetVersion": "1",
      "Parameters": {
        "BucketName": {
          "ResourceValue": {
            "Value": "RESOURCE_ID"
          }
        }
      },
      "Automatic": true,
      "ExecutionControls": {
        "SsmControls": {
          "ConcurrentExecutionRatePercentage": 10,
          "ErrorPercentage": 10
        }
      }
    }
  ]
}
```

## Configuration Aggregators

### Purpose
- **Multi-account** configuration data collection
- **Multi-region** configuration data collection
- **Centralized compliance** reporting

### Types
1. **Account Aggregator** - Collect from multiple regions in same account
2. **Organization Aggregator** - Collect from multiple accounts in AWS Organizations

### Benefits
- **Single dashboard** for compliance across organization
- **Cross-account** rule deployment
- **Centralized reporting** and analytics

## Conformance Packs

### Definition
**Collection of Config rules and remediation actions** deployed as a single entity

### AWS Conformance Packs
- **Operational Best Practices for PCI DSS**
- **Operational Best Practices for NIST**
- **Operational Best Practices for CIS**
- **Security Best Practices**

### Custom Conformance Packs
```yaml
# conformance-pack-template.yaml
Parameters:
  BucketName:
    Type: String
    Default: my-config-bucket

Resources:
  S3BucketEncryptionRule:
    Type: AWS::Config::ConfigRule
    Properties:
      ConfigRuleName: s3-bucket-server-side-encryption-enabled
      Source:
        Owner: AWS
        SourceIdentifier: S3_BUCKET_SERVER_SIDE_ENCRYPTION_ENABLED
```

## Pricing

### Configuration Items
- **$0.003 per configuration item** recorded
- First 1,000 configuration items per month are free

### Config Rules
- **$0.001 per config rule evaluation**
- First 100,000 evaluations per month are free

### Conformance Packs
- **$0.0012 per conformance pack evaluation**

### Additional Costs
- **S3 storage** for configuration snapshots
- **SNS notifications** if configured
- **Lambda functions** for custom rules

## Integration with Other Services

### AWS Organizations
- **Organization-wide** Config deployment
- **Delegated administrator** for Config management
- **Cross-account** aggregation

### AWS Systems Manager
- **Remediation actions** using SSM documents
- **Parameter Store** for configuration values
- **Automation documents** for complex remediation

### AWS Security Hub
- **Compliance findings** integration
- **Security standards** mapping
- **Centralized security** dashboard

### AWS CloudTrail
- **API call logging** for Config operations
- **Change attribution** - Who made the change?
- **Audit trail** for compliance

## Best Practices

### Setup and Configuration
1. **Enable in all regions** where you have resources
2. **Use organization aggregator** for multi-account setup
3. **Configure appropriate IAM roles** with least privilege
4. **Set up S3 bucket lifecycle** policies for cost optimization

### Rule Management
1. **Start with managed rules** before creating custom ones
2. **Test rules** in non-production environments first
3. **Use conformance packs** for standardized compliance
4. **Monitor rule evaluation** costs

### Remediation
1. **Test remediation actions** thoroughly
2. **Use manual remediation** for critical resources
3. **Set appropriate execution controls** to limit impact
4. **Monitor remediation** results and failures

## Common Use Cases

### 1. Security Compliance
- **Ensure S3 buckets** are not publicly accessible
- **Verify encryption** is enabled on EBS volumes
- **Check security group** configurations
- **Monitor IAM** policy changes

### 2. Operational Compliance
- **Ensure required tags** are present on resources
- **Verify backup** configurations
- **Check resource** naming conventions
- **Monitor configuration** drift

### 3. Cost Optimization
- **Identify unused** resources
- **Check for oversized** instances
- **Monitor storage** configurations
- **Track resource** utilization

### 4. Change Management
- **Track configuration** changes over time
- **Identify unauthorized** changes
- **Understand resource** relationships
- **Audit compliance** status

## Key Exam Points

✅ **Configuration monitoring** - Tracks resource configurations and changes  
✅ **Config Rules** - Evaluate compliance against policies  
✅ **Configuration Items** - Point-in-time snapshots of resources  
✅ **Automatic remediation** - Fix non-compliant resources automatically  
✅ **Multi-account aggregation** - Centralized compliance view  
✅ **Conformance Packs** - Pre-built compliance templates  
✅ **Integration** - Works with Organizations, Security Hub, Systems Manager  

## Common Exam Scenarios

**Scenario:** "Need to ensure all S3 buckets have encryption enabled"  
**Answer:** Use AWS Config rule "s3-bucket-server-side-encryption-enabled"

**Scenario:** "Want to track configuration changes across multiple AWS accounts"  
**Answer:** Set up AWS Config with organization aggregator

**Scenario:** "Need to automatically fix non-compliant security groups"  
**Answer:** Use AWS Config with automatic remediation using Systems Manager

**Scenario:** "Want to implement PCI DSS compliance across organization"  
**Answer:** Deploy AWS Config conformance pack for PCI DSS

## Practice Questions

**Q: What does AWS Config track?**  
A: Resource configurations and changes over time

**Q: How can you automatically fix non-compliant resources?**  
A: Use AWS Config automatic remediation with Systems Manager documents

**Q: What is a conformance pack?**  
A: Collection of Config rules and remediation actions for compliance frameworks

**Q: How do you get a centralized view of compliance across multiple accounts?**  
A: Use AWS Config aggregator with AWS Organizations
