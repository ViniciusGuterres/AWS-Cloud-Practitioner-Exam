# AWS CloudFormation

## What is AWS CloudFormation?

AWS CloudFormation is a service that helps you model and set up your AWS resources using **Infrastructure as Code (IaC)**. You create templates that describe your AWS resources, and CloudFormation provisions and configures those resources for you.

**Key Concept:** Treat infrastructure like software code - version controlled, repeatable, and automated.

## Core Components

### 1. Templates
**Definition:** JSON or YAML files that define AWS resources and their properties

**Template Structure:**
```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: 'My first CloudFormation template'
Resources:
  MyEC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: ami-0abcdef1234567890
      InstanceType: t2.micro
```

### 2. Stacks
**Definition:** A collection of AWS resources created and managed as a single unit

**Stack Lifecycle:**
- **Create** - Deploy resources from template
- **Update** - Modify existing resources
- **Delete** - Remove all resources in stack

### 3. Change Sets
**Definition:** Preview of changes before updating a stack
- Shows what will be added, modified, or deleted
- Allows review before execution
- Prevents accidental changes

## Key Features

### Infrastructure as Code (IaC)
- **Version Control** - Track changes over time
- **Repeatability** - Deploy same infrastructure multiple times
- **Consistency** - Eliminate configuration drift
- **Documentation** - Templates serve as documentation

### Automatic Rollback
- **Failed Creation** - Automatically deletes resources if stack creation fails
- **Failed Update** - Rolls back to previous working state
- **Dependency Management** - Handles resource dependencies automatically

### Drift Detection
- **Configuration Drift** - Identifies manual changes made outside CloudFormation
- **Drift Status** - Shows which resources have drifted
- **Remediation** - Can update stack to match current state

## Usage Examples

### Example 1: Simple Web Server
```yaml
Resources:
  WebServer:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: ami-0abcdef1234567890
      InstanceType: t2.micro
      SecurityGroups:
        - !Ref WebServerSecurityGroup
  
  WebServerSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Allow HTTP traffic
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0
```

### Example 2: S3 Bucket with Versioning
```yaml
Resources:
  MyS3Bucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: my-company-data-bucket
      VersioningConfiguration:
        Status: Enabled
      PublicAccessBlockConfiguration:
        BlockPublicAcls: true
        BlockPublicPolicy: true
```

### Example 3: Auto Scaling Group
```yaml
Resources:
  AutoScalingGroup:
    Type: AWS::AutoScaling::AutoScalingGroup
    Properties:
      MinSize: 1
      MaxSize: 5
      DesiredCapacity: 2
      LaunchTemplate:
        LaunchTemplateId: !Ref LaunchTemplate
        Version: !GetAtt LaunchTemplate.LatestVersionNumber
      VPCZoneIdentifier:
        - subnet-12345678
        - subnet-87654321
```

## Template Functions and Features

### Intrinsic Functions
- **!Ref** - Reference other resources or parameters
- **!GetAtt** - Get attributes from resources
- **!Join** - Concatenate strings
- **!Sub** - Substitute variables in strings

### Parameters
```yaml
Parameters:
  InstanceType:
    Type: String
    Default: t2.micro
    AllowedValues:
      - t2.micro
      - t2.small
      - t2.medium
```

### Outputs
```yaml
Outputs:
  WebsiteURL:
    Description: URL of the website
    Value: !Sub 'http://${WebServer.PublicDnsName}'
```

### Conditions
```yaml
Conditions:
  CreateProdResources: !Equals [!Ref Environment, 'production']

Resources:
  ProdDatabase:
    Type: AWS::RDS::DBInstance
    Condition: CreateProdResources
```

## Best Practices

### Template Organization
1. **Modular Design** - Break large templates into smaller, reusable components
2. **Nested Stacks** - Use child templates for complex architectures
3. **Cross-Stack References** - Share resources between stacks using exports

### Security
1. **IAM Roles** - Use least privilege for CloudFormation service role
2. **Parameter Store** - Store sensitive values in AWS Systems Manager
3. **Encryption** - Enable encryption for resources that support it

### Testing and Validation
1. **Template Validation** - Use `aws cloudformation validate-template`
2. **Change Sets** - Always preview changes before applying
3. **Stack Policies** - Protect critical resources from updates

## Common Use Cases

### 1. Environment Provisioning
- **Development/Staging/Production** environments
- **Consistent configuration** across environments
- **Quick environment teardown** for cost savings

### 2. Disaster Recovery
- **Infrastructure replication** in different regions
- **Automated recovery** procedures
- **Backup and restore** strategies

### 3. Compliance and Governance
- **Standardized deployments** meeting compliance requirements
- **Audit trails** of infrastructure changes
- **Policy enforcement** through templates

### 4. Multi-Account Deployments
- **AWS Organizations** integration
- **StackSets** for deploying across multiple accounts
- **Centralized governance** of infrastructure

## CloudFormation vs Other Tools

| Feature | CloudFormation | Terraform | AWS CDK |
|---------|---------------|-----------|---------|
| **Provider** | AWS Native | Third-party | AWS Native |
| **Language** | JSON/YAML | HCL | Programming languages |
| **State Management** | AWS Managed | Local/Remote | CloudFormation backend |
| **Multi-Cloud** | AWS Only | Yes | AWS focused |

## Pricing
- **No additional charges** for CloudFormation itself
- **Pay only for AWS resources** created by your stacks
- **Free tier eligible** for most operations

## Integration with Other Services

### AWS Services Integration
- **CodePipeline** - Automated deployments
- **CodeCommit** - Version control for templates
- **Systems Manager** - Parameter management
- **IAM** - Access control and permissions

### Monitoring and Logging
- **CloudTrail** - API call logging
- **CloudWatch** - Stack events and metrics
- **AWS Config** - Configuration compliance

## Key Exam Points

✅ **Infrastructure as Code (IaC)** - Treat infrastructure like software  
✅ **Templates** - JSON/YAML files defining resources  
✅ **Stacks** - Collection of resources managed together  
✅ **Automatic rollback** - Fails safely and rolls back  
✅ **Change sets** - Preview changes before applying  
✅ **No additional cost** - Pay only for resources created  
✅ **Drift detection** - Identifies manual changes  

## Common Exam Scenarios

**Scenario:** "Need to deploy identical infrastructure across multiple environments"  
**Answer:** Use CloudFormation templates for consistent, repeatable deployments

**Scenario:** "Want to version control infrastructure changes"  
**Answer:** Store CloudFormation templates in version control (CodeCommit/Git)

**Scenario:** "Need to preview infrastructure changes before applying"  
**Answer:** Use CloudFormation change sets

**Scenario:** "Infrastructure was manually modified outside of automation"  
**Answer:** Use CloudFormation drift detection to identify changes

## Practice Questions

**Q: What format are CloudFormation templates written in?**  
A: JSON or YAML

**Q: What happens if CloudFormation stack creation fails?**  
A: Automatic rollback - all created resources are deleted

**Q: How can you preview changes before updating a stack?**  
A: Use CloudFormation change sets

**Q: What is the cost of using CloudFormation?**  
A: No additional cost - pay only for the AWS resources created
