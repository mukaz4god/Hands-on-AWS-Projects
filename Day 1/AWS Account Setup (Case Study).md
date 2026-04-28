**📌 Case Study Title**

AWS Account Security Baseline for a KFJ Solutions Cloud Migration

**🧩 Business Problem**

KFJ Solutions Ltd, a fintech startup, planned to migrate sensitive payment services to AWS but lacked:

* A defined cloud security baseline
* Identity protection controls
* Audit logging
* Cost governance

**This created risks of:**
* Root account compromise
* Undetected malicious activity
* Unexpected cloud costs

**🎯 Objectives**
* Secure the AWS root account
* Enforce IAM best practices
* Enable full audit logging
* Prevent unexpected spend
* Align with AWS Well-Architected Security Pillar

**🛠️ Solution Design**
**Security Controls Implemented <br/>**

**Root MFA:**              Prevented unauthorized root access<br/>
**IAM Admin User:**	        Eliminated operational root usage <br/>
**AWS Budgets:**            Cost anomaly detection & alerts </br>
**CloudTrail:**	            Full audit logging across regions <br/>
**IAM Access Analyzer:**	    Detection of risky access configurations </br>

🧠 Security Architecture (Narrative)

**Identity access was centralized using IAM, with MFA enforced for privileged access.
All management activity is logged via CloudTrail and securely stored in S3.
Financial guardrails were implemented using AWS Budgets to detect cost anomalies early.**

**✅ Outcomes**

* AWS account secured before workload deployment
* Reduced risk of credential misuse
* Full audit visibility enabled
* Cost governance controls in place
* Alignment with AWS Well-Architected Security Pillar


**🧪 What I’d Improve Next (Shows Maturity)**

* Enable GuardDuty and Security Hub
* Add AWS Config rules for continuous compliance
* Apply least-privilege IAM policies
* Implement infrastructure as code using Terraform
