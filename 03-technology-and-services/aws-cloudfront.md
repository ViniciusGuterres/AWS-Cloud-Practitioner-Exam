# AWS CloudFront

## What is AWS CloudFront?

AWS CloudFront is a **global content delivery network (CDN) service** that securely delivers data, videos, applications, and APIs to customers globally with low latency and high transfer speeds. CloudFront uses a worldwide network of edge locations to cache content closer to users, improving performance and reducing the load on origin servers.

**Key Concept:** CloudFront acts as an intermediary between your users and your content, caching frequently requested content at edge locations around the world to provide faster access and better user experience.

## Core Components

### 1. Distributions
**Definition:** The configuration that tells CloudFront where to get content and how to deliver it

**Distribution Types:**
- **Web Distribution** - For websites, web applications, and general content delivery
- **RTMP Distribution** - For streaming media files (deprecated, use web distributions)
- **Origin settings** - Define where CloudFront gets the original content
- **Cache behaviors** - Rules for how different content types are cached

### 2. Origins
**Definition:** The source location where CloudFront retrieves content when it's not cached

**Origin Types:**
- **Amazon S3 buckets** - Static content like images, videos, documents
- **HTTP servers** - Web servers, load balancers, or any HTTP endpoint
- **MediaStore containers** - For video streaming applications
- **MediaPackage endpoints** - For live and on-demand video content

### 3. Edge Locations
**Definition:** Data centers where CloudFront caches copies of your content

**Edge Location Features:**
- **Global presence** - 400+ edge locations across 90+ cities worldwide
- **Automatic routing** - Users connected to nearest edge location
- **Content caching** - Stores frequently accessed content locally
- **Cache invalidation** - Ability to remove content from cache before expiration

### 4. Cache Behaviors
**Definition:** Rules that determine how CloudFront handles requests for different content

**Behavior Settings:**
- **Path patterns** - Define which URLs the behavior applies to
- **TTL settings** - How long content stays in cache
- **Query string handling** - Whether to include query parameters in caching
- **Header forwarding** - Which headers to forward to origin

## Key Features ⭐ **EXAM FOCUS**

### Global Content Delivery
- **Worldwide reach** - Deliver content to users anywhere in the world
- **Low latency** - Content served from nearest edge location
- **High availability** - Multiple edge locations provide redundancy
- **Automatic scaling** - Handle traffic spikes without manual intervention

### Performance Optimization
- **Caching** - Store frequently accessed content at edge locations
- **Compression** - Automatic gzip compression for text-based content
- **HTTP/2 support** - Modern protocol for improved performance
- **Keep-alive connections** - Reuse connections to origin servers

### Security Features
- **SSL/TLS encryption** - HTTPS support with custom or AWS certificates
- **Origin Access Identity (OAI)** - Restrict direct access to S3 origins
- **AWS WAF integration** - Web application firewall protection
- **DDoS protection** - Built-in protection against distributed attacks

### Customization Capabilities
- **Lambda@Edge** - Run code at edge locations for content customization
- **Custom error pages** - Serve custom pages for HTTP errors
- **Geographic restrictions** - Block or allow content based on user location
- **Signed URLs/Cookies** - Control access to premium content

## Content Types and Use Cases ⭐ **EXAM FOCUS**

### Static Content Delivery
**Content Types:** Images, CSS, JavaScript, fonts, documents

**Benefits:**
- **Fast loading** - Content cached at edge locations
- **Reduced origin load** - Less traffic to origin servers
- **Cost savings** - Lower bandwidth costs on origin
- **Global reach** - Consistent performance worldwide

### Dynamic Content Acceleration
**Content Types:** API responses, personalized content, database queries

**Benefits:**
- **Route optimization** - Use AWS backbone network
- **Connection reuse** - Persistent connections to origin
- **Request collapsing** - Combine similar requests
- **Edge-side includes** - Combine static and dynamic content

### Video Streaming
**Content Types:** Live streams, video on demand, adaptive bitrate

**Benefits:**
- **Smooth playback** - Reduced buffering and interruptions
- **Adaptive delivery** - Adjust quality based on connection speed
- **Global distribution** - Serve video content worldwide
- **Cost optimization** - Efficient bandwidth usage

### Software Distribution
**Content Types:** Application downloads, updates, patches

**Benefits:**
- **Fast downloads** - Cached files at edge locations
- **Reduced costs** - Lower origin bandwidth usage
- **High availability** - Multiple download locations
- **Version control** - Easy content updates and rollbacks

## Integration with AWS Services ⭐ **EXAM FOCUS**

### Amazon S3
**Integration:** Primary origin for static content

**S3 Features:**
- **Origin Access Identity** - Secure access to S3 buckets
- **Static website hosting** - Accelerate S3-hosted websites
- **Automatic failover** - Multiple S3 origins for redundancy
- **Cost optimization** - Reduce S3 data transfer costs

### Elastic Load Balancer (ELB)
**Integration:** Origin for dynamic content and applications

**ELB Features:**
- **Application acceleration** - Speed up dynamic web applications
- **Health checking** - Monitor origin health through CloudFront
- **SSL offloading** - Handle SSL termination at edge locations
- **Geographic routing** - Route to different ELB origins by region

### AWS Certificate Manager (ACM)
**Integration:** SSL/TLS certificate management

**ACM Features:**
- **Free SSL certificates** - No cost for CloudFront SSL certificates
- **Automatic renewal** - Certificates renewed automatically
- **Custom domains** - Use your own domain names with HTTPS
- **Wildcard certificates** - Secure multiple subdomains

### AWS WAF and Shield
**Integration:** Security and DDoS protection

**Security Features:**
- **Web application firewall** - Filter malicious traffic at edge
- **DDoS protection** - Shield Standard included, Shield Advanced available
- **Rate limiting** - Control request rates per IP address
- **Geographic blocking** - Block traffic from specific countries

## Pricing Model ⭐ **EXAM FOCUS**

### Data Transfer Pricing
- **Regional variations** - Different prices for different geographic regions
- **Volume discounts** - Lower per-GB costs for higher usage
- **Free tier** - 1 TB data transfer out and 10 million requests per month
- **Origin charges** - Separate charges for data transfer from origin to CloudFront

### Request Pricing
- **HTTP requests** - Charges per 10,000 requests
- **HTTPS requests** - Slightly higher charges for secure requests
- **Regional differences** - Request prices vary by geographic region
- **No minimum fees** - Pay only for actual usage

### Additional Charges
- **SSL certificates** - Custom SSL certificates incur monthly charges
- **Dedicated IP addresses** - Additional cost for dedicated IPs
- **Lambda@Edge** - Separate charges for edge computing
- **Invalidation requests** - First 1,000 invalidations per month free

## Common Use Cases ⭐ **EXAM FOCUS**

### Website Acceleration
**Scenario:** Speed up website loading times for global users

**Implementation:**
- **Static asset caching** - Cache images, CSS, JavaScript files
- **Dynamic content acceleration** - Optimize delivery of personalized content
- **Mobile optimization** - Optimize content for mobile devices
- **Progressive web apps** - Enhance PWA performance globally

### E-commerce Platforms
**Scenario:** Improve online shopping experience and conversion rates

**Implementation:**
- **Product catalog delivery** - Fast loading of product images and descriptions
- **Personalized content** - Location-specific pricing and promotions
- **Shopping cart optimization** - Accelerate checkout process
- **Inventory synchronization** - Real-time inventory updates

### Media and Entertainment
**Scenario:** Deliver video content and media files to global audiences

**Implementation:**
- **Video streaming** - Live and on-demand video delivery
- **Gaming content** - Distribute game assets and updates
- **Music streaming** - Deliver audio content with low latency
- **Digital publishing** - Distribute e-books and digital magazines

### API Acceleration
**Scenario:** Improve performance of REST APIs and microservices

**Implementation:**
- **API response caching** - Cache frequently requested API responses
- **Geographic distribution** - Serve APIs from multiple regions
- **Rate limiting** - Control API usage and prevent abuse
- **Authentication** - Implement API authentication at edge locations

## Best Practices ⭐ **EXAM FOCUS**

### Cache Optimization
- **Appropriate TTL values** - Set cache expiration based on content type
- **Cache-Control headers** - Use proper HTTP headers for caching
- **Query string handling** - Configure query parameter caching appropriately
- **Compression** - Enable compression for text-based content

### Security Implementation
- **HTTPS everywhere** - Use SSL/TLS for all content delivery
- **Origin protection** - Use OAI to protect S3 origins
- **Access controls** - Implement signed URLs for premium content
- **Regular monitoring** - Monitor for security threats and anomalies

### Performance Monitoring
- **CloudWatch metrics** - Monitor cache hit ratios and performance
- **Real user monitoring** - Track actual user experience
- **A/B testing** - Test different configurations for optimization
- **Regular reviews** - Periodically review and optimize configurations

### Cost Management
- **Cache hit optimization** - Improve cache hit ratios to reduce origin costs
- **Regional analysis** - Understand traffic patterns by region
- **Reserved capacity** - Consider reserved capacity for predictable workloads
- **Monitoring tools** - Use AWS Cost Explorer to track CloudFront costs

## Lambda@Edge Integration ⭐ **EXAM FOCUS**

### Edge Computing Capabilities
**Function Types:**
- **Viewer request** - Modify requests from users before cache lookup
- **Origin request** - Modify requests to origin when cache miss occurs
- **Origin response** - Modify responses from origin before caching
- **Viewer response** - Modify responses to users before delivery

### Common Lambda@Edge Use Cases
- **Authentication** - Implement user authentication at edge locations
- **A/B testing** - Route users to different content versions
- **Content personalization** - Customize content based on user attributes
- **SEO optimization** - Generate different content for search engines

## Monitoring and Analytics ⭐ **EXAM FOCUS**

### CloudWatch Metrics
- **Cache hit ratio** - Percentage of requests served from cache
- **Origin latency** - Response time from origin servers
- **Error rates** - 4xx and 5xx error percentages
- **Data transfer** - Amount of data delivered to users

### Real-Time Logs
- **Access logs** - Detailed information about every request
- **Real-time streaming** - Stream logs to Kinesis Data Streams
- **Custom analysis** - Analyze traffic patterns and user behavior
- **Security monitoring** - Detect and respond to security threats

### Reporting and Analytics
- **Usage reports** - Understand traffic patterns and popular content
- **Popular objects** - Identify most frequently requested content
- **Top referrers** - Track traffic sources and referral patterns
- **Cache statistics** - Analyze cache performance and optimization opportunities

## Exam Tips ⭐ **EXAM FOCUS**

### Key Concepts to Remember
- **CloudFront is a CDN** - Content delivery network for global distribution
- **Edge locations cache content** - Faster delivery from locations closer to users
- **Multiple origin types** - S3, HTTP servers, MediaStore, MediaPackage
- **Security features included** - SSL/TLS, DDoS protection, WAF integration

### Common Exam Scenarios
- **Website performance** - Using CloudFront to speed up websites
- **Global content delivery** - Serving content to worldwide audiences
- **Cost optimization** - Reducing bandwidth costs and origin load
- **Security enhancement** - Protecting origins and filtering traffic

### Important Distinctions
- **CloudFront vs S3 Transfer Acceleration** - CDN vs single service acceleration
- **Web vs RTMP distributions** - General content vs streaming media
- **Edge locations vs Regions** - Content caching vs full AWS services
- **Static vs dynamic content** - Different optimization strategies

### Pricing Considerations
- **Regional price variations** - Different costs in different regions
- **Data transfer charges** - Main cost component for CloudFront
- **Request charges** - Additional costs for HTTP/HTTPS requests
- **Free tier benefits** - 1 TB and 10 million requests per month

## Summary

AWS CloudFront is a powerful global CDN that improves website performance, reduces costs, and enhances security by caching content at edge locations worldwide. Understanding CloudFront's core components, integration with other AWS services, pricing model, and common use cases is essential for the CLF-C02 exam. Key concepts include distributions, origins, edge locations, cache behaviors, and the various content types that benefit from CDN acceleration.
