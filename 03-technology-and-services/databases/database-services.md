# AWS Database Services Comparison

## Database Categories

### Relational Databases (SQL)
- **Amazon RDS** - Managed relational database service
- **Amazon Aurora** - High-performance MySQL/PostgreSQL compatible

### NoSQL Databases
- **Amazon DynamoDB** - Key-value and document database
- **Amazon DocumentDB** - MongoDB-compatible document database
- **Amazon Neptune** - Graph database

### In-Memory Databases
- **Amazon ElastiCache** - Redis and Memcached caching
- **Amazon MemoryDB** - Redis-compatible in-memory database

## Detailed Service Comparison

### Amazon DynamoDB ⭐ **EXAM FOCUS**
**Type:** NoSQL (Key-Value & Document)  
**Performance:** **Sub-millisecond latency** at scale  
**Scaling:** Automatic, serverless  
**Use Cases:** Web applications, gaming, mobile backends, real-time analytics

**Key Features:**
- Fully managed NoSQL database
- Single-digit millisecond performance
- Built-in security, backup, and restore
- Global tables for multi-region replication
- On-demand and provisioned billing modes

**When to Use:**
- Need sub-millisecond response times
- Unpredictable or variable workloads
- Serverless applications
- High-scale web applications

### Amazon RDS
**Type:** Relational (SQL)  
**Engines:** MySQL, PostgreSQL, MariaDB, Oracle, SQL Server  
**Performance:** Depends on instance type  
**Scaling:** Vertical (instance size) and horizontal (read replicas)

**Key Features:**
- Managed relational database service
- Automated backups and patching
- Multi-AZ deployments for high availability
- Read replicas for scaling read workloads
- Point-in-time recovery

**When to Use:**
- Need ACID transactions
- Complex queries and joins
- Existing SQL applications
- Structured data with relationships

### Amazon Aurora
**Type:** Relational (MySQL/PostgreSQL compatible)  
**Performance:** Up to 5x faster than MySQL, 3x faster than PostgreSQL  
**Scaling:** Auto-scaling storage, up to 15 read replicas

**Key Features:**
- Cloud-native relational database
- Automatic storage scaling (up to 128 TB)
- Continuous backup to S3
- Global database for cross-region replication
- Serverless option available

**When to Use:**
- High-performance relational database needs
- Need MySQL/PostgreSQL compatibility
- Global applications requiring low latency

### Amazon DocumentDB
**Type:** Document (MongoDB-compatible)  
**Performance:** Optimized for document workloads  
**Scaling:** Automatic storage scaling, up to 15 read replicas

**Key Features:**
- MongoDB-compatible document database
- Fully managed and serverless options
- Automatic scaling and backup
- VPC isolation for security

**When to Use:**
- MongoDB applications
- JSON document storage
- Content management systems
- Catalog applications

### Amazon Neptune
**Type:** Graph Database  
**Performance:** Optimized for graph queries  
**Scaling:** Up to 15 read replicas

**Key Features:**
- Fully managed graph database
- Supports Apache TinkerPop Gremlin and W3C SPARQL
- High availability with read replicas
- Continuous backup to S3

**When to Use:**
- Social networks
- Recommendation engines
- Fraud detection
- Knowledge graphs

## Quick Comparison Table

| Service | Type | Latency | Best For |
|---------|------|---------|----------|
| **DynamoDB** | NoSQL | **Sub-millisecond** | High-scale web apps, gaming |
| **RDS** | SQL | Milliseconds | Traditional applications, complex queries |
| **Aurora** | SQL | Milliseconds | High-performance relational needs |
| **DocumentDB** | Document | Milliseconds | MongoDB applications, JSON data |
| **Neptune** | Graph | Milliseconds | Social networks, recommendations |

## Key Exam Points

✅ **DynamoDB = NoSQL + Sub-millisecond latency**  
✅ **Aurora = High-performance MySQL/PostgreSQL**  
✅ **RDS = Traditional relational databases**  
✅ **DocumentDB = MongoDB-compatible**  
✅ **Neptune = Graph database**  
✅ **ElastiCache = In-memory caching (Redis/Memcached)**

## Performance Characteristics

### Latency Rankings (Fastest to Slowest):
1. **ElastiCache** - Microseconds (in-memory)
2. **DynamoDB** - Sub-millisecond
3. **Aurora** - Low milliseconds
4. **RDS** - Milliseconds
5. **DocumentDB** - Milliseconds
6. **Neptune** - Milliseconds (depends on query complexity)

## Common Exam Scenarios

**Scenario:** "Need a database with sub-millisecond latency for a gaming application"  
**Answer:** DynamoDB

**Scenario:** "Migrating existing MySQL application to AWS"  
**Answer:** RDS for MySQL or Aurora MySQL

**Scenario:** "Need to store and query social network relationships"  
**Answer:** Neptune (graph database)

**Scenario:** "MongoDB application needs to run on AWS"  
**Answer:** DocumentDB

**Scenario:** "Need caching layer for web application"  
**Answer:** ElastiCache

## Practice Questions

**Q: Which database service provides sub-millisecond latency?**  
A: Amazon DynamoDB

**Q: What type of database is Amazon Neptune?**  
A: Graph database

**Q: Which service is MongoDB-compatible?**  
A: Amazon DocumentDB
