# My-AWS-Projects

# AWS Account & Security Baseline – Day 1 Project

## Scenario
KFJ Solutions Ltd is a fintech startup migrating to AWS without an existing cloud security baseline.
The goal of this project is to secure the AWS account from day one using AWS best practices.

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

## Scenario
A company runs a backend service on EC2 that uploads logs to S3.
During a routine security review, the security team suspects that IAM permissions are overly permissive and could allow unintended access to sensitive S3 buckets.

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

## Scenario
A UK-based FinTech startup, PayWave, is migrating its on-premise application to AWS. The application consists of:
- A public-facing web application (frontend)
- A private backend service (API & database)

## Due to regulatory and security requirements:
- Backend systems must not be directly accessible from the internet
- Only the frontend should be publicly reachable
- Private resources must still access the internet for updates and patching

## Security & Architecture Requirements 
- Network isolation using a custom VPC
- Separation of public and private subnets
- Controlled internet access using Internet Gateway & NAT Gateway
- Clear routing rules following AWS best practices

## Outcome 

I have designed and implemented a production-grade AWS VPC from scratch, ensuring secure network segmentation, adhering to real-world AWS architectural standards, and validating traffic flow through effective use of routing and gateways.

---------------------------------------------------------------------------------------------------------------------------
## IAM Deep Dive (IAM Least Privilege & Access Control Failure) – Day 4 Project
**Goal:**
Design and implement a secure administrative access architecture for EC2 instances by deploying a Bastion Host and evaluating a modern alternative using AWS Systems Manager Session Manager, while enforcing least-privilege security group rules and aligning with AWS Well-Architected Framework security best practices.

**Business Scenario**
A regulated SaaS company is deploying backend services in AWS. For security reasons, backend servers must not be exposed to the public internet. However, system administrators still require SSH access for maintenance, patching, and incident response.

**Security & Architecture Requirements**
- No direct public access to private servers
- Centralised controlled entry point for administrators
- Least-privilege network rules
- Full alignment with AWS security best practices

## Outcome
I have designed a secure EC2 access model that was successfully implemented and validated, demonstrating controlled SSH access through a Bastion Host and a zero-trust alternative using Session Manager with IAM-based authentication, ensuring private instances remain inaccessible from the public internet while maintaining auditable and secure administrative connectivity.
---------------------------------------------------------------------------------------------------------------------------
## S3 & Storage Security – Day 5 Project
**Goal:**
Secure cloud storage by implementing strong security controls for Amazon S3, including encryption, access management, versioning, and logging.

**Technologies Used**
- Amazon S3
- AWS KMS
- IAM
- S3 Bucket Policies
- Server Access Logging

**Security Controls Implemented**
- Block Public Access
- Server-side Encryption (SSE-S3 and SSE-KMS)
- Bucket Policy Access Control
- Versioning
- Storage Access Logging

## Outcome
I designed a secure Amazon S3 storage architecture that protects sensitive data through encryption, strict access control policies, versioning, and logging for audit and monitoring.

