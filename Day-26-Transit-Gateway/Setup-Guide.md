# Day 34 – Transit Gateway

# Setup Guide – Industrial Standard Step-by-Step Solution

## Architecture Overview

You will create:

- Shared Services VPC
- Development VPC
- Production VPC
- One AWS Transit Gateway
- VPC attachments
- Route table updates
- Cross-VPC connectivity test

Example CIDR ranges:

| VPC | CIDR |
|---|---|
| Shared Services | 10.10.0.0/16 |
| Development | 10.20.0.0/16 |
| Production | 10.30.0.0/16 |

---

## LAB 1 – Create Multiple VPCs

### Step 1 – Open VPC Console

1. Go to **AWS Console → VPC**
2. Click **Your VPCs**
3. Click **Create VPC**

### Step 2 – Create Shared Services VPC

Name:

```text
shared-services-vpc
```

CIDR:

```text
10.10.0.0/16
```

Create at least one subnet:

```text
10.10.1.0/24
```

### Step 3 – Create Development VPC

Name:

```text
dev-vpc
```

CIDR:

```text
10.20.0.0/16
```

Subnet:

```text
10.20.1.0/24
```

### Step 4 – Create Production VPC

Name:

```text
prod-vpc
```

CIDR:

```text
10.30.0.0/16
```

Subnet:

```text
10.30.1.0/24
```

### Important

Do not use overlapping CIDR ranges. Transit Gateway routing will not work correctly with overlapping networks.

### Outcome

You have three isolated VPCs ready for centralized connectivity.

---

## LAB 2 – Launch Test EC2 Instances

Launch one EC2 instance in each VPC.

Example names:

```text
shared-test-instance
dev-test-instance
prod-test-instance
```

Security Group test rule:

| Type | Port | Source |
|---|---:|---|
| ICMP | All | Other VPC CIDRs |
| SSH | 22 | Admin/Bastion source |

For production, avoid broad ICMP and restrict access to required ports only.

### Outcome

You have test workloads to validate cross-VPC communication.

---

## LAB 3 – Create Transit Gateway

### Step 1 – Open Transit Gateway Console

1. Go to **VPC**
2. Scroll to **Transit Gateways**
3. Click **Create transit gateway**

### Step 2 – Configure Transit Gateway

Name:

```text
enterprise-tgw
```

Recommended lab settings:

- Default route table association: Enabled
- Default route table propagation: Enabled
- DNS support: Enabled

Click **Create transit gateway**

### Outcome

The Transit Gateway is created as the central network hub.

---

## LAB 4 – Attach VPCs to Transit Gateway

### Step 1 – Create Attachment for Shared Services VPC

1. Go to **Transit Gateway Attachments**
2. Click **Create transit gateway attachment**
3. Resource type: **VPC**
4. Transit Gateway: `enterprise-tgw`
5. VPC: `shared-services-vpc`
6. Select subnet
7. Click **Create attachment**

Repeat the same process for:

- `dev-vpc`
- `prod-vpc`

### Outcome

All VPCs are attached to the Transit Gateway.

---

## LAB 5 – Update VPC Route Tables

Each VPC route table must know how to reach the other VPC CIDRs through the Transit Gateway.

### Dev VPC Route Table

Add:

| Destination | Target |
|---|---|
| 10.10.0.0/16 | Transit Gateway |
| 10.30.0.0/16 | Transit Gateway |

### Shared Services VPC Route Table

Add:

| Destination | Target |
|---|---|
| 10.20.0.0/16 | Transit Gateway |
| 10.30.0.0/16 | Transit Gateway |

### Production VPC Route Table

Add:

| Destination | Target |
|---|---|
| 10.10.0.0/16 | Transit Gateway |
| 10.20.0.0/16 | Transit Gateway |

### Outcome

Each VPC can route traffic to the others through the Transit Gateway.

---

## LAB 6 – Review Transit Gateway Route Table

1. Go to **Transit Gateway Route Tables**
2. Select the default TGW route table
3. Check propagated routes
4. Confirm all VPC CIDR ranges appear
5. If routes are missing, enable propagation for each attachment

### Outcome

Transit Gateway routing is validated centrally.

---

## LAB 7 – Test Cross-VPC Communication

From the Dev EC2 instance, test connectivity to the Shared Services instance private IP:

```bash
ping <shared-instance-private-ip>
```

From the Production EC2 instance, test connectivity to Shared Services:

```bash
ping <shared-instance-private-ip>
```

If ICMP is blocked, test application ports instead, such as HTTP or SSH, depending on your rules.

### Troubleshooting Checklist

- Are the VPC CIDRs non-overlapping?
- Are VPC route tables updated?
- Are TGW routes propagated?
- Do Security Groups allow traffic?
- Do NACLs allow inbound and outbound traffic?

### Outcome

Cross-VPC communication is successfully validated.

---

## Final Project Outcome

You implemented:

- Multiple isolated VPCs
- Transit Gateway as a central routing hub
- VPC attachments
- VPC route updates
- Cross-VPC communication testing

This is a common enterprise AWS networking architecture.
