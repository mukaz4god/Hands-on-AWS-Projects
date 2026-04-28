**LAB 1 – Create REST API** <br/>
- AWS Console → API Gateway
- Click Create API
- Select: ```REST API```
- Name: ```serverless-api```

**LAB 2 – Integrate with Lambda** <br/>
- Create resource: ```/process```
- Add method: ```POST```
- Integration type: ```Lambda Function```
- Select your Lambda

**LAB 3 – Enable CORS & Throttling** <br/>
- Enable CORS
  - Select resource → Actions → Enable CORS
- Throttling
  - API Gateway → Stages
  - Enable throttling:<br/>
    ```Rate limit: 10 requests/sec``` <br/>
    ```Burst: 20```

**LAB 4 – Test API**<br/>
- Deploy API
- Copy invoke URL
- Test using browser/Postman

**Outcome**<br/>
API successfully invokes Lambda
