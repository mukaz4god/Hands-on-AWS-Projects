# Case Study – Event-Driven Messaging System

**Business Scenario** <br/>
KFJ Solutions needs to process events asynchronously to improve scalability and decouple services.

**Task**<br/>
To build an event-driven architecture using SNS, SQS, and Lambda.

**LAB 1 – Create SNS Topic**<br/>
- AWS Console → SNS
- Click Create topic
  - Name: ```app-topic```

**LAB 2 – Create SQS Queue**<br/>
- AWS Console → SQS
- Click Create queue
  - Name: ```app-queue```

**LAB 3 – Subscribe SQS to SNS**<br/>
- SNS → Topic → Create subscription
- Protocol: ```SQS```
- Select queue

**LAB 4 – Add Lambda Subscriber**<br/>
- Lambda → Add trigger
- Select: ```SQS``
- Choose queue

**LAB 5 – Test Flow**<br/>
- Publish message to SNS
- SNS → SQS → Lambda triggers

**Outcome**<br/>
Event-driven pipeline working
