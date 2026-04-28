# Day 37 – API Gateway Deep Dive

# Setup Guide – Industrial Standard Step-by-Step Solution

## Architecture Overview

The architecture:

```text
Client → API Gateway REST API → Lambda Function
```

Security controls:

- API key
- Usage plan
- Throttling
- Resource policy
- CloudWatch logs

---

## LAB 1 – Create Lambda Backend

### Step 1 – Create Lambda Function

1. Go to **Lambda**
2. Click **Create function**
3. Choose **Author from scratch**
4. Name:

```text
orders-api-function
```

5. Runtime:

```text
Python 3.x
```

6. Click **Create function**

### Step 2 – Add Test Code

```python
import json

def lambda_handler(event, context):
    return {
        "statusCode": 200,
        "headers": {
            "Content-Type": "application/json"
        },
        "body": json.dumps({
            "message": "Secure API request processed successfully"
        })
    }
```

Click **Deploy**.

### Outcome

Lambda backend is ready.

---

## LAB 2 – Create REST API

### Step 1 – Open API Gateway

1. Go to **API Gateway**
2. Click **Create API**
3. Choose **REST API**
4. Click **Build**

API name:

```text
secure-orders-api
```

Endpoint type:

```text
Regional
```

Click **Create API**.

### Outcome

REST API container is created.

---

## LAB 3 – Create Resource and Method

### Step 1 – Create Resource

1. Click **Actions**
2. Click **Create Resource**
3. Resource name:

```text
orders
```

Resource path:

```text
/orders
```

Click **Create Resource**.

### Step 2 – Create Method

1. Select `/orders`
2. Click **Actions**
3. Click **Create Method**
4. Choose:

```text
POST
```

5. Integration type:

```text
Lambda Function
```

6. Select your Lambda function
7. Save and allow API Gateway permission

### Outcome

The REST API is integrated with Lambda.

---

## LAB 4 – Deploy API

1. Click **Actions**
2. Choose **Deploy API**
3. Deployment stage:

```text
prod
```

4. Click **Deploy**
5. Copy the Invoke URL

### Test

```bash
curl -X POST https://api-id.execute-api.region.amazonaws.com/prod/orders
```

### Outcome

The API can invoke Lambda.

---

## LAB 5 – Configure Throttling

### Step 1 – Open Stage Settings

1. Go to **Stages**
2. Select `prod`
3. Open **Default Method Throttling**

Example:

```text
Rate: 10 requests per second
Burst: 20 requests
```

Save changes.

### Outcome

The API has protection against excessive request rates.

---

## LAB 6 – Configure API Key and Usage Plan

### Step 1 – Require API Key on Method

1. Go to `/orders → POST → Method Request`
2. Set **API Key Required** to:

```text
true
```

3. Redeploy the API

### Step 2 – Create API Key

1. Go to **API Keys**
2. Click **Create API key**
3. Name:

```text
partner-client-key
```

4. Enable the key

### Step 3 – Create Usage Plan

1. Go to **Usage Plans**
2. Click **Create**
3. Name:

```text
partner-usage-plan
```

Set:

```text
Rate: 10
Burst: 20
Quota: 1000 requests per month
```

4. Associate the `prod` stage
5. Add the API key

### Test Without Key

```bash
curl -X POST https://api-url/prod/orders
```

Expected: Forbidden.

### Test With Key

```bash
curl -X POST https://api-url/prod/orders -H "x-api-key: YOUR_API_KEY"
```

Expected: Success.

### Outcome

API access is controlled using API keys and usage plans.

---

## LAB 7 – Configure Resource Policy

### Step 1 – Open Resource Policy

1. Open your API
2. Click **Resource Policy**

Example source IP restriction:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "execute-api:Invoke",
      "Resource": "execute-api:/*",
      "Condition": {
        "IpAddress": {
          "aws:SourceIp": "YOUR_PUBLIC_IP/32"
        }
      }
    }
  ]
}
```

Save and redeploy.

### Outcome

API access is restricted at the API Gateway boundary.

---

## LAB 8 – Observe Lambda Execution

1. Go to **CloudWatch**
2. Click **Log groups**
3. Open Lambda log group
4. Invoke API
5. Confirm execution logs appear

### Outcome

API calls and Lambda execution are observable.

---

## Final Project Outcome

You implemented:

- REST API
- Lambda integration
- API keys
- Usage plans
- Throttling
- Resource policy
- API testing and observability

This is a strong secure serverless API architecture.
