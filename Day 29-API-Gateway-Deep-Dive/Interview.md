# Day 37 – API Gateway Deep Dive

# Interview Ready Wording

## Question: Why use API Gateway with Lambda?

**Answer:**  
API Gateway provides a managed HTTP front door for Lambda functions. It handles request routing, throttling, API keys, authorization options, and integrations, while Lambda provides serverless compute.

---

## Question: What is a usage plan?

**Answer:**  
A usage plan defines throttling and quota limits for clients using API keys. It helps control how much traffic each client can send to the API.

---

## Question: What does a resource policy do in API Gateway?

**Answer:**  
A resource policy controls who can invoke the API. It can restrict access by source IP, VPC endpoint, AWS account, or principal.

---

## Question: Are API keys the same as authentication?

**Answer:**  
No. API keys identify and control clients for usage tracking and rate limiting, but they are not a strong authentication method by themselves. For stronger security, use IAM auth, Lambda authorizers, Cognito, or JWT-based authorization.
