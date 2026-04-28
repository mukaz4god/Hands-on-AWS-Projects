# Hands-on AWS Projects

# AWS Account & Security Baseline – Day 1 Project

## Objectives
- Protect root account
- Enforce IAM best practices
- Enable cost governance
- Enable logging and visibility
- Document decisions for audits

**Outcome**<br/>
I demonstrated creating an AWS account with a security baseline, with AWS account security fundamentals, which aligned with:
- AWS Well-Architected Framework (Security Pillar)
- CIS AWS Foundations Benchmark

## IAM Deep Dive (IAM Least Privilege & Access Control Failure) – Day 2 Project

## Objectives 
- Review IAM access
- Demonstrate the risk
- Apply least privilege
- Validate the fix

**Outcome**<br/>
I built a real AWS environment where I demonstrated the security impact of over-permissive IAM roles on EC2, then remediated it using least-privilege policies and validated the fix with controlled testing.

## VPC from Scratch – Day 3 Project
**Goal:** To design, build, and verify a production-style AWS VPC with public and private networking

**Outcome**<br/>
I have designed and implemented a production-grade AWS VPC from scratch, ensuring secure network segmentation, adhering to real-world AWS architectural standards, and validating traffic flow through effective use of routing and gateways.

## IAM Deep Dive (IAM Least Privilege & Access Control Failure) – Day 4 Project
**Goal:**
Design and implement a secure administrative access architecture for EC2 instances by deploying a Bastion Host and evaluating a modern alternative using AWS Systems Manager Session Manager, while enforcing least-privilege security group rules and aligning with AWS Well-Architected Framework security best practices.

**Outcome**<br/>
I have designed a secure EC2 access model that was successfully implemented and validated, demonstrating controlled SSH access through a Bastion Host and a zero-trust alternative using Session Manager with IAM-based authentication, ensuring private instances remain inaccessible from the public internet while maintaining auditable and secure administrative connectivity.

## S3 & Storage Security – Day 5 Project
**Goal:**
To secure cloud storage by implementing strong security controls for Amazon S3, including encryption, access management, versioning, and logging.

**Outcome**<br/>
I designed a secure Amazon S3 storage architecture that protects sensitive data through encryption, strict access control policies, versioning, and logging for audit and monitoring.

## Elastic Load Balancing – Day 6 Project
**Goal:**
To design and deploy a highly available web application architecture by implementing an Application Load Balancer that distributes incoming traffic across multiple EC2 instances.

**Outcome**<br/>
A highly available web application architecture was successfully deployed using an Application Load Balancer that distributes user traffic across multiple EC2 instances and automatically routes requests only to healthy servers.
## Auto Scaling & EC2 Launch Templates – Day 7 Project
**Goal:**
To implement horizontal scaling using Auto Scaling Groups and Launch Templates to handle variable application load.

**Outcome**<br/>
A scalable, fault-tolerant architecture was deployed that automatically adjusts compute capacity based on demand and integrates with a load balancer for high availability.

## Auto Scaling & EC2 Launch Templates – Day 8 Project
**Goal:** To implement DNS management and routing using Route 53 to map a custom domain to application infrastructure and enable failover.

**Outcome**<br/>
A fully functional DNS setup was created, enabling domain-based access to the application, along with health checks and failover routing to ensure high availability.

## CloudWatch Monitoring – Day 9 Project

**Goal:** To implement monitoring, alerting, and operational visibility in AWS using CloudWatch metrics, alarms, dashboards, and SNS notifications.

**Outcome**<br/>
A monitoring solution was deployed with real-time metrics, alarms, dashboards, and notifications, enabling proactive incident detection, alerting, and performance visibility across cloud infrastructure.

## CloudTrail & Logging – Day 10 Project

**Goal:** To implement centralised audit logging and compliance monitoring using CloudTrail, multi-region trails, S3 log storage, log validation, and Athena queries.

**Outcome**<br/>
A centralised and tamper-evident logging solution was deployed, enabling full visibility into AWS account activity, audit readiness, and support for security investigations and compliance requirements.

## Lambda Basics – Day 11 Project

**Goal:** To deploy a serverless function using AWS Lambda, trigger it with S3 events, and enable CloudWatch logging for monitoring and troubleshooting.

**Outcome**<br/>
A serverless event-driven workflow was implemented, where S3 uploads automatically triggered Lambda execution and CloudWatch logs provided operational visibility into function activity.

## API Gateway Basics – Day 12 Project

**Goal:** To build a REST API using API Gateway, integrate it with Lambda, and secure it with CORS and throttling controls.

**Outcome**<br/>
A serverless API architecture was deployed, enabling secure HTTP access to Lambda backends with throttling, CORS configuration, and observable execution flow.

## DynamoDB Serverless DB – Day 13 Project

**Goal:** To implement a serverless NoSQL database using DynamoDB, enable encryption and backups, and integrate it with Lambda for application data operations.

**Outcome**<br/>
A secure and scalable DynamoDB-backed serverless data layer was created, allowing Lambda functions to perform CRUD operations with encryption and backup protection enabled.

## SNS & SQS – Day 14 Project

**Goal:** To build an event-driven messaging architecture using SNS, SQS, and Lambda for decoupled and reliable message processing.

**Outcome**<br/>
An event-driven pipeline was successfully implemented, allowing messages to flow from SNS to SQS and then to Lambda for asynchronous and scalable processing.

## AWS Organisations & Multi-Account – Day 18 Project

**Goal:** To implement a multi-account AWS environment using AWS Organisations, organisational units, service control policies, and consolidated billing.

**Outcome**<br/>
A governed multi-account architecture was established, providing account isolation, centralised policy enforcement, and consolidated billing for improved enterprise control.

## AWS Config & Compliance – Day 19 Project

**Goal:** To enable continuous compliance monitoring using AWS Config, managed and custom rules, and automated remediation with Lambda.

**Outcome**<br/>
A continuous compliance framework was deployed, enabling resource configuration tracking, policy evaluation, and automated remediation of non-compliant resources.

## Security Hub & GuardDuty – Day 20 Project

**Goal:** To implement AWS-native threat detection and security posture monitoring using GuardDuty and Security Hub.

**Outcome**<br/>
A centralised security monitoring capability was established, with GuardDuty generating threat findings and Security Hub aggregating and presenting security alerts for investigation.

## S3 Advanced Security – Day 21 Project

**Goal:** To harden Amazon S3 storage using bucket policies, block public access, logging, replication, and MFA Delete.

**Outcome**<br/>
An enterprise-grade S3 security configuration was implemented, improving access control, auditability, resilience, and protection against accidental or unauthorised data deletion.

## EC2 Advanced Networking – Day 22 Project

**Goal:** To implement secure EC2 networking using private subnets, VPC endpoints for AWS services, and bastion-based administrative access.

**Outcome**<br/>
A secure private networking model was deployed, enabling controlled EC2 access and private connectivity to AWS services without exposing workloads directly to the internet.

## Systems Manager Advanced – Day 23 Project

**Goal:** To centralize EC2 management using Systems Manager Inventory, Patch Manager, State Manager, Automation documents, and Run Command without relying on SSH.

**Outcome**<br/>
A centralised EC2 operations model was implemented, enabling fleet-wide inventory, automated patching, configuration enforcement, and remote command execution through Systems Manager.

## EC2 Access Recovery & Abuse Handling – Day 24 Project

**Goal:** To simulate and implement EC2 access recovery methods for lost SSH keys, Session Manager access, EBS volume recovery, Windows password recovery, and abuse response handling.

**Outcome**<br/>
A structured EC2 recovery and incident-response workflow was established, enabling safe restoration of access to locked instances while preserving security and operational control.

## Advanced VPC Networking – Day 25 Project

**Goal:** To build private networking with secure access paths using a Bastion Host, gateway and interface VPC endpoints, DNS resolution, and layered traffic controls.

**Outcome**<br/>
A private AWS networking architecture was implemented, enabling secure service access, controlled administration paths, and validation of Security Group and NACL behaviour.

## Transit Gateway – Day 26 Project

**Goal:** To design and implement an enterprise multi-VPC network using Transit Gateway for centralised routing and cross-VPC communication.

**Outcome**<br/>
A hub-and-spoke multi-VPC architecture was deployed, enabling scalable cross-VPC connectivity and centralised route management through Transit Gateway.

## CloudFront Advanced Security – Day 27 Project

**Goal:** To secure global content delivery using CloudFront with a private S3 origin, Origin Access Control, geo-restrictions, signed URLs, and field-level encryption.

**Outcome**<br/>
A secure edge delivery architecture was implemented, protecting private S3 content behind CloudFront while enforcing controlled global access and advanced content protection mechanisms.

## AWS WAF & DDoS Protection – Day 28 Project

**Goal:** To protect a public web application using AWS WAF, managed rule groups, rate limiting, logging, and AWS Shield-aware protection.

**Outcome**<br/>
A web application firewall solution was deployed, enabling inspection and control of malicious traffic, request-rate abuse protection, and improved visibility into web threats.

## API Gateway Deep Dive – Day 29 Project

**Goal:** To build a secure REST API architecture with Lambda integration, throttling, API keys, usage controls, and resource policies.

**Outcome**<br/>
A production-style API Gateway deployment was implemented, providing secure API access, controlled traffic consumption, and policy-based restrictions for serverless backends.

## AWS Artefact Compliance – Day 30 Project

**Goal:** To develop enterprise compliance awareness by exploring AWS Artefact reports, reviewing AWS assurance documentation, and mapping the shared responsibility model.

**Outcome**<br/>
A compliance-awareness workflow was established, enabling structured review of AWS audit reports and a clearer understanding of AWS and customer control responsibilities.

## Route 53 DNSSEC – Day 31 Project

**Goal:** To protect public DNS integrity by enabling DNSSEC signing, configuring the Key Signing Key, and validating the chain of trust.

**Outcome**<br/>
A DNSSEC-enabled Route 53 hosted zone was implemented, strengthening DNS integrity and helping protect against spoofing and tampering attacks.

## AWS Network Firewall – Day 32 Project

**Goal:** To deploy AWS Network Firewall with stateless and stateful inspection rules for centralised VPC traffic filtering and inspection.

**Outcome**<br/>
A managed network inspection architecture was implemented, providing deeper traffic visibility, policy enforcement, and layered protection for VPC traffic flows.
