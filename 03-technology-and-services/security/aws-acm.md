# AWS Certificate Manager (ACM)

## Service Overview

AWS Certificate Manager (ACM) is a fully managed service that provisions, manages, and deploys public and private SSL/TLS certificates for use with AWS services and internal resources at no additional cost.

### 💡 Foundational Concepts

**What Problem Does It Solve?**

Websites and applications need SSL/TLS certificates to enable HTTPS connections, which:
- Encrypt data in transit between users and servers
- Verify the identity of websites (prevent impersonation)
- Build user trust (browsers show padlock icon)
- Meet compliance requirements (PCI-DSS, HIPAA)

Traditional certificate management is complex and costly:
- **Purchase certificates** from Certificate Authorities (CAs) - costs $50-$500+ per year
- **Manual installation** on web servers and load balancers
- **Track expiration dates** and renew before they expire (causes outages if forgotten)
- **Reissue and redeploy** certificates across multiple servers
- **Manage private keys** securely

**Core Value Proposition:**

AWS Certificate Manager eliminates the cost and complexity of SSL/TLS certificate management. ACM provides free public certificates for AWS services, automatically renews them before expiration, and handles all the technical details of certificate deployment. You never have to worry about certificate expiration causing website outages.

**Simple Analogy:** Think of ACM as an automated passport office for your websites. Instead of manually applying for passports (certificates), tracking expiration dates, and renewing them yourself, ACM automatically issues, renews, and updates your website's "passport" so it can securely communicate with visitors—all for free.

### 🌐 Key Benefits & Value Proposition

**1. Free Public SSL/TLS Certificates (Cost Optimization)**
- No cost for public certificates used with AWS services
- Eliminates annual certificate purchase fees ($50-$500+ per certificate)
- Unlimited certificates at no charge
- **Cloud Advantage:** *Cost savings* - Zero certificate costs compared to traditional CAs

**2. Automatic Certificate Renewal (Operational Excellence)**
- ACM automatically renews certificates before expiration
- No manual intervention required
- Prevents website outages from expired certificates
- **Cloud Advantage:** *Automation* - Eliminates manual renewal processes and human error

**3. Simplified Certificate Management**
- Single console to manage all certificates
- Automatic deployment to integrated AWS services
- No need to generate Certificate Signing Requests (CSRs)
- **Cloud Advantage:** *Centralized management* - Unified view of all certificates

**4. Seamless AWS Integration**
- Works natively with CloudFront, Application Load Balancer, API Gateway, and more
- Automatic certificate deployment to integrated services
- No manual installation or configuration required
- **Cloud Advantage:** *Built-in integration* - One-click certificate deployment

**5. Enhanced Security**
- Private keys managed securely by AWS (never exposed)
- Certificates stored in AWS-managed infrastructure
- Automatic security best practices applied
- **Cloud Advantage:** *Security at scale* - Enterprise-grade certificate security

### 🔒 Security and Compliance (CLF-C02 Focus)

**AWS Shared Responsibility Model:**

| **AWS Responsibility (Security OF the Cloud)** | **Customer Responsibility (Security IN the Cloud)** |
|---|---|
| ✅ Physical security of ACM infrastructure | ✅ Request and configure certificates |
| ✅ Certificate issuance and validation | ✅ Validate domain ownership (email or DNS) |
| ✅ Private key generation and storage | ✅ Associate certificates with AWS resources |
| ✅ Automatic certificate renewal | ✅ Configure DNS records for domain validation |
| ✅ Certificate revocation capabilities | ✅ Monitor certificate expiration (imported certificates) |
| ✅ Encryption of private keys at rest | ✅ Manage IAM permissions for ACM access |
| ✅ Service availability and durability | ✅ Delete unused certificates |
| ✅ Compliance with CA/Browser Forum requirements | ✅ Use appropriate certificate types for use cases |

**Key Security Features:**

- **Private Key Protection:** Private keys generated and stored securely by AWS, never exposed to customers
- **Automatic Validation:** Domain ownership validated via email or DNS before certificate issuance
- **Managed Renewal:** Certificates automatically renewed 60 days before expiration
- **Encryption in Transit:** All certificates enable HTTPS/TLS encryption
- **IAM Integration:** Fine-grained access control for certificate management
- **CloudTrail Logging:** All ACM API calls logged for audit

**Certificate Types:**

**1. Public Certificates (Free)**
- Issued by Amazon Trust Services (AWS's Certificate Authority)
- Trusted by all major browsers and operating systems
- Used for public-facing websites and applications
- Automatic renewal
- **Use Case:** CloudFront distributions, Application Load Balancers, API Gateway

**2. Private Certificates (Paid)**
- Issued by AWS Private Certificate Authority (Private CA)
- Used for internal applications and resources
- Not trusted by public browsers (internal use only)
- Requires AWS Private CA ($400/month)
- **Use Case:** Internal APIs, microservices, IoT devices

**3. Imported Certificates (Free to Store)**
- Certificates obtained from third-party CAs
- Imported into ACM for centralized management
- Manual renewal required (ACM doesn't auto-renew imported certificates)
- **Use Case:** Existing certificates from other CAs

**Domain Validation Methods:**

**Email Validation:**
- ACM sends validation email to domain owner
- Click link in email to validate ownership
- Simple but requires email access

**DNS Validation (Recommended):**
- Add CNAME record to DNS configuration
- Automatic validation when DNS record detected
- Supports automatic renewal
- Better for automation and CI/CD pipelines

**Compliance Support:**
- Helps meet PCI-DSS requirements (HTTPS encryption)
- Supports HIPAA compliance (data in transit encryption)
- Meets SOC, ISO 27001 standards
- GDPR compliance for data protection

### 💰 Billing, Pricing, and Support

**Pricing Model: Free for Public Certificates**

**1. Public SSL/TLS Certificates:**
- **FREE** - No charge for public certificates
- **FREE** - Unlimited certificates
- **FREE** - Automatic renewal
- **FREE** - No charge for certificate requests or renewals
- Only usable with integrated AWS services (CloudFront, ALB, API Gateway, etc.)

**2. Private Certificates:**
- Requires **AWS Private Certificate Authority (Private CA)**
- **$400 per month** per Private CA
- **$0.75 per private certificate** issued per month
- Used for internal applications and resources

**3. Imported Certificates:**
- **FREE** to import and store in ACM
- **FREE** to use with AWS services
- Manual renewal required (not automatic)

**Cost Comparison:**

| Scenario | Traditional CA Cost | ACM Cost | Annual Savings |
|----------|-------------------|----------|----------------|
| 1 public certificate | $100/year | $0 | $100 |
| 10 public certificates | $1,000/year | $0 | $1,000 |
| 100 public certificates | $10,000/year | $0 | $10,000 |

**Important Pricing Notes:**

✅ **Free for AWS-integrated services:** CloudFront, ALB, NLB, API Gateway, Elastic Beanstalk  
❌ **Cannot export:** Public certificates cannot be exported for use on EC2 instances or on-premises servers  
❌ **Not for EC2:** Cannot install ACM public certificates directly on EC2 instances (use ALB instead)

**Cost Optimization Tips:**
- Use ACM public certificates instead of purchasing from third-party CAs
- Consolidate multiple subdomains under wildcard certificates (*.example.com)
- Use ACM with CloudFront for global HTTPS delivery at no certificate cost
- Avoid Private CA unless you need internal certificates ($400/month)

**Support:**
- Available under all AWS Support Plans
- 24/7 support for Business and Enterprise plans
- Extensive documentation and tutorials
- Community forums and AWS re:Post

### 🎯 Common Use Cases (Scenario-Based)

**1. Secure Website with HTTPS (CloudFront + S3)**
- **Scenario:** A company hosts a static website on S3 and wants to enable HTTPS with a custom domain (www.example.com).
- **Solution:** Request a free public certificate from ACM for www.example.com, create a CloudFront distribution, and associate the ACM certificate.
- **Benefit:** Free HTTPS encryption, automatic certificate renewal, improved SEO (Google ranks HTTPS sites higher), user trust.

**2. Load Balanced Web Application**
- **Scenario:** An e-commerce application runs on multiple EC2 instances behind an Application Load Balancer and needs HTTPS encryption.
- **Solution:** Request an ACM certificate for the domain, attach it to the Application Load Balancer listener (port 443).
- **Benefit:** Centralized SSL termination at the load balancer, free certificate, automatic renewal, no certificate management on EC2 instances.

**3. Secure REST API**
- **Scenario:** A mobile app backend uses API Gateway to expose REST APIs and requires HTTPS with a custom domain (api.example.com).
- **Solution:** Request an ACM certificate for api.example.com, create a custom domain in API Gateway, and associate the certificate.
- **Benefit:** Secure API communication, professional custom domain, free certificate, automatic renewal.

**4. Multi-Region Application with Wildcard Certificate**
- **Scenario:** A global SaaS application has subdomains for different services (app.example.com, api.example.com, admin.example.com) across multiple regions.
- **Solution:** Request a wildcard ACM certificate (*.example.com) that covers all subdomains, deploy to CloudFront distributions in multiple regions.
- **Benefit:** Single certificate for all subdomains, simplified management, cost savings (one certificate instead of many).

**5. Migrating from Third-Party Certificates**
- **Scenario:** A company currently pays $200/year for SSL certificates from a third-party CA and wants to reduce costs.
- **Solution:** Request free ACM certificates for all domains, migrate applications to use ACM certificates, cancel third-party CA subscriptions.
- **Benefit:** Eliminate annual certificate costs, automatic renewal, simplified management.

### 🔗 Related Core Services

**1. Amazon CloudFront (Content Delivery Network)**
- **Relationship:** CloudFront uses ACM certificates to enable HTTPS for content delivery
- **Integration:** Attach ACM certificates to CloudFront distributions for custom domain HTTPS
- **CLF-C02 Context:** CloudFront delivers content globally; ACM provides SSL/TLS certificates for secure delivery

**2. Elastic Load Balancing (Application Load Balancer)**
- **Relationship:** ALB uses ACM certificates for SSL/TLS termination
- **Integration:** Attach ACM certificates to ALB HTTPS listeners (port 443)
- **CLF-C02 Context:** ALB distributes traffic; ACM provides certificates for encrypted connections

**3. Amazon API Gateway**
- **Relationship:** API Gateway uses ACM certificates for custom domain HTTPS
- **Integration:** Associate ACM certificates with API Gateway custom domains
- **CLF-C02 Context:** API Gateway exposes APIs; ACM secures API endpoints with HTTPS

**4. AWS Route 53 (DNS Service)**
- **Relationship:** Route 53 manages DNS records required for ACM domain validation
- **Integration:** Add CNAME records in Route 53 for ACM DNS validation
- **CLF-C02 Context:** Route 53 routes traffic; ACM validates domain ownership via DNS

**5. AWS Identity and Access Management (IAM)**
- **Relationship:** IAM controls who can request, manage, and delete ACM certificates
- **Integration:** IAM policies define permissions for ACM operations
- **CLF-C02 Context:** IAM provides access control; ACM provides certificate management

**6. AWS CloudTrail**
- **Relationship:** CloudTrail logs all ACM API calls for audit and compliance
- **Integration:** Automatic logging of certificate requests, renewals, deletions, and associations
- **CLF-C02 Context:** CloudTrail provides audit trail; ACM provides certificate operations to audit

**7. Amazon S3 + CloudFront**
- **Relationship:** Common architecture for static website hosting with HTTPS
- **Integration:** S3 stores website files, CloudFront delivers with HTTPS using ACM certificate
- **CLF-C02 Context:** S3 stores content; CloudFront delivers it; ACM secures the connection

### 📊 ACM Certificate Types Comparison

**Quick Reference for CLF-C02:**

| Feature | Public Certificates | Private Certificates | Imported Certificates |
|---------|-------------------|---------------------|----------------------|
| **Cost** | FREE | $0.75/month + $400/month CA | FREE to store |
| **Issuer** | Amazon Trust Services | AWS Private CA | Third-party CA |
| **Browser Trust** | ✅ Yes | ❌ No (internal only) | ✅ Yes (if from trusted CA) |
| **Automatic Renewal** | ✅ Yes | ✅ Yes | ❌ No (manual) |
| **Use Case** | Public websites, APIs | Internal apps, microservices | Existing third-party certs |
| **Can Export** | ❌ No | ✅ Yes | ✅ Yes |
| **AWS Service Integration** | ✅ Yes | ✅ Yes | ✅ Yes |
| **Domain Validation** | ✅ Required | ❌ Not required | ❌ Not required |

### 🔐 SSL/TLS and HTTPS Concepts (CLF-C02 Context)

**What is SSL/TLS?**
- **SSL (Secure Sockets Layer):** Legacy encryption protocol
- **TLS (Transport Layer Security):** Modern successor to SSL (more secure)
- **Purpose:** Encrypts data in transit between client and server

**What is HTTPS?**
- **HTTPS = HTTP + SSL/TLS**
- Secure version of HTTP protocol
- Encrypts all communication between browser and website
- Indicated by padlock icon in browser

**Why HTTPS Matters:**
- **Security:** Prevents eavesdropping and man-in-the-middle attacks
- **Trust:** Users trust websites with HTTPS (browsers warn about non-HTTPS sites)
- **SEO:** Google ranks HTTPS sites higher in search results
- **Compliance:** Required for PCI-DSS (payment card data), HIPAA (healthcare)

**How ACM Enables HTTPS:**
1. Request certificate from ACM for your domain
2. Validate domain ownership (email or DNS)
3. ACM issues certificate
4. Attach certificate to AWS service (CloudFront, ALB, API Gateway)
5. Service automatically enables HTTPS using the certificate

### ✅ Key Exam Points

**Remember for CLF-C02:**

✅ **Primary Purpose:** Provision, manage, and deploy SSL/TLS certificates for AWS services  
✅ **Cost:** Public certificates are FREE (major cost advantage)  
✅ **Automatic Renewal:** Certificates automatically renewed before expiration (60 days)  
✅ **Integration:** Works with CloudFront, ALB, NLB, API Gateway, Elastic Beanstalk  
✅ **Cannot Export:** Public certificates cannot be used outside AWS integrated services  
✅ **Not for EC2:** Cannot install ACM public certificates directly on EC2 (use ALB instead)  
✅ **Domain Validation:** Email or DNS validation required for public certificates  
✅ **Private CA:** Costs $400/month for internal certificates  
✅ **Imported Certificates:** Can import third-party certificates (no auto-renewal)  
✅ **Use Case Keywords:** "HTTPS," "SSL/TLS," "secure website," "custom domain," "certificate management"

### 🎓 Practice Scenarios

**Scenario 1:** A company wants to enable HTTPS for their website hosted on S3 and delivered via CloudFront with a custom domain.  
**Answer:** Request a free public certificate from ACM, validate domain ownership, attach to CloudFront distribution

**Scenario 2:** An application runs on EC2 instances behind an Application Load Balancer and needs HTTPS encryption.  
**Answer:** Request ACM certificate, attach to ALB HTTPS listener (SSL termination at load balancer)

**Scenario 3:** A business wants to avoid annual SSL certificate costs of $500/year for their website.  
**Answer:** Use AWS Certificate Manager public certificates (free) instead of purchasing from third-party CAs

**Scenario 4:** A development team needs to install an SSL certificate directly on an EC2 instance for testing.  
**Answer:** Cannot use ACM public certificates on EC2; must import third-party certificate or use self-signed certificate

**Scenario 5:** A company has 20 subdomains (app1.example.com, app2.example.com, etc.) and wants to minimize certificate management.  
**Answer:** Request a wildcard ACM certificate (*.example.com) to cover all subdomains with one certificate

**Scenario 6:** An organization needs SSL certificates for internal microservices that don't need to be trusted by public browsers.  
**Answer:** Use AWS Private Certificate Authority with ACM private certificates ($400/month + $0.75/cert)

**Scenario 7:** A website's SSL certificate is about to expire in 30 days and the team is worried about outages.  
**Answer:** ACM automatically renews certificates 60 days before expiration (no manual action needed)

---

## Official AWS Documentation

- [AWS Certificate Manager Official Documentation](https://docs.aws.amazon.com/acm/)
- [AWS Certificate Manager FAQs](https://aws.amazon.com/certificate-manager/faqs/)
- [AWS Certificate Manager Pricing](https://aws.amazon.com/certificate-manager/pricing/)
- [ACM User Guide](https://docs.aws.amazon.com/acm/latest/userguide/)
- [ACM Best Practices](https://docs.aws.amazon.com/acm/latest/userguide/acm-bestpractices.html)
- [Requesting a Public Certificate](https://docs.aws.amazon.com/acm/latest/userguide/gs-acm-request-public.html)
- [Using ACM with CloudFront](https://docs.aws.amazon.com/acm/latest/userguide/acm-services.html)
