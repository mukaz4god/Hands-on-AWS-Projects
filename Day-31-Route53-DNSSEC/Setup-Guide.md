# Day 39 – Route 53 DNSSEC

# Setup Guide – Industrial Standard Step-by-Step Solution

## Architecture Overview

DNSSEC protects DNS responses by allowing resolvers to validate that records have not been tampered with.

You will configure:

- Route 53 hosted zone
- DNSSEC signing
- Key Signing Key
- DS record at parent zone/registrar
- DNS integrity validation

---

## LAB 1 – Prepare Route 53 Hosted Zone

### Step 1 – Open Route 53

1. Go to **AWS Console**
2. Search for **Route 53**
3. Click **Hosted zones**

### Step 2 – Select Hosted Zone

Select your public hosted zone, for example:

```text
example.com
```

### Step 3 – Confirm Domain Control

You must be able to update DS records at the registrar or parent zone.

### Outcome

The hosted zone is ready for DNSSEC configuration.

---

## LAB 2 – Enable DNSSEC Signing

### Step 1 – Open DNSSEC Settings

1. Inside the hosted zone, find **DNSSEC signing**
2. Click **Enable DNSSEC signing**

### Step 2 – Create Key Signing Key

Create a Key Signing Key.

Example name:

```text
route53-ksk
```

Route 53 uses AWS KMS for key management.

### Step 3 – Enable Signing

Complete the wizard and enable signing.

### Outcome

Route 53 begins signing DNS records for the hosted zone.

---

## LAB 3 – Retrieve DS Record

### Step 1 – Open KSK Details

1. In the DNSSEC section, select the Key Signing Key
2. Locate the DS record information

You should see values such as:

- Key tag
- Algorithm
- Digest type
- Digest

### Outcome

You have the DS record needed to establish the chain of trust.

---

## LAB 4 – Add DS Record at Registrar

### Step 1 – Open Registrar DNSSEC Settings

Go to the registrar where your domain is registered.

Examples:

- Route 53 Domains
- Namecheap
- GoDaddy
- Cloudflare registrar
- Other registrar

### Step 2 – Add DS Record

Enter:

- Key tag
- Algorithm
- Digest type
- Digest

Save changes.

### Important

DNSSEC is not fully validated until the parent zone has the DS record.

### Outcome

The DNSSEC chain of trust is established.

---

## LAB 5 – Test DNSSEC Validation

### Option 1 – Use dig

Run:

```bash
dig +dnssec example.com
```

Look for DNSSEC-related records and validation indicators.

### Option 2 – Use Online DNSSEC Analyzer

Use a DNSSEC validation tool to check:

- DS record exists
- DNSKEY exists
- Chain of trust is valid
- No signing errors

### Troubleshooting

If validation fails, check:

- DS record values
- KSK status
- Registrar propagation
- Hosted zone signing status
- DNSSEC algorithm mismatch

### Outcome

DNS integrity validation is confirmed.

---

## LAB 6 – Operational Best Practices

Document:

- KSK name
- Registrar DS record status
- Validation test results
- Recovery plan if DNSSEC misconfiguration causes resolution failure

### Best Practice

DNSSEC misconfiguration can cause domain resolution failures. Always validate carefully and document rollback steps.

### Outcome

DNSSEC is enabled safely and operationally documented.

---

## Final Project Outcome

You implemented:

- DNSSEC signing
- Key Signing Key
- DS record publication
- DNSSEC validation testing
- DNS integrity documentation

This helps protect public DNS against spoofing and tampering attacks.
