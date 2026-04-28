## STEP 1: Create IAM Foundations
Create IAM Users, Roles, Policies

## Step 1.1 – Create IAM User (Human)

Purpose: Simulate a developer or engineer

1. AWS Console → IAM → Users → Create user
2. Name: dev-user
3. Access type:
  - AWS Management Console
  - Programmatic access
4. Attach temporary admin (we’ll remove later):
  - AdministratorAccess
5. Save Access Key + Secret

📌 **Security Note:** This simulates a risky but common setup.

## Step 1.2 – Create S3 Bucket

1. S3 → Create bucket
2. Name: kfj-company-app-logs-<random>
3. Block public access: ON
4. No bucket policy yet

## Step 1.3 – Create EC2 Role

**Purpose:** EC2 should upload logs to S3 — nothing else.
1. IAM → Roles → Create role
2. Trusted entity: AWS Service
3. Use case: EC2
4. Role name: ec2-log-writer-role

## STEP 2: Create Over-Permissive Policy (Intentionally Wrong)

**2a. Test: Over-Permissive Policy**

## Step 2.1 -  Create Bad IAM Policy

IAM → Policies → Create policy → JSON:

**{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:*",
      "Resource": "*"
    }
  ]
}**

**Name it: S3FullAccess-OverPermissive**

**Attach it to: ec2-log-writer-role**

📌 Why this matters:
This is exactly how real breaches happen.

## STEP 3: Break Access (Demonstrate the Risk)

**2b. Break & Fix Access**

## Step 3.1 – Launch EC2

1. EC2 → Launch instance
2. Amazon Linux 2
3. Attach IAM role: "ec2-log-writer-role"
4. Enable SSH

## Step 3.2 – SSH into EC2
ssh ec2-user@public-ip OR ssh -i /path/key-pair.pem ec2-user@public-ip
## Step 3.3 – Demonstrate the Problem
aws s3 ls


## 👉 Expected result:
You can list all S3 buckets.

**aws s3 cp /etc/passwd s3://some-other-bucket/**
**Note: 👉 This should NOT be allowed, but it works.**
<img width="455" height="260" alt="image" src="https://github.com/user-attachments/assets/6a0997aa-c5ae-43f5-9f8b-54635ab1db0b" />
<img width="934" height="209" alt="image" src="https://github.com/user-attachments/assets/810b523e-43e2-4fb7-858f-a709d2cca099" />


## STEP 4: Fix with Least Privilege
**1b. Least-Privilege Policy for EC2 → S3**

## Step 4.1 – Create Correct IAM Policy
**{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:PutObject"
      ],
      "Resource": "arn:aws:s3:::company-app-logs-<random>/*"
    }
  ]
}**


**Name: "EC2-Write-Only-Logs"**

## Step 4.2 – Replace Policy

1. Detach S3FullAccess-OverPermissive
2. Attach EC2-Write-Only-Logs

## Step 4.3 – Re-Test Access
aws s3 ls
<img width="455" height="124" alt="image" src="https://github.com/user-attachments/assets/b53f7665-5b3c-4759-b09f-1b64961343e7" />


## ❌ Access denied (GOOD)

echo "test log" > log.txt
aws s3 cp log.txt s3://company-app-logs-<random>/

## ✅ Upload succeeds
