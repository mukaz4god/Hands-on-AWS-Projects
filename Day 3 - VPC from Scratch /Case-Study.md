## Case Study – Secure Cloud Network for a FinTech Startup

**Business Scenario**

A UK-based FinTech startup, PayWave, is migrating its on-premise application to AWS. The application consists of:
- A public-facing web application (frontend)
- A private backend service (API & database)

Due to regulatory and security requirements:
- Backend systems must not be directly accessible from the internet
- Only the frontend should be publicly reachable
- Private resources must still access the internet for updates and patching

**Security & Architecture Requirements**
- Network isolation using a custom VPC
- Separation of public and private subnets
- Controlled internet access using Internet Gateway & NAT Gateway
- Clear routing rules following AWS best practices

**Your Role**
You are acting as a Cloud / DevOps Engineer, responsible for designing and implementing a secure, production-ready VPC from scratch.
