# Question: Why use Systems Manager instead of SSH for EC2 management?<br/>
**Answer:** I use Systems Manager to reduce administrative exposure and centralize operations. It gives me fleet-wide inventory, patching, configuration enforcement, and run-command capability without requiring SSH as the primary management channel. It also improves auditability because actions are orchestrated through managed AWS services and runbooks.

# Question: What is the difference between Patch Manager and State Manager?<br/>

**Answer:** Patch Manager automates operating system and software patching for managed nodes, while State Manager enforces a desired operational state on managed nodes and other supported resources.

# Question: What are Systems Manager documents?

**Answer:** Systems Manager documents define the actions that Systems Manager performs. I use Amazon-owned documents for standard operations and custom documents for organization-specific procedures.
