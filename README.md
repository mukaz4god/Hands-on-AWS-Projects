# My-AWS-Projects

# AWS Account & Security Baseline – Day 1 Project

## Objectives
- Protect root account
- Enforce IAM best practices
- Enable cost governance
- Enable logging and visibility
- Document decisions for audits

## Security Controls Implemented
- Root MFA
- IAM Admin User (no root usage)
- AWS Budgets & Alerts
- CloudTrail (For Regions)
- IAM Access Analyser

## Outcome
I demonstrated creating an AWS account with a security baseline, with AWS account security fundamentals, which aligned with:
- AWS Well-Architected Framework (Security Pillar)
- CIS AWS Foundations Benchmark
---------------------------------------------------------------------------------------------------------------------------
## IAM Deep Dive (IAM Least Privilege & Access Control Failure) – Day 2 Project

## Objectives 
- Review IAM access
- Demonstrate the risk
- Apply least privilege
- Validate the fix

## Outcome
I built a real AWS environment where I demonstrated the security impact of over-permissive IAM roles on EC2, then remediated it using least-privilege policies and validated the fix with controlled testing.
---------------------------------------------------------------------------------------------------------------------------
## VPC from Scratch – Day 3 Project
**Goal:** To design, build, and verify a production-style AWS VPC with public and private networking

## Outcome 
I have designed and implemented a production-grade AWS VPC from scratch, ensuring secure network segmentation, adhering to real-world AWS architectural standards, and validating traffic flow through effective use of routing and gateways.

---------------------------------------------------------------------------------------------------------------------------
## IAM Deep Dive (IAM Least Privilege & Access Control Failure) – Day 4 Project
**Goal:**
Design and implement a secure administrative access architecture for EC2 instances by deploying a Bastion Host and evaluating a modern alternative using AWS Systems Manager Session Manager, while enforcing least-privilege security group rules and aligning with AWS Well-Architected Framework security best practices.

## Outcome
I have designed a secure EC2 access model that was successfully implemented and validated, demonstrating controlled SSH access through a Bastion Host and a zero-trust alternative using Session Manager with IAM-based authentication, ensuring private instances remain inaccessible from the public internet while maintaining auditable and secure administrative connectivity.
---------------------------------------------------------------------------------------------------------------------------
## S3 & Storage Security – Day 5 Project
**Goal:**
To secure cloud storage by implementing strong security controls for Amazon S3, including encryption, access management, versioning, and logging.

## Outcome
I designed a secure Amazon S3 storage architecture that protects sensitive data through encryption, strict access control policies, versioning, and logging for audit and monitoring.

--------------------------------------------------------------------------------------------------------------------------
## Elastic Load Balancing – Day 6 Project
**Goal:**
To design and deploy a highly available web application architecture by implementing an Application Load Balancer that distributes incoming traffic across multiple EC2 instances.

## Outcome
A highly available web application architecture was successfully deployed using an Application Load Balancer that distributes user traffic across multiple EC2 instances and automatically routes requests only to healthy servers.
--------------------------------------------------------------------------------------------------------------------------
## Auto Scaling & EC2 Launch Templates – Day 7 Project
**Goal:**
To implement horizontal scaling using Auto Scaling Groups and Launch Templates to handle variable application load.

## Outcome
A scalable, fault-tolerant architecture was deployed that automatically adjusts compute capacity based on demand and integrates with a load balancer for high availability.
--------------------------------------------------------------------------------------------------------------------------
## Auto Scaling & EC2 Launch Templates – Day 8 Project
**Goal:** To implement DNS management and routing using Route 53 to map a custom domain to application infrastructure and enable failover.

##Outcome
A fully functional DNS setup was created, enabling domain-based access to the application, along with health checks and failover routing to ensure high availability.
##Outcome
A fully functional DNS setup was created, enabling domain-based access to the application, along with health checks and failover routing to ensure high availability.



