# AWS Lambda

## What is AWS Lambda?

AWS Lambda is a **serverless compute service** that lets you run code without provisioning or managing servers. You pay only for the compute time you consume - there's no charge when your code isn't running.

**Key Concept:** Lambda follows the "Function as a Service" (FaaS) model - you upload your code and Lambda handles everything required to run and scale your code with high availability.

## Core Components

### 1. Functions
**Definition:** A resource that contains your code and configuration information

**Function Components:**
- **Code** - Your application logic (up to 50 MB zipped)
- **Runtime** - Language-specific environment (Python, Node.js, Java, etc.)
- **Handler** - Entry point method in your code
- **Configuration** - Memory, timeout, environment variables

### 2. Event Sources
**Definition:** AWS services or custom applications that trigger Lambda functions

**Common Event Sources:**
- **API Gateway** - HTTP requests trigger functions
- **S3** - Object creation/deletion events
- **DynamoDB** - Stream events from table changes
- **CloudWatch Events/EventBridge** - Scheduled or event-driven triggers
- **SQS** - Message queue processing
- **SNS** - Notification processing

### 3. Execution Environment
**Definition:** Secure, isolated runtime environment for your function

**Environment Features:**
- **Automatic scaling** - Handles concurrent executions
- **Built-in monitoring** - CloudWatch integration
- **Security isolation** - Each function runs in separate environment
- **Temporary storage** - 512 MB to 10 GB in /tmp directory

## Key Features ⭐ **EXAM FOCUS**

### Serverless Architecture
- **No server management** - AWS handles infrastructure
- **Automatic scaling** - From zero to thousands of concurrent executions
- **High availability** - Built-in fault tolerance and redundancy
- **Pay-per-use** - Only pay for actual compute time

### Event-Driven Processing
- **Real-time processing** - Respond to events as they occur
- **Asynchronous execution** - Handle events without blocking
- **Integration** - Works with 200+ AWS services
- **Batch processing** - Process multiple records efficiently

### Built-in Security
- **IAM integration** - Fine-grained access control
- **VPC support** - Access private resources securely
- **Encryption** - Data encrypted in transit and at rest
- **Environment variables** - Secure configuration management

## Usage Examples

### Example 1: S3 Image Processing
```python
import json
import boto3
from PIL import Image

def lambda_handler(event, context):
    # Get S3 event details
    bucket = event['Records'][0]['s3']['bucket']['name']
    key = event['Records'][0]['s3']['object']['key']
    
    # Process image (resize, compress, etc.)
    # Upload processed image back to S3
    
    return {
        'statusCode': 200,
        'body': json.dumps('Image processed successfully')
    }
```

### Example 2: API Gateway Integration
```python
import json

def lambda_handler(event, context):
    # Extract request data
    http_method = event['httpMethod']
    path = event['path']
    body = json.loads(event['body']) if event['body'] else {}
    
    # Business logic
    if http_method == 'GET':
        response_body = {'message': 'Hello from Lambda!'}
    else:
        response_body = {'error': 'Method not allowed'}
    
    return {
        'statusCode': 200,
        'headers': {
            'Content-Type': 'application/json',
            'Access-Control-Allow-Origin': '*'
        },
        'body': json.dumps(response_body)
    }
```

### Example 3: Scheduled Task
```python
import boto3
import json

def lambda_handler(event, context):
    # Scheduled function (e.g., daily cleanup)
    s3 = boto3.client('s3')
    
    # Delete old files from S3 bucket
    # Send notification email
    # Update database records
    
    return {
        'statusCode': 200,
        'body': json.dumps('Scheduled task completed')
    }
```

## Supported Runtimes

### Programming Languages
- **Python** - 3.8, 3.9, 3.10, 3.11
- **Node.js** - 16.x, 18.x, 20.x
- **Java** - 8, 11, 17, 21
- **C#** - .NET Core 3.1, .NET 6, .NET 8
- **Go** - 1.x
- **Ruby** - 2.7, 3.2
- **Custom Runtime** - Any language using Runtime API

### Container Images
- **Docker containers** up to 10 GB
- **Base images** provided by AWS
- **Custom base images** supported
- **Multi-architecture** support (x86_64, arm64)

## Pricing ⭐ **EXAM FOCUS**

### Request Pricing
- **Free tier** - 1 million requests per month
- **Additional requests** - $0.20 per 1 million requests

### Duration Pricing
- **Free tier** - 400,000 GB-seconds per month
- **Additional duration** - $0.0000166667 per GB-second

### Example Cost Calculation
```
Function: 128 MB memory, 100ms execution time
Monthly executions: 3 million

Request charges: (3M - 1M free) × $0.20/1M = $0.40
Duration charges: 3M × 0.1s × 0.125GB = 37,500 GB-seconds
Duration cost: (37,500 - 400,000 free) = $0 (within free tier)

Total monthly cost: $0.40
```

## Integration with Other Services

### API Gateway
- **RESTful APIs** - Create HTTP endpoints
- **WebSocket APIs** - Real-time communication
- **Request/response** transformation
- **Authentication** and authorization

### S3
- **Event notifications** - Object creation/deletion triggers
- **Data processing** - Image resizing, file conversion
- **Backup automation** - Automated backup workflows

### DynamoDB
- **Stream processing** - React to table changes
- **Data validation** - Validate records before insertion
- **Aggregation** - Calculate metrics from table data

### CloudWatch
- **Automatic monitoring** - Built-in metrics and logs
- **Custom metrics** - Application-specific monitoring
- **Alarms** - Alert on function errors or performance

## Best Practices

### Performance Optimization
1. **Right-size memory** - More memory = faster CPU and network
2. **Minimize cold starts** - Keep functions warm with provisioned concurrency
3. **Optimize dependencies** - Include only necessary libraries
4. **Use connection pooling** - Reuse database connections

### Cost Optimization
1. **Monitor usage** - Use CloudWatch to track costs
2. **Optimize memory allocation** - Find the sweet spot for performance/cost
3. **Set appropriate timeouts** - Avoid paying for hung functions
4. **Use Savings Plans** - For predictable workloads

### Security Best Practices
1. **Least privilege IAM** - Grant minimal required permissions
2. **Environment variables** - Store sensitive configuration securely
3. **VPC configuration** - Access private resources when needed
4. **Input validation** - Validate all incoming data

### Error Handling
1. **Dead letter queues** - Handle failed executions
2. **Retry logic** - Implement exponential backoff
3. **Monitoring** - Set up CloudWatch alarms
4. **Logging** - Use structured logging for debugging

## Common Use Cases ⭐ **EXAM FOCUS**

### 1. Web Applications
- **API backends** - RESTful services with API Gateway
- **Authentication** - User login and authorization
- **Data processing** - Form submissions and validation
- **File uploads** - Process uploaded files

### 2. Data Processing
- **ETL pipelines** - Extract, transform, load data
- **Real-time analytics** - Process streaming data
- **Image/video processing** - Resize, compress, convert media
- **Log analysis** - Parse and analyze log files

### 3. Automation and Operations
- **Infrastructure automation** - Start/stop EC2 instances
- **Backup automation** - Scheduled backup tasks
- **Monitoring** - Custom health checks and alerts
- **Compliance** - Automated compliance checking

### 4. IoT and Mobile
- **IoT data processing** - Handle sensor data streams
- **Mobile backends** - API services for mobile apps
- **Push notifications** - Send notifications to devices
- **Real-time messaging** - Chat and messaging systems

## Limitations and Considerations

### Execution Limits
- **Maximum execution time** - 15 minutes
- **Memory allocation** - 128 MB to 10,008 MB
- **Temporary disk space** - 512 MB to 10 GB
- **Concurrent executions** - 1,000 (default, can be increased)

### Cold Starts
- **Definition** - Delay when function hasn't run recently
- **Impact** - Additional latency for first request
- **Mitigation** - Provisioned concurrency, keep functions warm

### Stateless Nature
- **No persistent storage** - Use external storage (S3, DynamoDB)
- **No guaranteed execution order** - Design for eventual consistency
- **Connection limits** - Manage database connections carefully

## Key Exam Points

✅ **Serverless compute** - No server management required  
✅ **Pay-per-use** - Only pay for actual execution time  
✅ **Event-driven** - Triggered by AWS services or custom events  
✅ **Automatic scaling** - Handles concurrent executions automatically  
✅ **15-minute maximum** - Functions timeout after 15 minutes  
✅ **Integration** - Works with 200+ AWS services  
✅ **Built-in monitoring** - CloudWatch logs and metrics included  

## Common Exam Scenarios

**Scenario:** "Need to process images uploaded to S3 bucket"  
**Answer:** Use Lambda function triggered by S3 events

**Scenario:** "Want to create RESTful API without managing servers"  
**Answer:** Use API Gateway with Lambda functions

**Scenario:** "Need to run code only when specific events occur"  
**Answer:** Lambda with appropriate event sources (S3, DynamoDB, etc.)

**Scenario:** "Want to automate daily backup tasks"  
**Answer:** Lambda function triggered by CloudWatch Events on schedule

**Scenario:** "Application needs to scale automatically based on demand"  
**Answer:** Lambda automatically scales based on incoming requests

## Practice Questions

**Q: What is the maximum execution time for a Lambda function?**  
A: 15 minutes

**Q: How does Lambda pricing work?**  
A: Pay per request and compute time (GB-seconds)

**Q: What happens when a Lambda function receives more requests than it can handle?**  
A: Lambda automatically scales by creating additional concurrent executions

**Q: Which AWS service is commonly used with Lambda to create RESTful APIs?**  
A: Amazon API Gateway

**Q: What is a "cold start" in Lambda?**  
A: The delay that occurs when a function hasn't been used recently and needs to initialize