# Day 39 – Route 53 DNSSEC

## Project Goal

To protect public DNS integrity by enabling DNSSEC signing, configuring the Key Signing Key, and validating the chain of trust.

## Services Used

- Amazon Route 53
- DNSSEC
- AWS KMS
- Domain Registrar DNSSEC Settings

## Outcome

A DNSSEC-enabled Route 53 hosted zone was implemented, strengthening DNS integrity and helping protect against spoofing and tampering attacks.

## Key Learning

- DNSSEC signs DNS responses.
- KSK and DS records establish trust.
- Registrar configuration is required.
- DNSSEC must be validated carefully.
