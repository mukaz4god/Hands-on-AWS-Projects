## Industrial Setup Standard – Step-by-Step Solution

**LAB 1 – Create Hosted Zone**<br/>
**Step 1 – Navigate to Route 53**
- AWS Console → Route 53
- Click Hosted zones
- Click Create hosted zone

**Step 2 – Configure Hosted Zone**<br/>
- Domain name:```yourdomain.com```
- Type:```Public hosted zone```
- Click Create

**Outcome**<br/>
DNS zone created for your domain

**LAB 2 – Create DNS Records**<br/>
**Step 1 – Create A Record (ALB Mapping)**
- Click Create record
  - Record type:```A – IPv4 address```
  - Alias: ```Enable```
  - Target: Select your Application Load Balancer

- Click Create record

**Outcome**
Domain now points to ALB

**Step 2 – Create CNAME Record**<br/>
- Example: ```www → yourdomain.com```
- Type: ```CNAME```

**Step 3 – Create MX Record (Email)**
- Example:
```
Type: MX
Value: mail.yourdomain.com
```
**Outcome**<br/>
DNS records configured

**LAB 3 – Test DNS Resolution**<br/>
**Step 1 – Verify Domain**<br/>
Use browser: ```http://yourdomain.com```

**Step 2 – CLI Test**
```nslookup yourdomain.com```
OR
```dig yourdomain.com```

**Outcome**<br/>
Domain resolves to ALB successfully

**LAB 4 – Enable Health Checks & Failover**<br/>
**Step 1 – Create Health Check**
- Route 53 → Health checks
- Click Create health check to point to your EC2 instance (50.10.11.123:80/)

**Configure:**
- Endpoint: ALB DNS
- Protocol: HTTP
- Path: /

**Step 2 – Create Failover Record**<br/>
- Edit A record
- Add: ```Routing policy: Failover```
- Primary → ALB
- Secondary → Backup endpoint

**Outcome**<br/>
Automatic failover if primary becomes unhealthy

**Final Project Outcome** <br/>

I implemented:
- DNS management using Route 53
- Domain mapping to ALB
- Health checks for monitoring
- Failover routing for resilience

# NOTE: Two Ways to Use Route 53 with a GoDaddy Domain
Option 1 (Recommended): Use Route 53 as your DNS provider

This is the cleanest setup.

**Steps:**
- **In Route 53**:
- Create a Hosted Zone for your domain (e.g. example.com)
- AWS will generate 4 nameservers (NS records) <br/>
**In GoDaddy**: Go to your domain → DNS settings
- Replace GoDaddy nameservers with the Route 53 nameservers
- **Back in Route 53:**
- Create records:
- A record → your server IP or ALB
- CNAME → for subdomains

**After propagation, Route 53 is fully managing your DNS.**

**Option 2:** Keep GoDaddy DNS and just point to AWS

- If you don’t want to change nameservers:
- Stay in GoDaddy DNS and add: 
- Add records like:
  - A → EC2 public IP
  - CNAME → AWS services (e.g. CloudFront)

**In this Option 2 setup, Route 53 is NOT used at all — just AWS resources.**





