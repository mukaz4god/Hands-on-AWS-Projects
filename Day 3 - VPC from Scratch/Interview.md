## I built a VPC from scratch and implemented a full network observability pipeline using VPC Flow Logs, CloudWatch, Kinesis Data Streams, Firehose, S3, and Athena to support real-time monitoring and post-incident investigation.

**Question: Have you designed a VPC from scratch?**
 - Answer: Yes. I designed and implemented a custom AWS VPC for a scenario-based FinTech migration project. I created public and private subnets, configured Internet and NAT Gateways, and implemented separate route tables to enforce secure traffic flow. Public-facing resources had direct internet access, while private backend systems used a NAT Gateway for outbound-only connectivity. I verified the setup by testing access patterns from both subnets.


**Question: Why use a NAT Gateway instead of making everything public?**
- Answer: Making backend systems public increases the attack surface. A NAT Gateway allows private resources to access external services for updates while remaining inaccessible from the internet, which aligns with AWS security best practices.

**Question: How do you verify public vs private subnet behavior?**
- Answer: I verify by launching EC2 instances in both subnets. Public subnet instances receive a public IP and are reachable externally, while private subnet instances have no public IP and rely on a NAT Gateway for outbound internet access only.
