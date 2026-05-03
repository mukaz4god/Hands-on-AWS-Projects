# Day 39 – Route 53 DNSSEC

# Interview Ready Wording

## Question: What does DNSSEC protect against?

**Answer:**  
DNSSEC helps protect against DNS spoofing and tampering by allowing resolvers to validate that DNS responses are authentic and have not been modified.

---

## Question: What is a Key Signing Key?

**Answer:**  
A Key Signing Key is used in DNSSEC to help sign and validate DNS zone signing keys. In Route 53, the KSK is managed through AWS KMS integration.

---

## Question: Why is the DS record important?

**Answer:**  
The DS record is published in the parent zone or registrar and establishes the chain of trust between the parent zone and the signed hosted zone.

---

## Question: What is a risk of misconfigured DNSSEC?

**Answer:**  
Misconfigured DNSSEC can break domain resolution for validating resolvers, so it must be enabled carefully with validation and rollback planning.
