# Route 53 DNSSEC

## Case Study – Protecting DNS Integrity

### Business Scenario

A company hosts its public domain in Amazon Route 53. The security team wants to reduce the risk of DNS spoofing and tampering by enabling DNSSEC signing.

The organization must configure DNSSEC, create a Key Signing Key, publish the DS record at the registrar, and validate that DNS integrity protection is working.

### Security Requirements

- Enable DNSSEC signing.
- Create or configure a Key Signing Key.
- Add DS record to parent zone or registrar.
- Test DNSSEC validation.
- Document DNS integrity protection.

### Your Role

You are the Cloud / DNS Security Engineer responsible for enabling DNSSEC on a Route 53 hosted zone.

### Project Goal

Protect DNS integrity by enabling DNSSEC signing and establishing a valid chain of trust.
