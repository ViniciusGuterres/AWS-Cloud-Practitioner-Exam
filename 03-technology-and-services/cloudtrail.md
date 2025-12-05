# AWS CloudTrail

## What is AWS CloudTrail?

AWS CloudTrail is a service that enables **governance, compliance, operational auditing, and risk auditing** of your AWS account. It records AWS API calls and delivers log files to an S3 bucket, providing a complete audit trail of all actions taken in your AWS account.

**Key Concept:** CloudTrail answers "Who did what, when, and from where?" in your AWS environment.

## Core Components

### 1. Events
**Definition:** Record of an activity in an AWS account (API call, console sign-in, etc.)

**Event Types:**
- **Management Events** - Control plane operations (creating/deleting resources)
- **Data Events** - Data plane operations (S3 object access, Lambda function execution)
- **Insight Events** - Unusual activity patterns detected by machine learning

### 2. Trails
**Definition:** Configuration that enables delivery of events to S3 bucket, CloudWatch Logs, and EventBridge

**Trail Types:**
- **Single-region trail** - Records events in one region
- **Multi-region trail** - Records events in all regions
- **Organization trail** - Records events for all accounts in AWS Organizations

### 3. Event History
**Definition:** Viewable, searchable, and downloadable record of past 90 days of management events
- **Free feature** - No additional cost
- **Limited to management events** only
- **90-day retention** period

## Key Features

### Comprehensive Logging
- **API calls** from AWS Management Console
- **CLI and SDK** operations
- **AWS service** actions
- **Third-party integrations**

### Real-time Delivery
- **S3 bucket** delivery (within 15 minutes)
- **CloudWatch Logs** integration
- **EventBridge** for real-time processing

### Security and Compliance
- **Log file integrity** validation
- **Encryption** at rest and in transit
- **Access logging** for audit trails
- **Compliance reporting** capabilities

### Advanced Analytics
- **CloudTrail Insights** - Detect unusual activity patterns
- **CloudWatch integration** - Metrics and alarms
- **Athena queries** - Analyze logs with SQL

## Event Structure

### Sample CloudTrail Event
```json
{
  "eventVersion": "1.08",
  "userIdentity": {
    "type": "IAMUser",
    "principalId": "AIDACKCEVSQ6C2EXAMPLE",
    "arn": "arn:aws:iam::123456789012:user/johndoe",
    "accountId": "123456789012",
    "userName": "johndoe"
  },
  "eventTime": "2023-01-15T12:00:00Z",
  "eventSource": "ec2.amazonaws.com",
  "eventName": "RunInstances",
  "awsRegion": "us-east-1",
  "sourceIPAddress": "203.0.113.12",
  "userAgent": "aws-cli/2.0.0",
  "requestParameters": {
    "instanceType": "t2.micro",
    "imageId": "ami-0abcdef1234567890"
  },
  "responseElements": {
    "instancesSet": {
      "items": [
        {
          "instanceId": "i-1234567890abcdef0"
        }
      ]
    }
  }
}
```

## Usage Examples

### Example 1: Create a Multi-Region Trail
```bash
# Create S3 bucket for CloudTrail logs
aws s3 mb s3://my-cloudtrail-bucket-12345

# Create CloudTrail
aws cloudtrail create-trail \
  --name MyCloudTrail \
  --s3-bucket-name my-cloudtrail-bucket-12345 \
  --include-global-service-events \
  --is-multi-region-trail \
  --enable-log-file-validation

# Start logging
aws cloudtrail start-logging --name MyCloudTrail
```

### Example 2: Enable Data Events for S3
```bash
# Configure data events for S3 bucket
aws cloudtrail put-event-selectors \
  --trail-name MyCloudTrail \
  --event-selectors '[
    {
      "ReadWriteType": "All",
      "IncludeManagementEvents": true,
      "DataResources": [
        {
          "Type": "AWS::S3::Object",
          "Values": ["arn:aws:s3:::my-sensitive-bucket/*"]
        }
      ]
    }
  ]'
```

### Example 3: Query CloudTrail Logs with Athena
```sql
-- Create table for CloudTrail logs in Athena
CREATE EXTERNAL TABLE cloudtrail_logs (
  eventversion STRING,
  useridentity STRUCT<
    type: STRING,
    principalid: STRING,
    arn: STRING,
    accountid: STRING,
    username: STRING
  >,
  eventtime STRING,
  eventsource STRING,
  eventname STRING,
  awsregion STRING,
  sourceipaddress STRING,
  useragent STRING
)
PARTITIONED BY (
  region STRING,
  year STRING,
  month STRING,
  day STRING
)
STORED AS INPUTFORMAT 'com.amazon.emr.cloudtrail.CloudTrailInputFormat'
OUTPUTFORMAT 'org.apache.hadoop.hive.ql.io.HiveIgnoreKeyTextOutputFormat'
LOCATION 's3://my-cloudtrail-bucket-12345/AWSLogs/123456789012/CloudTrail/'

-- Query for failed login attempts
SELECT 
  eventtime,
  sourceipaddress,
  useridentity.username,
  errorcode,
  errormessage
FROM cloudtrail_logs
WHERE eventname = 'ConsoleLogin'
  AND errorcode IS NOT NULL
  AND year = '2023'
  AND month = '01'
ORDER BY eventtime DESC;
```

## CloudTrail Insights

### Purpose
**Detect unusual activity patterns** in your AWS account using machine learning

### How It Works
1. **Baseline establishment** - Analyzes normal API call patterns
2. **Anomaly detection** - Identifies deviations from baseline
3. **Insight generation** - Creates insight events for unusual activity
4. **Notification** - Delivers insights to S3 and CloudWatch

### Types of Insights
- **Unusual API call volume** - Spikes in API activity
- **Error rate anomalies** - Unusual error patterns
- **Geographic anomalies** - API calls from unusual locations
- **Time-based anomalies** - Activity outside normal hours

### Example Insight Event
```json
{
  "eventVersion": "1.07",
  "eventTime": "2023-01-15T14:30:00Z",
  "eventSource": "cloudtrail.amazonaws.com",
  "eventName": "CloudTrailInsight",
  "insightDetails": {
    "state": "Start",
    "eventSource": "ec2.amazonaws.com",
    "eventName": "RunInstances",
    "insightType": "ApiCallRateInsight",
    "insightContext": {
      "statistics": {
        "baseline": {
          "average": 2.5
        },
        "insight": {
          "average": 25.7
        }
      }
    }
  }
}
```

## Integration with Other Services

### Amazon S3
- **Log storage** - Primary destination for CloudTrail logs
- **Lifecycle policies** - Automatic archival and deletion
- **Cross-region replication** - Backup logs to different region

### CloudWatch Logs
- **Real-time monitoring** - Stream logs to CloudWatch
- **Metric filters** - Create custom metrics from log data
- **Alarms** - Alert on specific events or patterns

### EventBridge (CloudWatch Events)
- **Real-time processing** - React to events as they happen
- **Event routing** - Send events to Lambda, SNS, SQS
- **Custom applications** - Build event-driven architectures

### AWS Config
- **Configuration changes** - Track who made configuration changes
- **Compliance auditing** - Correlate changes with compliance status
- **Change attribution** - Link Config changes to CloudTrail events

## Security Best Practices

### Trail Configuration
1. **Enable in all regions** - Comprehensive coverage
2. **Enable log file validation** - Detect tampering
3. **Use separate S3 bucket** - Dedicated for CloudTrail logs
4. **Enable MFA delete** - Protect against accidental deletion

### Access Control
1. **Restrict S3 bucket access** - Only authorized users/roles
2. **Use CloudTrail service role** - Least privilege access
3. **Enable S3 bucket notifications** - Alert on log delivery
4. **Monitor CloudTrail configuration** - Detect unauthorized changes

### Log Management
1. **Encrypt logs at rest** - Use S3 server-side encryption
2. **Encrypt logs in transit** - HTTPS delivery
3. **Set lifecycle policies** - Manage storage costs
4. **Monitor log delivery** - Ensure continuous logging

## Common Use Cases

### 1. Security Auditing
- **Track privileged user** activities
- **Monitor failed login** attempts
- **Detect unauthorized** API calls
- **Investigate security** incidents

### 2. Compliance Reporting
- **Audit trail** for regulatory requirements
- **Change tracking** for compliance frameworks
- **Access logging** for data governance
- **Retention policies** for legal requirements

### 3. Operational Troubleshooting
- **Root cause analysis** - What changed before the issue?
- **Change attribution** - Who made the change?
- **Timeline reconstruction** - Sequence of events
- **Impact assessment** - What was affected?

### 4. Cost Analysis
- **Resource creation** tracking
- **Usage pattern** analysis
- **Cost attribution** by user/role
- **Optimization opportunities** identification

## Pricing

### Management Events
- **First copy** of management events - **Free**
- **Additional copies** - $2.00 per 100,000 events

### Data Events
- **First 2 million** data events per month - **Free**
- **Additional data events** - $0.10 per 100,000 events

### CloudTrail Insights
- **$0.35 per 100,000 events** analyzed

### Additional Costs
- **S3 storage** for log files
- **Data transfer** charges
- **CloudWatch Logs** ingestion (if configured)

## Key Exam Points

✅ **API call logging** - Records all AWS API calls and console actions  
✅ **90-day event history** - Free searchable history of management events  
✅ **Multi-region trails** - Log events from all regions  
✅ **Data events** - Optional logging of S3/Lambda data plane operations  
✅ **CloudTrail Insights** - ML-powered anomaly detection  
✅ **Log file validation** - Detect tampering with log files  
✅ **Integration** - Works with S3, CloudWatch, EventBridge, Config  

## Common Exam Scenarios

**Scenario:** "Need to track who deleted an S3 object"  
**Answer:** Enable CloudTrail data events for the S3 bucket

**Scenario:** "Want to monitor for unusual API activity patterns"  
**Answer:** Enable CloudTrail Insights

**Scenario:** "Need audit trail for compliance across all regions"  
**Answer:** Create multi-region CloudTrail with log file validation

**Scenario:** "Want real-time alerts when root user logs in"  
**Answer:** Stream CloudTrail to CloudWatch Logs and create alarm

## Practice Questions

**Q: How long does CloudTrail Event History retain management events for free?**  
A: 90 days

**Q: What type of events does CloudTrail record by default?**  
A: Management events (control plane operations)

**Q: How can you detect if CloudTrail log files have been tampered with?**  
A: Enable log file validation

**Q: What service can detect unusual API activity patterns in CloudTrail?**  
A: CloudTrail Insights

**Q: Where are CloudTrail logs typically stored?**  
A: Amazon S3 bucket
