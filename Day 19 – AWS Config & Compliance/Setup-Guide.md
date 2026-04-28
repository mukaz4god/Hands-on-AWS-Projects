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

**LAB 3 – Deploy a Conformance Pack**<br/>
1. Click on Conformance Packs
2. Click Deploy conformance pack
- Choose either sample template(this contains PCI-DSS, OWASP, etc.), which will help get started and quickly build your own OR
- Choose a 'Template is Ready' if you have an existing template or a template from an Amazon SSM Document, or a template in an S3 bucket.
- Choose a conformance pack name (For example: ```kjf solutions conformance park```)
- Review and click Deploy Conformance Pack

**Outcome**
AWS Config rules & remediation actions active

**LAB 4 – Create Custom Rule (Optional)**<br/>
- Use Lambda for custom logic

**Outcome**
Custom compliance checks

**LAB 5 – Auto-Remediation**
1. Select rule. Click Manage remediation

Choose:

- SSM Automation or Lambda

**Outcome**
Automatic fixing of violations

**Final Project Outcome**<br/>
Continuous compliance monitoring
Automated remediation
