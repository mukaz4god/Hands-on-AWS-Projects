**LAB 1 – Enable AWS Config**<br/>
1. AWS Console → AWS Config
2. Click Get started

Enable:

- Record all resources
- Deliver logs to S3

**Outcome**<br/>
Continuous configuration tracking

**LAB 2 – Enable Managed Rules**<br/>
1. Config → Rules → Add rule

Example: ```s3-bucket-public-read-prohibited```

**Outcome**<br/>
Compliance rules active

**LAB 3 – Create Custom Rule (Optional)**<br/>
- Use Lambda for custom logic

**Outcome**
Custom compliance checks

**LAB 4 – Auto-Remediation**
1. Select rule Click Manage remediation

Choose:

- SSM Automation or Lambda

**Outcome**
Automatic fixing of violations

**Final Project Outcome**<br/>
Continuous compliance monitoring
Automated remediation
