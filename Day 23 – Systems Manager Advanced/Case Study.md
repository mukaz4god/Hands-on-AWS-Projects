## Case Study – Centralised Fleet Operations Without SSH

**Business Scenario**

KFJ Solutions is a financial services company that runs Linux and Windows EC2 instances across multiple environments. The security team has mandated that day-to-day administration no longer rely on direct SSH access, as it increases the attack surface and makes access harder to audit. The operations team needs centralised visibility into installed software, automated patching, baseline enforcement, and repeatable operational runbooks. This aligns with the AWS Well-Architected Operational Excellence and Security pillars, which emphasise operational standards, event response, and secure administration.

**Task**

You are the Cloud / Platform Engineer responsible for implementing:

- SSM Inventory
- Patch Manager
- State Manager
- Automation documents
- Run Command across multiple instances

**Project Goal**

Build a centralised EC2 management model using Systems Manager so that instances can be inventoried, patched, configured, and operated at scale without relying on SSH as the primary management path. AWS Systems Manager documents define the actions it performs, and it includes Amazon-owned preconfigured documents you can use directly.
