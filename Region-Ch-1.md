## How to choose an AWS Region?

- Compliance
- Proximity
- Available Services
- Pricing

## Availability zone

- Each region has many availability zones. (Usually 3, min 3 and max 6)
- Each availability zone is one or more discrete data centers with redundant power, networking, and connectivity
- They are separated from each other so that they are isolated from disasters.
- These data centers/availability zones are connected with high bandwidth, ultra-low latency networking, and therefore altogether
  being linked together forms a region.
- Points of Presence/Edge locations

# Tour of AWS Console

* AWS has Global services
  - Identity & Access Management (IAM)
  - Route 53 (DNS Service)
  - CloudFront (Content Delivery Network)
  - WAF (Web Application Firewall)
* Most AWS Services are region scoped
  - Amazon EC2 (IAAS)
  - Elastic Beanstalk (PAAS)
  - Lambda (FAAS)
  - Rekognition (SAAS)
 
  ### Note: Some services in AWS are global services
