# Day 33 – Advanced VPC Networking

# Setup Guide – Industrial Standard Step-by-Step Solution

## Architecture Overview

This project builds a secure private networking design with:

- One VPC
- Public subnet for Bastion Host
- Private subnet for workload EC2
- Gateway VPC Endpoint for S3
- Interface VPC Endpoints for Systems Manager
- DNS resolution enabled
- Security Group and NACL testing

Traffic pattern:

```text
Admin → Bastion Host → Private EC2
Private EC2 → S3 via Gateway Endpoint
Private EC2 → Systems Manager via Interface Endpoints
```

---

## LAB 1 – Create or Verify VPC DNS Settings

### Step 1 – Open the VPC Console

1. Go to **AWS Console**
2. Search for **VPC**
3. Click **Your VPCs**
4. Select your project VPC

### Step 2 – Enable DNS Features

Confirm the following are enabled:

- DNS resolution
- DNS hostnames

To enable them:

1. Select the VPC
2. Click **Actions**
3. Choose **Edit VPC settings**
4. Enable:
   - DNS resolution
   - DNS hostnames
5. Click **Save**

### Why This Matters

Private endpoints rely on DNS names resolving correctly inside the VPC. Without DNS support, private endpoint connectivity may fail.

### Outcome

The VPC is ready for private AWS service connectivity.

---

## LAB 2 – Create Bastion Host

### Step 1 – Launch Bastion EC2

1. Go to **EC2 → Instances**
2. Click **Launch instances**
3. Name the instance:

```text
bastion-host
```

4. Choose Amazon Linux 2023 or Ubuntu LTS
5. Select an instance type such as `t2.micro`
6. Select your key pair

### Step 2 – Network Settings

1. Click **Edit** under Network settings
2. Select your VPC
3. Select the **public subnet**
4. Enable **Auto-assign public IP**

### Step 3 – Bastion Security Group

Create a Security Group:

```text
bastion-sg
```

Inbound rule:

| Type | Port | Source |
|---|---:|---|
| SSH | 22 | Your public IP only |

Outbound rule:

| Type | Destination |
|---|---|
| SSH | Private EC2 Security Group |

### Outcome

You now have a controlled administrative entry point into the VPC.

---

## LAB 3 – Create Private EC2 Instance

### Step 1 – Launch Private Instance

1. Go to **EC2 → Instances**
2. Click **Launch instances**
3. Name:

```text
private-app-server
```

4. Choose Amazon Linux 2023 or Ubuntu LTS
5. Select your key pair or use Session Manager only

### Step 2 – Network Settings

1. Select the same VPC
2. Select the **private subnet**
3. Disable **Auto-assign public IP**

### Step 3 – Private EC2 Security Group

Create a Security Group:

```text
private-ec2-sg
```

Inbound rule if using Bastion:

| Type | Port | Source |
|---|---:|---|
| SSH | 22 | bastion-sg |

Inbound rule if using SSM only:

| Type | Port | Source |
|---|---:|---|
| None | N/A | N/A |

Outbound rule:

| Type | Destination |
|---|---|
| HTTPS | VPC endpoints / AWS services |
| S3 | S3 Gateway Endpoint |

### Outcome

The private EC2 instance is isolated from direct public internet access.

---

## LAB 4 – Create S3 Gateway VPC Endpoint

### Step 1 – Open Endpoints

1. Go to **VPC**
2. Click **Endpoints**
3. Click **Create endpoint**

### Step 2 – Select S3 Gateway Endpoint

1. Service category: **AWS services**
2. Search for:

```text
s3
```

3. Select the service type showing **Gateway**

### Step 3 – Configure Endpoint

1. Select your VPC
2. Select the route table associated with your private subnet
3. Choose Full Access for lab purposes or use a restricted endpoint policy for production
4. Click **Create endpoint**

### Production Endpoint Policy Example

```json
{
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": [
        "s3:GetObject",
        "s3:ListBucket"
      ],
      "Resource": [
        "arn:aws:s3:::example-private-bucket",
        "arn:aws:s3:::example-private-bucket/*"
      ]
    }
  ]
}
```

### Test

Connect to the private instance and run:

```bash
aws s3 ls
```

### Outcome

The private EC2 instance can access S3 without using a public internet path.

---

## LAB 5 – Create Systems Manager Interface Endpoints

### Required Endpoints

Create the following Interface Endpoints:

```text
com.amazonaws.<region>.ssm
com.amazonaws.<region>.ssmmessages
com.amazonaws.<region>.ec2messages
```

### Step 1 – Create Endpoint

1. Go to **VPC → Endpoints**
2. Click **Create endpoint**
3. Select **AWS services**
4. Search for `ssm`
5. Select the Interface endpoint
6. Choose your VPC
7. Select the private subnet
8. Enable **Private DNS**
9. Attach a Security Group that allows HTTPS from your private instance SG
10. Click **Create endpoint**

Repeat for:

- `ssmmessages`
- `ec2messages`

### Endpoint Security Group

Inbound rule:

| Type | Port | Source |
|---|---:|---|
| HTTPS | 443 | private-ec2-sg |

### Outcome

Private EC2 instances can communicate with Systems Manager without needing internet access.

---

## LAB 6 – Test Session Manager Access

### Step 1 – Attach IAM Role

Attach an IAM role to the private EC2 instance with:

```text
AmazonSSMManagedInstanceCore
```

Console path:

```text
EC2 → Instances → Select instance → Actions → Security → Modify IAM role
```

### Step 2 – Verify Managed Node

1. Go to **Systems Manager**
2. Click **Fleet Manager** or **Managed nodes**
3. Confirm the private EC2 instance appears as online

### Step 3 – Start Session

1. Go to **Systems Manager → Session Manager**
2. Click **Start session**
3. Select the private instance
4. Click **Start session**

### Outcome

You can administer the private instance without SSH and without a public IP.

---

## LAB 7 – Security Group vs NACL Testing

### Security Group Test

1. Confirm SSM works
2. Remove HTTPS outbound from the private EC2 Security Group or inbound from endpoint SG
3. Retry Session Manager
4. Observe failure
5. Restore the rule

### NACL Test

1. Go to **VPC → Network ACLs**
2. Create a custom NACL
3. Associate it with the private subnet
4. Add a temporary deny rule for selected traffic
5. Test connectivity
6. Restore normal rules

### Key Learning

| Control | Behaviour | Scope |
|---|---|---|
| Security Group | Stateful | Instance/ENI level |
| NACL | Stateless | Subnet level |

### Outcome

You understand how layered network controls affect private connectivity.

---

## Final Project Outcome

You implemented:

- Bastion-based controlled access
- Private EC2 workload isolation
- S3 Gateway Endpoint
- SSM Interface Endpoints
- DNS resolution for private services
- Security Group and NACL validation

This is a real enterprise AWS networking pattern used for private workloads.
