# Day 40 – AWS Network Firewall

# Setup Guide – Industrial Standard Step-by-Step Solution

## Architecture Overview

AWS Network Firewall provides managed network traffic inspection.

You will create:

- Stateless rule group
- Stateful rule group
- Firewall policy
- Network Firewall
- Firewall subnet/endpoints
- Route table updates
- Traffic inspection tests

Example traffic path:

```text
Workload Subnet → Firewall Endpoint → Internet/NAT/Other Destination
```

---

## LAB 1 – Plan Firewall Subnets

### Step 1 – Review VPC Design

You need dedicated firewall subnets in the VPC.

Example:

| Subnet | Purpose |
|---|---|
| Public subnet | ALB/NAT/Bastion |
| Private subnet | Workloads |
| Firewall subnet | Network Firewall endpoint |

### Step 2 – Create Firewall Subnet

1. Go to **VPC → Subnets**
2. Click **Create subnet**
3. Select your VPC
4. Name:

```text
firewall-subnet-a
```

5. CIDR example:

```text
10.0.10.0/24
```

### Outcome

The VPC has a subnet dedicated to firewall endpoints.

---

## LAB 2 – Create Stateless Rule Group

### Step 1 – Open Network Firewall

1. Go to **VPC**
2. Scroll to **Network Firewall**
3. Click **Rule groups**
4. Click **Create rule group**

### Step 2 – Configure Stateless Rule Group

Name:

```text
stateless-basic-rules
```

Type:

```text
Stateless
```

Capacity:

```text
100
```

### Step 3 – Add Stateless Rule

Example rule:

- Match protocol: TCP
- Source: workload subnet CIDR
- Destination: anywhere
- Destination port: 80 or 443
- Action: Forward to stateful rule group

### Outcome

The first inspection layer can forward selected traffic to the stateful engine.

---

## LAB 3 – Create Stateful Rule Group

### Step 1 – Create Stateful Group

1. Go to **Rule groups**
2. Click **Create rule group**
3. Type:

```text
Stateful
```

Name:

```text
stateful-egress-rules
```

Capacity:

```text
100
```

### Step 2 – Add Stateful Rules

Example rule ideas:

- Alert on HTTP traffic
- Drop traffic to prohibited domain
- Reject specific destination pattern

Example Suricata-style rule for learning:

```text
alert http any any -> any any (msg:"HTTP traffic observed"; sid:1000001; rev:1;)
```

### Outcome

The firewall can inspect traffic flows at a deeper level.

---

## LAB 4 – Create Firewall Policy

### Step 1 – Create Policy

1. Go to **Firewall policies**
2. Click **Create firewall policy**

Name:

```text
enterprise-firewall-policy
```

### Step 2 – Add Rule Groups

Attach:

- `stateless-basic-rules`
- `stateful-egress-rules`

Set default stateless action based on your design:

```text
Forward to stateful rule groups
```

### Outcome

Firewall policy combines stateless and stateful inspection logic.

---

## LAB 5 – Deploy AWS Network Firewall

### Step 1 – Create Firewall

1. Go to **Firewalls**
2. Click **Create firewall**
3. Name:

```text
enterprise-network-firewall
```

4. Choose your VPC
5. Select firewall subnet
6. Attach firewall policy
7. Click **Create firewall**

### Step 2 – Wait for Endpoint

Wait until firewall status is ready.

### Outcome

AWS Network Firewall endpoint is deployed inside the VPC.

---

## LAB 6 – Update Route Tables

### Important

Traffic must be routed through the firewall endpoint, otherwise it will not be inspected.

### Example Route Changes

For workload subnet route table:

| Destination | Target |
|---|---|
| 0.0.0.0/0 | Firewall endpoint |

For firewall subnet route table:

| Destination | Target |
|---|---|
| 0.0.0.0/0 | NAT Gateway or Internet Gateway path |

Exact routing depends on your VPC design.

### Outcome

Selected traffic is now steered through AWS Network Firewall.

---

## LAB 7 – Test Traffic Inspection

### Step 1 – Generate Allowed Traffic

From an EC2 instance:

```bash
curl https://aws.amazon.com
```

### Step 2 – Generate Traffic Matching Alert Rule

```bash
curl http://example.com
```

### Step 3 – Review Logs

Enable and review firewall logs if configured:

- Alert logs
- Flow logs

### Step 4 – Validate Blocking

If you created a drop rule, attempt traffic to the blocked destination and confirm it fails.

### Outcome

Network Firewall inspection is validated.

---

## LAB 8 – Operational Best Practices

- Start with alert rules before blocking.
- Test in non-production first.
- Use dedicated inspection subnets.
- Use clear route table documentation.
- Log firewall activity to CloudWatch or S3.
- Avoid routing production traffic until rules are validated.

### Outcome

Firewall deployment follows a safer enterprise rollout approach.

---

## Final Project Outcome

You implemented:

- AWS Network Firewall
- Stateless rule group
- Stateful rule group
- Firewall policy
- Route table traffic steering
- Traffic inspection testing

This provides centralized inspection and deeper network-layer protection for VPC traffic.
