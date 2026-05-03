# Day 33 – Advanced VPC Networking

# Interview Ready Wording

## Question: What is the difference between a Gateway Endpoint and an Interface Endpoint?

**Answer:**  
A Gateway Endpoint is used for services such as S3 and DynamoDB and works through route table entries. An Interface Endpoint creates elastic network interfaces inside the VPC and is commonly used for services like Systems Manager, CloudWatch, and other AWS APIs through PrivateLink.

---

## Question: Why use VPC Endpoints?

**Answer:**  
VPC Endpoints allow private resources to access AWS services without traversing the public internet. This reduces exposure, improves security posture, and supports private networking requirements in regulated environments.

---

## Question: What is the difference between Security Groups and NACLs?

**Answer:**  
Security Groups are stateful and attached to ENIs or instances, while NACLs are stateless subnet-level controls. With NACLs, both inbound and outbound rules must explicitly allow traffic.

---

## Question: Why use Systems Manager Interface Endpoints?

**Answer:**  
Systems Manager endpoints allow private EC2 instances to be managed without public IP addresses, NAT Gateway dependency, or SSH access. This supports a more secure administrative model.
