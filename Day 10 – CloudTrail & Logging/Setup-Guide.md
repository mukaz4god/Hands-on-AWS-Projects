# Industrial Setup Standard – Step-by-Step Solution

**LAB 1 – Enable CloudTrail (Multi-Region)** <br/>

**Step 1 – Navigate to CloudTrail**<br/>
- AWS Console → CloudTrail
- Click Trails
- Click Create trail

**Step 2 – Configure Trail**<br/>
- Name: ```kjf-organization-trail```
- Apply to: ```All regions```

**Outcome**<br/>
All AWS API activity is captured across regions

**LAB 2 – Configure Central S3 Logging**<br/>

**Step 1 – Create S3 Bucket**<br/>
- Go to S3
- Click Create bucket: ```kfj-cloudtrail-logs-bucket```
- Enable:
  - Block public access
  - Encryption (SSE-S3 or SSE-KMS)

**Step 2 – Attach Bucket to CloudTrail**<br/>
- In CloudTrail setup → select this bucket

**Outcome**<br/>
Centralized storage for audit logs

**LAB 3 – Enable Log File Validation**<br/>

**Step 1 – Enable Validation**<br/>
- In CloudTrail setup: ```Enable log file validation```

**Outcome**<br/>
Ensures logs are not tampered with (integrity validation)

**LAB 4 – Query Logs with Athena**<br/>

**Step 1 – Navigate to Athena**<br/>
- AWS Console → Athena
- Set query result location (S3)

**Step 2 – Create Table (Simplified)** <br/>
- Use AWS-provided CloudTrail table template OR run:
  ```CREATE DATABASE cloudtrail_logs;```

**Step 3 – Query Logs**<br/>
- Example query:
```SELECT eventname, useridentity.username, eventtime FROM cloudtrail_logs LIMIT 10;```
<br/>

**Outcome** <br/>
Ability to investigate user activity using SQL











