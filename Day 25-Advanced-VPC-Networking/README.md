# Day 33 – Advanced VPC Networking

## Project Goal

To build private AWS networking with secure access paths using a Bastion Host, Gateway VPC Endpoint for S3, Interface Endpoints for Systems Manager, DNS resolution, and layered network controls.

## Services Used

- Amazon VPC
- EC2
- Security Groups
- Network ACLs
- VPC Gateway Endpoint
- VPC Interface Endpoint
- AWS Systems Manager

## Outcome

A private AWS networking architecture was implemented, enabling secure service access, controlled administration paths, and validation of Security Group and NACL behaviour.

## Key Learning

- Private subnets can access AWS services without internet exposure.
- Gateway Endpoints are ideal for S3 and DynamoDB.
- Interface Endpoints support private API access for services such as SSM.
- Security Groups are stateful, while NACLs are stateless.
