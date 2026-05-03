# Day 34 – Transit Gateway

## Project Goal

To design and implement an enterprise multi-VPC network using Transit Gateway for centralized routing and scalable cross-VPC communication.

## Services Used

- Amazon VPC
- AWS Transit Gateway
- EC2
- Route Tables
- Security Groups
- Network ACLs

## Outcome

A hub-and-spoke multi-VPC architecture was deployed, enabling scalable cross-VPC connectivity and centralized route management through Transit Gateway.

## Key Learning

- Transit Gateway scales better than VPC peering for many VPCs.
- VPC CIDRs must not overlap.
- Route tables must be updated on both VPC and TGW sides.
- Security Groups and NACLs still control actual traffic flow.
