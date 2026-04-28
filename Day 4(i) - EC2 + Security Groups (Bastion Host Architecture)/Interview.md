## 3. Interview‑Ready Wording

**Q1: How do you securely access private EC2 instances?**
Answer:
I deploy a Bastion Host in a public subnet and place sensitive instances in private subnets without public IPs. Security Groups restrict SSH so that only administrators can access the Bastion, and only the Bastion can access the private instances. This ensures no direct internet exposure while maintaining operational access.

**Q2: Why not give the private instance a public IP?**
Answer:
Assigning a public IP increases the attack surface. Keeping instances private enforces network isolation and aligns with least‑privilege principles from the AWS Well‑Architected Framework.

**Q3: How do you verify the setup is secure?**
Answer:
I test that direct SSH from the internet to the private instance fails, while SSH via the Bastion succeeds. I also review security group rules and logs to ensure no unintended access paths exist.
