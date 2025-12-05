# Data Encryption in AWS

## Encryption in Transit vs Encryption at Rest

### Encryption in Transit
**Definition:** Protects data while it moves between locations (client to server, server to server)

**AWS Methods:**
- **SSL/TLS** - Primary method for encrypting data in transit
- **HTTPS** - HTTP over SSL/TLS
- **VPN connections** - Encrypted tunnels for network traffic
- **AWS PrivateLink** - Private connectivity without internet exposure

### Encryption at Rest
**Definition:** Protects stored data on disks, databases, and storage services

**AWS Methods:**
- **S3 Server-Side Encryption (SSE)**
- **EBS Encryption**
- **RDS Encryption**
- **AWS KMS** - Key management service

## SSL/TLS Deep Dive

### What is SSL/TLS?
- **SSL (Secure Sockets Layer)** - Legacy protocol
- **TLS (Transport Layer Security)** - Modern successor to SSL
- Creates encrypted connection between client and server
- Ensures data integrity and authentication

### How SSL/TLS Works:
1. **Handshake:** Client and server negotiate encryption parameters
2. **Certificate Exchange:** Server presents digital certificate
3. **Key Exchange:** Symmetric encryption key is established
4. **Encrypted Communication:** All data encrypted with shared key

### AWS Services Using SSL/TLS:
- **CloudFront** - HTTPS delivery
- **Application Load Balancer** - SSL termination
- **API Gateway** - HTTPS endpoints
- **ElastiCache** - Encryption in transit
- **RDS** - SSL connections to databases

## Common Encryption Scenarios

### Web Applications
```
Client Browser --[HTTPS/TLS]--> CloudFront --[HTTPS]--> ALB --[HTTP/HTTPS]--> EC2
```

### Database Connections
```
Application --[SSL/TLS]--> RDS Database
```

### API Communications
```
Mobile App --[HTTPS]--> API Gateway --[HTTPS]--> Lambda
```

## Key Exam Points

✅ **SSL/TLS encrypts data in transit**  
✅ **HTTPS = HTTP + SSL/TLS**  
✅ **AWS Certificate Manager (ACM) provides free SSL certificates**  
✅ **Most AWS services support encryption in transit by default**  
✅ **Always use HTTPS for web applications**

## Related AWS Services

| Service | Purpose |
|---------|---------|
| AWS Certificate Manager (ACM) | Provision and manage SSL/TLS certificates |
| AWS KMS | Key management for encryption |
| AWS CloudHSM | Hardware security modules |
| AWS Shield | DDoS protection (not encryption) |
| AWS WAF | Web application firewall (not encryption) |

## Practice Questions

**Q: What protects data while it travels over the network?**  
A: SSL/TLS encryption (encryption in transit)

**Q: Which AWS service provides free SSL certificates?**  
A: AWS Certificate Manager (ACM)

**Q: What's the difference between SSL and TLS?**  
A: TLS is the modern, more secure successor to SSL
