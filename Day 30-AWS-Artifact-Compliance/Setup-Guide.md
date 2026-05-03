# Day 38 – AWS Artifact Compliance

# Setup Guide – Industrial Standard Step-by-Step Solution

## Architecture Overview

This is a governance and compliance project. You will not deploy infrastructure. Instead, you will learn how to access AWS compliance evidence and translate it into operational responsibilities.

---

## LAB 1 – Access AWS Artifact

### Step 1 – Open AWS Artifact

1. Go to **AWS Console**
2. Search for:

```text
Artifact
```

3. Open **AWS Artifact**

### Step 2 – Review Dashboard

You should see options for:

- Reports
- Agreements
- Compliance documents

### Outcome

You know where AWS compliance evidence is located.

---

## LAB 2 – Explore SOC Reports

### Step 1 – Find SOC Reports

1. In AWS Artifact, go to **Reports**
2. Search for:

```text
SOC
```

3. Review available SOC reports

Common examples:

- SOC 1
- SOC 2
- SOC 3

### Step 2 – Document Relevance

Create notes:

```text
Report reviewed:
Purpose:
Relevant services:
Customer responsibility:
```

### Best Practice

Downloaded reports may contain sensitive compliance information. Store them securely and do not upload them to a public GitHub repository.

### Outcome

You understand how SOC evidence supports audit and customer assurance.

---

## LAB 3 – Explore ISO Certifications

### Step 1 – Search ISO Documents

In Artifact Reports, search:

```text
ISO
```

Review available certifications and attestations.

Examples may include:

- ISO 27001
- ISO 27017
- ISO 27018

### Step 2 – Document Control Relevance

Map what AWS covers, such as:

- Data center security
- Infrastructure security
- Service-level compliance

Then map customer responsibilities, such as:

- IAM permissions
- Encryption configuration
- Logging
- Patch management
- Data classification

### Outcome

You understand how ISO certifications support enterprise cloud assurance.

---

## LAB 4 – Explore PCI Compliance Reports

### Step 1 – Search PCI Reports

Search:

```text
PCI
```

Review PCI-related documentation available in Artifact.

### Step 2 – Map PCI Responsibility

Example mapping:

| Area | AWS Responsibility | Customer Responsibility |
|---|---|---|
| Physical data center | AWS | N/A |
| IAM least privilege | Shared | Customer configuration |
| Encryption | AWS provides services | Customer enables/configures |
| Logging | AWS provides services | Customer enables/monitors |

### Outcome

You understand that AWS compliance does not automatically make your workload compliant.

---

## LAB 5 – Build Shared Responsibility Matrix

Create a file called:

```text
shared-responsibility-matrix.md
```

Example:

| Control Area | AWS Responsibility | Customer Responsibility |
|---|---|---|
| Physical security | Secures data centers | Validate reports |
| IAM | Provides IAM service | Create least-privilege policies |
| Logging | Provides CloudTrail/CloudWatch | Enable and monitor logs |
| Encryption | Provides KMS/S3 encryption | Configure encryption policies |
| Patching | Patches managed services | Patch EC2 guest OS |

### Outcome

You can explain cloud compliance clearly to auditors, hiring managers, and security teams.

---

## LAB 6 – Write Compliance Review Summary

Document:

- Reports reviewed
- Services in scope
- Customer-side controls still required
- Evidence storage considerations
- Summary of shared responsibility

### Outcome

You produce a professional compliance-awareness artifact.

---

## Final Project Outcome

You implemented:

- AWS Artifact exploration
- SOC report awareness
- ISO certification awareness
- PCI report awareness
- Shared responsibility mapping
- Compliance documentation practice

This supports enterprise cloud security, audit readiness, and governance awareness.
