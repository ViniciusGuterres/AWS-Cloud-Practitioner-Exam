# AWS CloudWatch

## What is AWS CloudWatch?

AWS CloudWatch is a **monitoring and observability service** that provides data and actionable insights to monitor applications, respond to system-wide performance changes, and optimize resource utilization.

**Key Concept:** CloudWatch collects monitoring and operational data in the form of logs, metrics, and events.

## Core Components

### 1. Metrics
**Definition:** Time-ordered set of data points that represent the value of a variable over time

**Default Metrics (Examples):**
- **EC2:** CPU Utilization, Network In/Out, Disk Read/Write
- **RDS:** Database Connections, CPU Utilization, Free Storage Space
- **S3:** Number of Objects, Bucket Size
- **Lambda:** Invocations, Duration, Errors

**Custom Metrics:**
- Application-specific metrics you define
- Business metrics (orders per minute, user logins)
- System metrics from on-premises servers

### 2. Alarms
**Definition:** Watches a single metric and performs actions based on the value relative to a threshold

**Alarm States:**
- **OK** - Metric is within threshold
- **ALARM** - Metric has breached threshold
- **INSUFFICIENT_DATA** - Not enough data to determine state

**Alarm Actions:**
- Send notification to SNS topic
- Auto Scaling actions (scale up/down)
- EC2 actions (stop, terminate, reboot, recover)

### 3. Logs
**Definition:** Monitor, store, and access log files from EC2 instances, CloudTrail, and other sources

**Log Components:**
- **Log Groups** - Collection of log streams with same retention and permissions
- **Log Streams** - Sequence of log events from same source
- **Log Events** - Individual log entries with timestamp and message

### 4. Events (EventBridge)
**Definition:** Stream of system events that describe changes in AWS resources

**Event Sources:**
- AWS services (EC2 state changes, S3 object creation)
- Custom applications
- Third-party SaaS applications

## Key Features

### Real-time Monitoring
- **Live dashboards** with customizable widgets
- **Real-time metrics** updated every minute (or faster)
- **Automatic scaling** based on metrics

### Alerting and Notifications
- **Threshold-based alarms** for proactive monitoring
- **Composite alarms** combining multiple metrics
- **Integration with SNS** for notifications

### Log Analysis
- **CloudWatch Logs Insights** - Query and analyze log data
- **Log retention** - Configurable retention periods
- **Log streaming** - Real-time log processing

### Dashboards
- **Custom dashboards** with multiple widgets
- **Cross-region dashboards** - Monitor resources across regions
- **Shareable dashboards** - Share with team members

## Usage Examples

### Example 1: EC2 CPU Monitoring
```bash
# Create alarm for high CPU utilization
aws cloudwatch put-metric-alarm \
  --alarm-name "High-CPU-Utilization" \
  --alarm-description "Alarm when CPU exceeds 80%" \
  --metric-name CPUUtilization \
  --namespace AWS/EC2 \
  --statistic Average \
  --period 300 \
  --threshold 80 \
  --comparison-operator GreaterThanThreshold \
  --dimensions Name=InstanceId,Value=i-1234567890abcdef0 \
  --evaluation-periods 2
```

### Example 2: Custom Application Metric
```python
import boto3

cloudwatch = boto3.client('cloudwatch')

# Send custom metric
cloudwatch.put_metric_data(
    Namespace='MyApp/Orders',
    MetricData=[
        {
            'MetricName': 'OrdersPerMinute',
            'Value': 25,
            'Unit': 'Count',
            'Dimensions': [
                {
                    'Name': 'Environment',
                    'Value': 'Production'
                }
            ]
        }
    ]
)
```

### Example 3: Log Group Creation
```bash
# Create log group
aws logs create-log-group --log-group-name /aws/lambda/my-function

# Set retention policy (14 days)
aws logs put-retention-policy \
  --log-group-name /aws/lambda/my-function \
  --retention-in-days 14
```

## CloudWatch Agent

### Purpose
- Collect **system-level metrics** from EC2 and on-premises servers
- Collect **application logs** and send to CloudWatch Logs
- More detailed monitoring than default CloudWatch metrics

### Metrics Collected
- **Memory utilization** (not available by default)
- **Disk space utilization**
- **Network metrics per interface**
- **Process-level metrics**

### Configuration
```json
{
  "metrics": {
    "namespace": "CWAgent",
    "metrics_collected": {
      "cpu": {
        "measurement": ["cpu_usage_idle", "cpu_usage_iowait"],
        "metrics_collection_interval": 60
      },
      "disk": {
        "measurement": ["used_percent"],
        "metrics_collection_interval": 60,
        "resources": ["*"]
      },
      "mem": {
        "measurement": ["mem_used_percent"],
        "metrics_collection_interval": 60
      }
    }
  }
}
```

## CloudWatch Logs Insights

### Query Language
```sql
-- Find errors in Lambda logs
fields @timestamp, @message
| filter @message like /ERROR/
| sort @timestamp desc
| limit 20

-- Analyze API Gateway response times
fields @timestamp, @duration
| filter @type = "REPORT"
| stats avg(@duration), max(@duration), min(@duration) by bin(5m)
```

### Common Use Cases
- **Error analysis** - Find and analyze application errors
- **Performance monitoring** - Track response times and latency
- **Security analysis** - Identify suspicious activities
- **Troubleshooting** - Debug application issues

## Pricing

### Metrics
- **Standard metrics** - Free (5-minute frequency)
- **Detailed metrics** - $2.10 per metric per month (1-minute frequency)
- **Custom metrics** - $0.30 per metric per month

### Logs
- **Ingestion** - $0.50 per GB
- **Storage** - $0.03 per GB per month
- **Data transfer** - Standard AWS data transfer rates

### Alarms
- **Standard alarms** - $0.10 per alarm per month
- **High-resolution alarms** - $0.30 per alarm per month

## Integration with Other Services

### Auto Scaling
- **Scale EC2 instances** based on CloudWatch metrics
- **Application Auto Scaling** for other AWS services
- **Predictive scaling** using machine learning

### AWS Lambda
- **Automatic monitoring** of Lambda functions
- **Custom metrics** from Lambda code
- **Log aggregation** from multiple functions

### Amazon SNS
- **Alarm notifications** via email, SMS, HTTP
- **Fan-out messaging** to multiple endpoints
- **Integration with other AWS services**

### AWS Systems Manager
- **Parameter Store** for configuration
- **Run Command** triggered by CloudWatch Events
- **Patch Manager** scheduling

## Best Practices

### Monitoring Strategy
1. **Start with defaults** - Use built-in metrics first
2. **Add custom metrics** for business-specific monitoring
3. **Set meaningful alarms** - Avoid alarm fatigue
4. **Use composite alarms** for complex conditions

### Cost Optimization
1. **Adjust log retention** - Don't keep logs longer than needed
2. **Use log filters** - Only send relevant log data
3. **Monitor custom metrics usage** - Track costs
4. **Archive old logs** to S3 for long-term storage

### Dashboard Design
1. **Focus on key metrics** - Don't overcrowd dashboards
2. **Use appropriate time ranges** - Match business needs
3. **Group related metrics** - Logical organization
4. **Share dashboards** - Promote visibility

## Common Use Cases

### 1. Application Performance Monitoring
- **Response time tracking** across all tiers
- **Error rate monitoring** and alerting
- **Resource utilization** optimization

### 2. Infrastructure Monitoring
- **Server health** and capacity planning
- **Network performance** monitoring
- **Storage utilization** tracking

### 3. Security Monitoring
- **Failed login attempts** detection
- **Unusual API activity** monitoring
- **Resource access patterns** analysis

### 4. Cost Optimization
- **Resource utilization** analysis
- **Idle resource** identification
- **Scaling pattern** optimization

## Key Exam Points

✅ **Monitoring service** - Collects metrics, logs, and events  
✅ **Default metrics** - Provided automatically for AWS services  
✅ **Custom metrics** - Application-specific metrics you define  
✅ **Alarms** - Take actions based on metric thresholds  
✅ **CloudWatch Agent** - Collect system-level metrics and logs  
✅ **Logs Insights** - Query and analyze log data  
✅ **Integration** - Works with Auto Scaling, SNS, Lambda  

## Common Exam Scenarios

**Scenario:** "Need to monitor EC2 memory utilization"  
**Answer:** Install CloudWatch Agent (memory not available by default)

**Scenario:** "Want to scale Auto Scaling Group based on CPU usage"  
**Answer:** Create CloudWatch alarm that triggers Auto Scaling action

**Scenario:** "Need to analyze application logs for errors"  
**Answer:** Use CloudWatch Logs Insights to query log data

**Scenario:** "Want notification when Lambda function errors exceed threshold"  
**Answer:** Create CloudWatch alarm on Lambda error metric with SNS notification

## Practice Questions

**Q: What does CloudWatch monitor by default for EC2 instances?**  
A: CPU utilization, network traffic, disk I/O (but NOT memory)

**Q: How do you monitor memory utilization on EC2?**  
A: Install and configure CloudWatch Agent

**Q: What can CloudWatch alarms trigger?**  
A: SNS notifications, Auto Scaling actions, EC2 actions (stop/terminate/reboot)

**Q: What service is used to query CloudWatch logs?**  
A: CloudWatch Logs Insights
