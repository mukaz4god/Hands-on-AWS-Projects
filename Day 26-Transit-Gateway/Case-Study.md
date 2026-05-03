# Transit Gateway

## Case Study – Enterprise Multi-VPC Networking Architecture

### Business Scenario

A company has multiple AWS environments:

- Shared services VPC
- Development VPC
- Production VPC

Initially, teams used VPC peering for connectivity, but as the number of VPCs increased, managing one-to-one peering connections became complex and difficult to scale.

The network team wants a centralized hub-and-spoke architecture using AWS Transit Gateway.

### Business Requirements

- Connect multiple VPCs using a centralized routing hub.
- Avoid complex VPC peering mesh architecture.
- Use non-overlapping CIDR blocks.
- Control cross-VPC communication through route tables.
- Validate private connectivity between VPCs.

### Your Role

You are the Cloud Network Engineer responsible for implementing an enterprise multi-VPC network using AWS Transit Gateway.

### Project Goal

Design and deploy a scalable multi-VPC architecture using Transit Gateway for centralized routing and cross-VPC communication.
