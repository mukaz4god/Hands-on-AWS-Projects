
**Architecture Overview**
This setup reflects a security‑mature, production AWS environment where network traffic is not only routed securely but also streamed, monitored, stored, and analyzed.

**Core Components**
- 1 VPC (10.0.0.0/16)
- Public Subnet (10.0.1.0/24)
- Private Subnet (10.0.2.0/24)
- Internet Gateway (public ingress/egress)
- NAT Gateway (private egress only)
- Separate Route Tables

**Observability & Security Pipeline**
- VPC Flow Logs
- CloudWatch Logs (real‑time monitoring)
- Kinesis Data Streams (KDS) (stream processing & fan‑out)
- Kinesis Data Firehose (KDF) (delivery pipeline)
- Amazon S3 (long‑term retention)
- Amazon Athena (SQL‑based investigation)

**Step 1 – Create the VPC**

Action:
- Create a VPC with CIDR 10.0.0.0/16
- Enable DNS resolution and DNS hostnames

Industry Reasoning Custom VPCs are mandatory for enterprises to support logging, compliance, and segmentation.

**Outcome:** To isolated production‑ready network boundary.

**Step 2 – Create Public and Private Subnets**
Public Subnet:
- CIDR: 10.0.1.0/24
- AZ: eu-west-2a
- Auto‑assign public IPv4: Enabled

Private Subnet:
- CIDR: 10.0.2.0/24
- AZ: eu-west-2a
- Auto‑assign public IPv4: Disabled

**Outcome:** Clear separation between internet‑facing and internal workloads.

**Step 3 – Create and Attach Internet Gateway**
Action:
- Create an Internet Gateway
- Attach it to the VPC

**Outcome:** To allow public subnet communicate with the internet.

**Step 4 – Create NAT Gateway**

Action:
- Allocate an Elastic IP
- Deploy NAT Gateway in the public subnet

Why Allows private resources outbound internet access without inbound exposure.

**Outcome:** To secure egress for backend systems.

**Step 5 – Configure Route Tables**

Public Route Table:
- 0.0.0.0/0 → Internet Gateway

Private Route Table
- 0.0.0.0/0 → NAT Gateway

**Outcome:** Correct traffic flow aligned with AWS best practices.

**Step 6 – Enable VPC Flow Logs (Source of Truth)**

VPC Flow Logs act as the raw network telemetry source.

Configuration:

- Resource: VPC
- Traffic type: ALL (ACCEPT + REJECT)
- Log format: Version 2 (default)

**Outcome:** All network traffic is captured for monitoring and investigation.

**Step 7 – Stream Flow Logs to CloudWatch Logs**

Actions
- Create CloudWatch Log Group: vpc-flow-logs
- Create IAM role for VPC Flow Logs
- Send flow logs to CloudWatch

**Why**
- Near real‑time visibility
- SOC alerting & troubleshooting

**Outcome:** Live network monitoring capability.

**Step 8 – Stream Logs Using Kinesis Data Streams (KDS)**

**Purpose of KDS**
KDS enables real‑time streaming and fan‑out to multiple consumers (SIEM, analytics, detection engines).

Actions:
- Create Kinesis Data Stream: vpc-flow-stream
- Shard count: 1 (scale horizontally as needed)
- Configure CloudWatch Logs subscription filter to send logs to KDS

**Industry Use Case**

- This feed security analytics
- Detect anomalies and scanning activity
- Integrate with SIEM or Lambda processors

**Outcome:** Real‑time stream of network traffic events.

**Step 9 – Deliver Logs Using Kinesis Data Firehose (KDF)**

**Purpose of KDF**
KDF provides fully managed, near‑real‑time delivery to storage and analytics services.

Actions:
- Create Firehose delivery stream
- Source: Kinesis Data Streams
- Destination: Amazon S3
- Buffering: 1–5 minutes
- Enable compression (GZIP or Parquet)

**Why**
- No custom code required
- Automatic scaling and retry

**Outcome:** Reliable delivery of logs to long‑term storage.

**Step 10 – Store Flow Logs in S3 (Compliance Layer)**
S3 Configuration
- Bucket example: paywave-vpc-flow-logs

Enable:
- Server‑side encryption (SSE‑S3 or SSE‑KMS)
- Versioning
- Lifecycle policies (archive to Glacier)

**Industry Reasoning**
- Audit evidence
- Regulatory retention
- Cost optimisation

**Outcome**: Durable, compliant log archive.

**Step 11 – Analyze Logs with Athena**

- Create Database
  - ``` CREATE DATABASE vpc_flow_logs;```
- Create Table
``` CREATE EXTERNAL TABLE vpc_flow_logs.flow_logs (
  version int,
  account_id string,
  interface_id string,
  srcaddr string,
  dstaddr string,
  srcport int,
  dstport int,
  protocol int,
  packets bigint,
  bytes bigint,
  start bigint,
  end bigint,
  action string,
  log_status string
)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe'
LOCATION 's3://paywave-vpc-flow-logs/'; ```

- Example Security Query
``` SELECT srcaddr, COUNT(*) AS attempts
FROM vpc_flow_logs.flow_logs
WHERE action = 'REJECT'
GROUP BY srcaddr
ORDER BY attempts DESC; ```

**Outcome:** SQL‑based threat hunting on network traffic.

**Step 12 – Verification**

Public Subnet
- Internet reachable
- Flow logs show ACCEPT via IGW

Private Subnet
- No inbound internet access
- Outbound traffic via NAT
- Rejected attempts visible in logs

**Outcome:** End‑to‑end verification of routing and observability.

## Final Project Outcome

I implemented:
- A production‑grade AWS VPC
- Secure routing and segmentation
- Real‑time streaming of network telemetry
- CloudWatch for monitoring
- Kinesis for streaming & delivery
- S3 for compliance storage
- Athena for investigation

This project mirrors architectures used in FinTech, SaaS, SOC, and government cloud environments.
