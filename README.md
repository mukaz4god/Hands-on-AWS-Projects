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
- IAM Access Analyzer

## Outcome
I demonstrated creat an AWS account with security baseline with AWS account security fundamentals which aligned with:
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

## Due to regulatory and security requirements: ##
- Backend systems must not be directly accessible from the internet
- Only the frontend should be publicly reachable
- Private resources must still access the internet for updates and patching

## Security & Architecture Requirements ##
- Network isolation using a custom VPC
- Separation of public and private subnets
- Controlled internet access using Internet Gateway & NAT Gateway
- Clear routing rules following AWS best practices

## Your Role: ##
You are acting as a Cloud / DevOps Engineer, responsible for designing and implementing a secure, production-ready VPC from scratch.

## Outcome 
I have designed and implemented a production-grade AWS VPC from scratch, ensuring secure network segmentation, adhering to real-world AWS architectural standards, and validating traffic flow through effective use of routing and gateways.
