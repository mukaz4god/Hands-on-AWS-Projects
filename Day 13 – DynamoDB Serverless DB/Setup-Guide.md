**LAB 1 – Create DynamoDB Table**<br/>
- AWS Console → DynamoDB
- Click Create table
  - Table name: ```kfj-users-table```
  - Primary key: ```userId (String)```
- Enable Security
  - Enable encryption (default AWS owned or KMS)
  - Enable Point-in-Time Recovery (backups)
    
**Outcome**<br/>
Secure NoSQL database created

**LAB 2 – Integrate with Lambda** <br/>
- Lambda → Add permission
- Attach policy: ```AmazonDynamoDBFullAccess (lab only)```
- Update Lambda Code <br/>
  ``` import boto3```<br/>
  ```dynamodb = boto3.resource('dynamodb')```<br/>
  ```def lambda_handler(event, context): ```<br/>
  ```table.put_item(Item={"userId": "1", "name": "Test"})```<br/>
  ```return "Item added"```table = dynamodb.Table('users-table')```

**LAB 3 – Test CRUD**
- Invoke Lambda
- Check DynamoDB → Items

**Outcome**<br/>
Lambda performs database operations
