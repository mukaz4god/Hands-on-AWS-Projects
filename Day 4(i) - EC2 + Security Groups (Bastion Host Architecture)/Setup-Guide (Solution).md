## Day 4 (i) — EC2 + Security Groups (Bastion Host Architecture) & Day 4 (ii) - EC2 Secure Access (Bastion vs SSM Comparison)

## PART A

**Case Study — Secure Admin Access to Private Servers**
A regulated organisation deploys backend systems in private subnets. Direct internet access is prohibited. Administrators must connect securely via a controlled entry point.

## Solution 1: Bastion Host (Jump Server)

## Industrial Setup — Step-by-Step (AWS Console Navigation)**
**Step 1 — Launch Bastion Host (Public EC2)**
1. Go to AWS Console → EC2
2. Left menu → Instances → Launch instances
  
**Configuration**:
 - Name: bastion-host
 - Application and OS: Amazon Linux 2 (recommended)
 - Instance type: t2.micro (free tier eligible)
 - Key pair:
  - Create new key pair
  - Download .pem file
 - Network settings → Edit
  - VPC: Select your Day 3 VPC
  - Subnet: Public subnet
  - Auto-assign public IP: Enable
 - Security group
  - Create new security group
   - Name: bastion-sg
 - Add inbound rule: Type(SSH)	Port(22)	Source(MYIP
 - Click Launch instance

**Outcome: Public entry point for admins**

**Step 2: — Launch Private EC2 Instance**
1. Stay in EC2 → Launch instances

**Configuration**:
- Name: private-ec2
- Network settings → Edit
  - VPC: Same VPC
  - Subnet: Private subnet
  - Auto-assign public IP: Disable
  - Security group
    - Create new security group
    - Name: private-ec2-sg
    - Inbound rule: Type(SSH)	Port(22)	Source(bastion-sg)
    - To select SG as source: In source field → search for bastion-sg
    - Launch instance

**Outcome: Private server not internet-accessible**

**Step 3 — Verify Network Isolation**
❌ Test Direct Access (Should Fail)
- From your laptop:
``` ssh ec2-user@<PRIVATE-EC2-PUBLIC-IP> ```
- No public IP → connection impossible

**Outcome: Proper isolation confirmed**

**Step 4 — Connect to Bastion Host**
- EC2 → Instances → Select bastion-host
- Click Connect
- Choose SSH client
- Follow displayed command
Example:<br/>
``` ssh -i key.pem ec2-user@<bastion-public-ip> ```

**Outcome: Admin successfully reaches bastion**

**Step 5 — Connect to Private Instance via Bastion**

From Bastion terminal:
- Copy private key to bastion (if needed)
- SSH using private IP: ``` ssh ec2-user@<private-instance-private-ip> ```

**Outcome: Secure jump access established**

**Step 6 — Additional Industrial Controls (Recommended)**

Enable CloudTrail
- AWS Console → CloudTrail
- Create trail → Apply to all regions → Enable logging to S3

Enable VPC Flow Logs
- Console → VPC → Your VPC → Flow Logs → Create flow log

**Outcome: Auditable production-ready environment**

## Final Outcome

I have implemented:
- Secure bastion architecture
- Network segmentation
- Least-privilege security groups
- Verified controlled access path

## PART B

## Day 4 (ii) — EC2 Secure Access (Bastion vs SSM Comparison)
**Case Study: Migrating to Zero-Trust Administrative Access**
The company wants to evaluate whether to replace bastion hosts with a modern IAM-based solution.

**Part A — Bastion Architecture (Repeat for Comparison)**
Use the exact steps from Project (i).

**PART B - Session Manager (Modern Best Practice)**

**Step 1 - Create IAM for EC2**
1. AWS Console → IAM
2. Left menu → Roles → Create role
  - Configuration
    - Trusted entity: AWS service
    - Use case: EC2
    - Click Next
    - Attach Policy & Search & Select: **AmazonSSMManagedInstanceCore**
    - Click Next → Create role
    - Name: **EC2-SSM-Role**

**Outcome: Instance can communicate with Systems Manager**

**Step 2 - Attach Role to Private EC2**
- Go to EC2 → Instances
- Select private-ec2
- Actions → Security → Modify IAM role
- Select EC2-SSM-Role
- Save

**Step 3 - Ensure SSM Connectivity**
If the instance is in a private subnet:

Option A — NAT Gateway exists
- No action needed

Option B — No NAT
- Create VPC Endpoints:
  - Console → VPC → Endpoints → Create endpoint
  Create these interface endpoints:
  - com.amazonaws.<region>.ssm
  - com.amazonaws.<region>.ssmmessages
  - com.amazonaws.<region>.ec2messages
Attach to private subnet

**Outcome: Private SSM connectivity without internet**

**Step B4 — Verify Instance is Managed**
- Console → Systems Manager
- Left menu → Fleet Manager → Managed nodes
Confirm instance appears as Online

**Step B5 — Start Session Manager Session**
- Systems Manager → Session Manager
- Click Start session
- Select **private-ec2**
- Click Start session
Terminal opens in browser
- No SSH
- No key pair
- No public IP

**Step B6 — Enable Session Logging (Industrial Standard)**
CloudWatch Logs
- Systems Manager → Session Manager → Preferences
- Edit preferences
- Enable:
    - Send logs to CloudWatch
    - Choose log group
S3 Logging (optional)
- Enable S3 logging for long-term retention

**Outcome: Full audit trail of admin activity**

## PART C - Security Comparison (Validated)
**Bastion Path**
- Admin → Internet → Bastion → Private EC2
- Public exposure exists

**Session Manager Path**
- Admin → IAM → AWS Control Plane → Private EC2
- No inbound ports
- No public exposure

## Final Outcome
  
I implemented and evaluated:
1. Traditional Approach
   - Bastion host
   - SSH keys
   - Network-based access control
AND  
2. Modern Approach:
   - IAM-based access
   - Zero inbound exposure
   - Full session auditing
   - Reduced attack surface

