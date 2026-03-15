## Step-by-Step Solution

**Architecture Overview**<br/>
This project implements secure object storage using Amazon S3 with the following controls:<br/>

- Secure S3 bucket configuration
- Encryption at rest (SSE-S3 and SSE-KMS)
- Bucket policies for access control
- Versioning for data protection
- Server access logging for auditing

**LAB 1 – Create Secure S3 Buckets**<br/>

**Step 1 – Navigate to Amazon S3**
- Log in to AWS Console
- Search for S3
- Click Amazon S3

**Step 2 – Create the Primary Data Bucket**
- Click Create bucket
  **Configure the bucket:**
  - Bucket name: kfj-secure-data-bucket

   **AWS Region**
  - Choose the same region as your infrastructure.
  
  **Object Ownership**
  - Select: ACLs disabled (recommended)
**Note:** This ensures access is controlled only through IAM policies and bucket policies, which is an AWS security best practice.

  **Block Public Access**
  - Ensure all options remain enabled: Block all public access and confirm the warning checkbox.

  **Default Encryption**
  - Leave default encryption for the next lab.

  **Click:**: Create bucket

**Outcome**
A secure S3 bucket is created with public access blocked.

**LAB 2 – Enable Encryption** : Encryption protects sensitive data stored in S3.

Two common methods are used:
-  SSE-S3 – AWS managed encryption
-  SSE-KMS – Encryption using AWS Key Management Service

**Step 1 – Enable SSE-S3**
-  Go to S3 → Buckets
-  Select your bucket
-  Click Properties
-  Scroll to Default encryption
-  Click Edit

**Select:** Server-side encryption with Amazon S3 managed keys (SSE-S3) then **Save changes.**

**Outcome**
All new objects stored in the bucket are encrypted automatically.

**Step 2 – Enable SSE-KMS (Advanced Security)**
- Go to Properties → Default encryption
- Click Edit
  - Select: Server-side encryption with AWS Key Management Service (SSE-KMS)
  - Choose: aws/s3 or create a customer-managed KMS key.
  - Click Save changes.

**Outcome**
Encryption keys are managed and auditable using AWS KMS.

**LAB 3 – Configure Bucket Policies & Access Controls**: Bucket policies define who can access objects in the bucket.

**Step 1 – Navigate to Bucket Policy**
- Open your S3 bucket
- Click Permissions
- Scroll to Bucket policy
- Click Edit

**Step 2 – Add a Secure Policy Example**
Sample: Allow read access only from a specific IAM role.
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::ACCOUNT-ID:role/AppRole"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::company-secure-data-bucket/*"
    }
  ]
}
```
- Click Save changes.

**Outcome**
Only approved IAM roles can access bucket objects.

**LAB 4 – Enable Versioning & Logging**

**Enable Versioning**: Versioning protects against accidental deletion or overwriting.

**Step 1 – Enable Versioning**
- Open the bucket
- Click Properties
- Scroll to Bucket Versioning
- Click Edit
- Select: Enable
- Save changes.

**Outcome**
Multiple versions of files are preserved.

## Enable Server Access Logging
Logging records all requests made to the bucket.

**Step 1 – Create Log Bucket**
- Go to S3 → Create bucket
- Provide a bucket name: kfj-s3-access-logs
- Enable: Block Public Access
- Create bucket.

**Step 2 – Enable Logging**
- Go to your primary bucket
- Click Properties
- Scroll to Server access logging
- Click Edit
- Enable logging and select: Target bucket → your-bucket-name (kfj-s3-access-logs)
- Save changes.

**Outcome**
All S3 access activity is recorded for auditing.

## Final Project Outcome

After completing this project, I  have successfully implemented:
- Secure S3 bucket architecture
- Encryption at rest using SSE-S3 and SSE-KMS
- Strict access control with bucket policies
- Data protection using versioning
- Storage access auditing through logging

**Note:** This setup aligns with AWS security best practices and the AWS Well-Architected Framework Security Pillar.
