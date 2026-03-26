# Industrial Setup Standard – Step-by-Step Solution

****LAB 1 – Create Lambda Function**<br/>
**Step 1 – Navigate to Lambda**<br/>
- AWS Console → Lambda
- Click Create function

**Step 2 – Configure Function**
- Select: ```Author from scratch```
- Name: ```s3-file-processor```
- Runtime: ```Python 3.x```
- Permissions: ```Create new IAM role (basic Lambda permissions)```
- Click the Create function

**Step 3 – Add Code**
- Replace code with: <br/>
```def lambda_handler(event, context):``` <br/>
    ```print("S3 Event Received:", event)``` <br/>
    ```return "Success"```
- Click Deploy
  
**Outcome**<br/>
Lambda function created

**LAB 2 – Add S3 Trigger**<br/>
**Step 1 – Configure Trigger**<br/>
- Lambda → Function → Add trigger
- Select: ```S3```
- Choose: ```Existing bucket (Day 5 bucket)```
- Event type: ```PUT (Object Created)```
- Click Add

**Outcome** <br/>
Lambda triggers when a file is uploaded

**LAB 3 – Enable CloudWatch Logging** <br/>
**Step 1 – Test Logging**<br/>
- Upload a file to S3
- Go to: ```CloudWatch → Logs → Log groups```
- Open Lambda log group

**Outcome**<br/>
Logs show S3 event execution

**Final Project Outcome**<br/>
- Serverless function deployed
- Event-driven trigger from S3
- Logging enabled via CloudWatch
