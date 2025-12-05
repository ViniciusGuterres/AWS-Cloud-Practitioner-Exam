# AWS EventBridge

## What is AWS EventBridge?

AWS EventBridge is a **serverless event bus service** that makes it easy to connect applications using data from your own applications, integrated Software-as-a-Service (SaaS) applications, and AWS services.

**Key Concept:** EventBridge enables event-driven architectures by routing events between event sources and targets based on rules you define.

## Core Components

### 1. Events
**Definition:** A signal that a system's state has changed, represented as a JSON object

**Event Structure:**
```json
{
  "version": "0",
  "id": "unique-event-id",
  "detail-type": "EC2 Instance State-change Notification",
  "source": "aws.ec2",
  "account": "123456789012",
  "time": "2023-10-22T13:38:09Z",
  "region": "us-east-1",
  "detail": {
    "instance-id": "i-1234567890abcdef0",
    "state": "running"
  }
}
```

### 2. Event Buses
**Definition:** A pipeline that receives events and delivers them to targets based on rules

**Types of Event Buses:**
- **Default Event Bus** - Receives events from AWS services
- **Custom Event Bus** - For your applications and third-party SaaS
- **Partner Event Bus** - For SaaS partner integrations

### 3. Rules
**Definition:** Match incoming events and route them to targets for processing

**Rule Components:**
- **Event Pattern** - Defines which events to match
- **Schedule** - Time-based rules (cron or rate expressions)
- **Targets** - Where to send matched events

### 4. Targets
**Definition:** Resources that process events when rules are triggered

**Supported Targets:**
- AWS Lambda functions
- Amazon SQS queues
- Amazon SNS topics
- Amazon Kinesis streams
- AWS Step Functions
- Amazon ECS tasks
- AWS Batch jobs

## Key Features

### Event-Driven Architecture
- **Loose coupling** between event producers and consumers
- **Scalable processing** of events
- **Real-time event routing** with low latency

### Schema Registry
- **Event schema discovery** and management
- **Code generation** for strongly-typed event handling
- **Schema evolution** tracking and versioning

### Content Filtering
- **Event pattern matching** based on event content
- **Prefix matching** for flexible filtering
- **Numeric matching** with ranges and operators

### Replay and Archive
- **Event replay** from archived events
- **Event archiving** for compliance and debugging
- **Point-in-time recovery** capabilities

## Usage Examples

### Example 1: EC2 State Change Processing
```json
{
  "Rules": [
    {
      "Name": "EC2StateChangeRule",
      "EventPattern": {
        "source": ["aws.ec2"],
        "detail-type": ["EC2 Instance State-change Notification"],
        "detail": {
          "state": ["running", "stopped"]
        }
      },
      "Targets": [
        {
          "Id": "1",
          "Arn": "arn:aws:lambda:us-east-1:123456789012:function:ProcessEC2StateChange"
        }
      ]
    }
  ]
}
```

### Example 2: Custom Application Events
```python
import boto3
import json

eventbridge = boto3.client('events')

# Send custom event
response = eventbridge.put_events(
    Entries=[
        {
            'Source': 'myapp.orders',
            'DetailType': 'Order Placed',
            'Detail': json.dumps({
                'orderId': '12345',
                'customerId': 'cust-67890',
                'amount': 99.99,
                'status': 'confirmed'
            }),
            'EventBusName': 'custom-event-bus'
        }
    ]
)
```

### Example 3: Scheduled Events
```bash
# Create scheduled rule (every 5 minutes)
aws events put-rule \
  --name "ScheduledRule" \
  --schedule-expression "rate(5 minutes)" \
  --description "Trigger Lambda every 5 minutes"

# Add Lambda target
aws events put-targets \
  --rule "ScheduledRule" \
  --targets "Id"="1","Arn"="arn:aws:lambda:us-east-1:123456789012:function:ScheduledTask"
```

## Event Sources

### AWS Services
- **Amazon EC2** - Instance state changes, EBS volume events
- **Amazon S3** - Object creation, deletion, restoration
- **AWS CloudTrail** - API call logging and monitoring
- **Amazon RDS** - Database events and notifications
- **AWS CodePipeline** - Pipeline state changes
- **Amazon ECS** - Task and service state changes

### SaaS Partners
- **Salesforce** - CRM events and updates
- **Zendesk** - Support ticket events
- **Shopify** - E-commerce events
- **Auth0** - Authentication events
- **PagerDuty** - Incident management events

### Custom Applications
- **Microservices** - Service-to-service communication
- **Mobile apps** - User interaction events
- **IoT devices** - Sensor data and telemetry
- **Web applications** - User activity tracking

## Event Patterns

### Basic Pattern Matching
```json
{
  "source": ["aws.ec2"],
  "detail-type": ["EC2 Instance State-change Notification"]
}
```

### Content-Based Filtering
```json
{
  "source": ["myapp.orders"],
  "detail": {
    "amount": [{"numeric": [">", 100]}],
    "region": ["us-east-1", "us-west-2"],
    "status": ["confirmed"]
  }
}
```

### Prefix Matching
```json
{
  "detail": {
    "eventName": [{"prefix": "Describe"}]
  }
}
```

## Schema Registry

### Schema Discovery
- **Automatic discovery** of event schemas
- **Schema inference** from event samples
- **Version management** for schema evolution

### Code Generation
```bash
# Generate code bindings
aws schemas get-code-binding-source \
  --registry-name discovered-schemas \
  --schema-name aws.ec2@EC2InstanceStateChangeNotification \
  --language Java8
```

### Schema Validation
- **Event validation** against registered schemas
- **Breaking change detection** in schema updates
- **Compatibility checking** between versions

## Pricing

### Event Processing
- **$1.00 per million events** published to custom event bus
- **Free tier** - 100 million events per month on default event bus
- **No charge** for AWS service events on default bus

### Schema Registry
- **$1.00 per million schema requests**
- **$0.10 per schema per month** for storage
- **Free tier** - 5 million requests and 10 schemas per month

### Replays
- **$0.10 per million events** replayed
- **Storage costs** for archived events

## Integration with Other Services

### AWS Lambda
- **Event-driven function execution**
- **Automatic scaling** based on event volume
- **Dead letter queue** support for failed invocations

### Amazon SQS
- **Reliable event delivery** with message queuing
- **Batch processing** of events
- **Message deduplication** for exactly-once processing

### AWS Step Functions
- **Workflow orchestration** triggered by events
- **Complex business logic** execution
- **State management** across multiple services

### Amazon SNS
- **Fan-out messaging** to multiple subscribers
- **Mobile push notifications**
- **Email and SMS** notifications

## Best Practices

### Event Design
1. **Use descriptive event names** - Clear detail-type values
2. **Include relevant context** - Sufficient detail for processing
3. **Keep events immutable** - Don't modify event content
4. **Use consistent schema** - Standardize event structure

### Rule Management
1. **Start with broad patterns** - Refine as needed
2. **Use multiple targets** - Distribute processing load
3. **Monitor rule metrics** - Track invocation success/failure
4. **Test event patterns** - Validate before production

### Error Handling
1. **Configure dead letter queues** - Handle failed events
2. **Set retry policies** - Automatic retry with backoff
3. **Monitor target health** - Ensure targets are available
4. **Use input transformers** - Format events for targets

### Security
1. **Use IAM policies** - Control access to event buses
2. **Encrypt sensitive data** - Use KMS for event encryption
3. **Validate event sources** - Verify event authenticity
4. **Monitor access patterns** - Detect unusual activity

## Common Use Cases

### 1. Microservices Communication
- **Service decoupling** through event-driven messaging
- **Asynchronous processing** of business events
- **Event sourcing** for audit trails

### 2. Real-time Data Processing
- **Stream processing** of IoT sensor data
- **Real-time analytics** on user interactions
- **Fraud detection** based on transaction patterns

### 3. Application Integration
- **SaaS application** integration and synchronization
- **Legacy system** modernization with events
- **Multi-cloud** event routing and processing

### 4. Operational Automation
- **Infrastructure monitoring** and automated responses
- **Security incident** detection and remediation
- **Compliance reporting** and audit automation

## Key Exam Points

✅ **Serverless event bus** - No infrastructure to manage  
✅ **Event-driven architecture** - Loose coupling between components  
✅ **Multiple event sources** - AWS services, SaaS, custom apps  
✅ **Rule-based routing** - Events routed based on patterns  
✅ **Schema registry** - Event schema management and discovery  
✅ **Integration targets** - Lambda, SQS, SNS, Step Functions  

## Common Exam Scenarios

**Scenario:** "Need to trigger Lambda when EC2 instance state changes"  
**Answer:** Create EventBridge rule matching EC2 state change events with Lambda target

**Scenario:** "Want to integrate Salesforce events with AWS applications"  
**Answer:** Use EventBridge partner event bus for Salesforce integration

**Scenario:** "Need to process events from multiple microservices"  
**Answer:** Create custom event bus with rules routing to appropriate targets

**Scenario:** "Want to schedule Lambda function to run every hour"  
**Answer:** Create EventBridge rule with schedule expression and Lambda target

## Practice Questions

**Q: What is the difference between EventBridge and CloudWatch Events?**  
A: EventBridge is the evolution of CloudWatch Events with additional features like SaaS integration and schema registry

**Q: How do you filter events in EventBridge?**  
A: Use event patterns in rules to match specific event content and route to targets

**Q: What happens if an EventBridge target fails to process an event?**  
A: Configure dead letter queues and retry policies to handle failed events

**Q: Can EventBridge handle events from third-party SaaS applications?**  
A: Yes, through partner event buses and SaaS partner integrations
