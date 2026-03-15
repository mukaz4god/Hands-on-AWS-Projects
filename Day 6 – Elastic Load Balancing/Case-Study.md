## Case Study – Building a Highly Available Web Application

**Business Scenario**

A rapidly growing SaaS company is deploying a customer-facing web application on AWS. As traffic increases, relying on a single EC2 instance becomes a risk because any instance failure would result in downtime. To improve availability, scalability, and reliability, the company wants to deploy multiple application servers behind a load balancer that can distribute traffic evenly across instances.

***The architecture must support:**
- High availability
- Automatic traffic distribution
- Health monitoring of application servers
- Fault tolerance

**Your Task**
You are the Cloud Engineer responsible for implementing a highly available web architecture using Application Load Balancer (ALB).

**Your task is to configure:**
- Application Load Balancer
- Target Groups
- Health Checks
- Load balancing verification

This architecture follows AWS best practices from the AWS Well-Architected Framework Reliability Pillar.
