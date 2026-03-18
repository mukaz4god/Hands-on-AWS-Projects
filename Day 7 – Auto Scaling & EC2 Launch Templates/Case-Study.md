## Case Study – Scaling a High-Traffic Web Application
**Business Scenario**
A SaaS company has deployed its application using EC2 instances behind an Application Load Balancer **(from Day 6)**. However, during peak traffic hours, users experience slow response times due to limited compute capacity. 

To solve this, the company wants to implement automatic horizontal scaling, ensuring:
- Instances scale out during high demand
- Instances scale in during low demand
- High availability is maintained
- Cost is optimized

**Your Task:** You are the Cloud Engineer responsible for implementing:

- EC2 Launch Templates
- Auto Scaling Groups (ASG)
- Dynamic scaling policies
- Integration with ALB
