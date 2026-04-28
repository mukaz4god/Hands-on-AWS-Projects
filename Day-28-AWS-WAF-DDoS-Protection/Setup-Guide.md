# Day 36 – AWS WAF & DDoS Protection

# Setup Guide – Industrial Standard Step-by-Step Solution

## Architecture Overview

This project assumes you have one of the following:

- CloudFront distribution
- Application Load Balancer
- API Gateway REST API

You will attach AWS WAF to the public-facing resource.

---

## LAB 1 – Create Web ACL

### Step 1 – Open AWS WAF

1. Go to **AWS Console**
2. Search for **WAF**
3. Open **AWS WAF & Shield**
4. Click **Web ACLs**
5. Click **Create web ACL**

### Step 2 – Configure Web ACL

Name:

```text
prod-web-acl
```

Resource type:

Choose one:

- CloudFront distribution
- Regional resources such as ALB or API Gateway

Default action:

```text
Allow
```

### Step 3 – Associate Resource

Select your:

- CloudFront distribution, or
- ALB, or
- API Gateway stage

### Outcome

A Web ACL is created and associated with your public application.

---

## LAB 2 – Add AWS Managed Rules

### Step 1 – Add Managed Rule Groups

1. In the Web ACL wizard, click **Add rules**
2. Select **Add managed rule groups**
3. Choose AWS managed rule groups such as:
   - Core rule set
   - Known bad inputs
   - SQL database protection
   - Amazon IP reputation list

### Step 2 – Start in Count Mode

For production tuning, start with:

```text
Count
```

After reviewing logs, switch to:

```text
Block
```

### Outcome

The application receives baseline protection against common web attacks.

---

## LAB 3 – Add Rate Limiting Rule

### Step 1 – Create Rate-Based Rule

1. Go to Web ACL rules
2. Click **Add rules**
3. Choose **Add my own rule**
4. Select **Rate-based rule**

Name:

```text
rate-limit-by-ip
```

Aggregation:

```text
Source IP address
```

Threshold example:

```text
1000 requests per 5 minutes
```

Action:

```text
Block
```

For first-time testing, use Count mode.

### Outcome

Requests from overly noisy clients are rate-limited.

---

## LAB 4 – Enable WAF Logging

### Step 1 – Open Logging Settings

1. Open the Web ACL
2. Go to **Logging and metrics**
3. Click **Enable logging**

### Step 2 – Choose Destination

Choose one:

- CloudWatch Logs
- S3
- Kinesis Data Firehose

Recommended for investigation:

```text
CloudWatch Logs for live visibility
S3 for retention
```

### Outcome

WAF request data is available for tuning and investigation.

---

## LAB 5 – Review AWS Shield Protection

### Step 1 – Open Shield Console

1. Go to **AWS WAF & Shield**
2. Click **Shield**

### Step 2 – Understand Protection

AWS Shield Standard is automatically available for common DDoS protection. For higher-risk workloads, review AWS Shield Advanced.

### Key Point

- AWS WAF protects Layer 7 web requests.
- AWS Shield protects against DDoS attacks.

### Outcome

The architecture now includes application-layer and DDoS-aware protection.

---

## LAB 6 – Test Simulated Malicious Traffic

### Safe Test Options

Use a non-production endpoint.

Test rate limiting:

```bash
for i in {1..100}; do curl https://your-domain.com; done
```

Test managed rules with safe suspicious strings:

```bash
curl "https://your-domain.com/?id=' OR '1'='1"
```

### Review Results

Check:

- WAF sampled requests
- WAF logs
- Rule match counts
- CloudWatch metrics

### Outcome

You verify that AWS WAF is inspecting and responding to suspicious traffic.

---

## Final Project Outcome

You implemented:

- Web ACL
- AWS Managed Rules
- Rate limiting
- WAF logging
- AWS Shield awareness
- Simulated malicious traffic testing

This provides a strong web protection baseline for public AWS applications.
