
**LAB 1 – Create VPC Endpoints**<br/>
1. AWS Console → VPC → Endpoints
2. Click Create endpoint
  Create:
  - S3 endpoint
  - DynamoDB endpoint

**Outcome**<br/>
Private AWS service access

**LAB 2 – Verify Private Subnet**<br/>
1. Ensure no public IP
2. Route via NAT or endpoint

**LAB 3 – Bastion Access**<br/>
1. SSH via Bastion host
2. Access private EC2

**LAB 4 – Test Connectivity**<br/>
1. From private EC2:
  - aws s3 ls

**Outcome**<br/>
Private connectivity confirmed

**Final Project Outcome**<br/>
- Secure private networking
- No internet exposure
- Controlled access via Bastion
