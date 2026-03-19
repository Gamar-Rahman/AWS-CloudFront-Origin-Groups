# AWS-CloudFront-Origin-Groups
# AWS project: Understanding CloudFront Origin Groups

## Overview
This project demonstrates how to use **Amazon CloudFront Origin Groups** to build a highly available and resilient content delivery architecture.

We combine:
- **Amazon S3 (Primary Origin)**
- **Amazon EC2 (Failover Origin)**
- **CloudFront CDN**

The goal is to ensure **content availability even if one origin fails**.

---

## Architecture

                      User Request
                           |
                           v
               +--------------------------+
               |     CloudFront CDN       |
               |   (Edge Locations)       |
               +-----------+--------------+
                           |
                 -------------------------
                 |                       |
                 v                       v
        +------------------+     +------------------+
        |   S3 Bucket      |     |   EC2 Instance   |
        |  Primary Origin  |     | Failover Origin  |
        +------------------+     +------------------+

#### Key AWS Services
Amazon EC2

Elastic Compute Cloud (EC2) provides virtual servers used here as a failover origin.

Amazon S3

Simple Storage Service (S3) stores static content and acts as the primary origin.

Amazon CloudFront

CloudFront is a Content Delivery Network (CDN) that caches and delivers content globally with low latency.

#### What is CloudFront Origin Group?

An Origin Group allows CloudFront to:

Define primary + secondary origins

Automatically failover if the primary origin becomes unavailable

Improve availability and fault tolerance

#### Why This Matters

In real-world systems:

Downtime = lost users + revenue

Single origin = single point of failure

CloudFront Origin Groups solve this by enabling:

Automatic failover

Global performance optimization

Resilient architecture

#### Lab Implementation
# Step 1 — Create S3 Bucket

Upload static content (HTML/image)

Enable public access (for lab purposes)

# Step 2 — Launch EC2 Instance

Install web server:

sudo yum install httpd -y
sudo systemctl start httpd
# Step 3 — Create CloudFront Distribution

Origin 1 → S3 Bucket (Primary)

Origin 2 → EC2 Instance (Failover)

# Step 4 — Configure Origin Group

Set S3 as primary

Set EC2 as secondary

Define failover criteria (HTTP 5xx errors)

# Step 5 — Test Failover

Access CloudFront URL

Stop S3 access or simulate failure

Observe traffic routed to EC2

#### Security Insight

CloudFront adds a strong security layer:

Reduces direct exposure of backend resources

Supports HTTPS and TLS encryption

Integrates with AWS WAF for protection

Enables DDoS mitigation (via AWS Shield)

#### Best Practice:

Keep S3 private and use Origin Access Control (OAC) instead of public access

#### Real-World Use Cases

Highly available web applications

Disaster recovery architectures

Media streaming platforms

Global content delivery systems

E-commerce platforms

#### Security insights

CloudFront improves performance and availability

Origin Groups enable automatic failover

S3 + EC2 combination ensures resilience

CDN is critical for modern cloud architecture

   
