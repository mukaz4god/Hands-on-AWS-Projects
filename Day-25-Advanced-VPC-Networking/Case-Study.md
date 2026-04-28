# Advanced VPC Networking

## Case Study – Private Service Access with Controlled Administration

### Business Scenario

A regulated application team runs backend EC2 instances in private subnets. These instances must access AWS services such as Amazon S3 and AWS Systems Manager without being exposed to the public internet.

The security team also wants to validate how Security Groups and Network ACLs behave differently so they can apply layered network controls correctly.

### Business Requirements

- EC2 instances must remain in private subnets.
- Private instances must not have public IP addresses.
- Administrators must access private workloads through a controlled path.
- S3 access should use a Gateway VPC Endpoint.
- Systems Manager access should use Interface VPC Endpoints.
- DNS resolution must work correctly for private endpoint access.
- Security Group and NACL behaviour must be tested.

### Your Role

You are the Cloud Security / Network Engineer responsible for designing and implementing a secure private networking pattern that supports private service access and controlled administration.

### Project Goal

Build a private networking architecture where EC2 instances can securely access AWS services without public internet exposure, while validating Security Group and NACL behaviour.
