**LAB 1 – Block Public Access**<br/>
1. S3 → Bucket → Permissions
2. Enable:
  - Block all public access

**Outcome**<br/>
No public exposure

**LAB 2 – Configure Bucket Policy**<br/>

Restrict access to specific IAM roles

**Outcome**<br/>
Least-privilege enforced

**LAB 3 – Enable Logging & Replication**</br>
- Enable server access logging
- Enable cross-region replication

**Outcome**<br/>
Audit + disaster recovery

**LAB 4 – Enable MFA Delete**<br/>
1. Use CLI:
```
aws s3api put-bucket-versioning \
--bucket your-bucket \
--versioning-configuration Status=Enabled,MFADelete=Enabled \
--mfa "arn-of-mfa-device code"
```

**Outcome**<br/>
Protection against accidental deletion

**Final Project Outcome**<br/>
- Hardened S3 security
- Audit logging
- Data protection mechanisms
