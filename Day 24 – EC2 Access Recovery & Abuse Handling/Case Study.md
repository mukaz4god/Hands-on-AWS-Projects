## Case Study – Recovering Locked-Out Instances and Responding to Access Incidents

**Business Scenario**

A production operations team receives two common incident types. In one case, an engineer loses the SSH private key for a Linux instance. In another, a Windows server password must be recovered after an access issue. Security also raises an abuse alert involving suspicious access attempts, so the team must restore access safely while preserving evidence and limiting blast radius.

AWS documents note that EC2 does not keep a copy of your private key, so the private key itself cannot be recovered; instead, supported recovery methods must be used. AWS also provides the AWSSupport-ResetAccess runbook to recover access for lost keys and Windows password issues.

**Task**

You are the Incident Response / Cloud Operations Engineer responsible for:

- Recovering access without destroying evidence
- Using Session Manager where possible
- Using user data or Automation for Linux recovery
- Using EBS volume swap when deeper repair is needed
- Recovering Windows access safely
- Testing EC2 Instance Connect as a just-in-time method, where supported
