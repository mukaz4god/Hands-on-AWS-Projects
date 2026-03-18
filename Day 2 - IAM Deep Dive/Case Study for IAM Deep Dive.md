## Case Study Title

IAM Least Privilege Failure in EC2-to-S3 Access

## Scenario

A company runs a backend service on EC2 that uploads application logs to Amazon S3. During a routine security review, the security team suspects that IAM permissions are overly permissive and could allow unintended access to sensitive S3 buckets.

**As the Security Engineer, your task is to:**
- Review IAM access
- Demonstrate the risk
- Apply least privilege
- Validate the fix

## Business Problem

The engineering team granted broad IAM permissions to EC2 instances to speed up development.
Over time, these permissions were never reviewed, increasing the risk of unauthorized data access if an instance were compromised.

## This Created Risks Of

- Excessive access to all S3 buckets
- Data exfiltration from unrelated or sensitive buckets
- Increased blast radius in case of EC2 compromise
- Violation of least-privilege and cloud security best practices

## Objectives

- Identify over-permissive IAM policies
- Demonstrate real-world impact of misconfiguration
- Restrict access using least-privilege principles
- Validate access before and after remediation

## Solution Design – Security Controls Implemented

- IAM Role attached to EC2 (instead of IAM user credentials)
- Removal of wildcard (s3:*, Resource: "*") permissions
- Scoped S3 permissions limited to:
    - s3:PutObject
    - A single log bucket path
- Explicit validation via AWS CLI testing

## Security Architecture (Narrative)

The EC2 instance assumes an IAM role that defines what AWS resources it can access. Initially, the role allowed unrestricted S3 access, enabling the EC2 instance to list and write to all buckets.
After remediation, the IAM role was restricted to allow write-only access to a specific S3 bucket used for application logs, enforcing least privilege and minimizing blast radius.

## Outcomes

- Over-permissive access was successfully demonstrated and proven
- Unauthorized S3 access was blocked after remediation
- EC2 retained only the permissions required for its business function
- Security posture aligned with AWS Well-Architected Framework (Security Pillar)

**By completing this project, you I have demonstrated, proven, and documented how improper IAM permissions create real security risk — and how to fix it using least privilege.**

## What I’d Improve Next

- Enable CloudTrail to log IAM and S3 activity
- Use IAM Access Analyzer to detect future misconfigurations
- Enforce IAM policies using Infrastructure as Code (Terraform)
- Add automated security checks in CI/CD pipelines
