## Business Scenario

A regulated SaaS company is deploying backend services in AWS. For security reasons, backend servers must not be exposed to the public internet. However, system administrators still require SSH access for maintenance, patching, and incident response.

**Security Requirements**
- No direct public access to private servers
- Centralised controlled entry point for administrators
- Least-privilege network rules
- Full alignment with AWS security best practices

**Solution Approach**
- Implement a Bastion Host architecture:
- Public EC2 instance (Bastion Host) acts as the secure entry point
- Private EC2 instance hosts sensitive workloads
- Access restricted using tightly scoped Security Groups
- SSH access controlled and auditable

**Your Role**
You are the Cloud Security Engineer responsible for designing secure administrative access to private infrastructure.
