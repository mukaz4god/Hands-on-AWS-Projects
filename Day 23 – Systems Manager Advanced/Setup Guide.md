## Industrial Setup Standard – Step-by-Step Solution

**Architecture Overview**

This project assumes you already have EC2 instances running in your VPC. For best practice, use instances with the SSM Agent installed, attach an IAM instance profile with Systems Manager permissions, and ensure connectivity either through NAT or Systems Manager interface endpoints. State Manager associations can schedule automations and enforce desired states over time.

**Step 1 – Prepare Managed Instances**

1. Go to AWS Console → EC2 → Instances
2. Select the instances you want to manage
3. Confirm they have an IAM role attached with Systems Manager permissions, typically the managed policy used for managed instances
4. Go to AWS Console → Systems Manager → Fleet Manager / Managed nodes
5. Verify the instances appear as managed

**Outcome**<br/>
You now have EC2 instances enrolled on Systems Manager and ready for centralised administration.

**Step 2 – Configure SSM Inventory**

AWS Systems Manager Inventory collects metadata from managed nodes and can store it centrally, including in Amazon S3 for later query and reporting.

1. Go to Systems Manager → Node Tools → Inventory
2. Click Set up inventory
3. Choose the target instances:
  - By instance IDs, or
  - By tags such as Environment=Dev or PatchGroup=Linux-Prod
4. Choose collection schedule, such as every 30 minutes or hourly
5. Enable common inventory types such as:
  - Applications
  - AWS Components
  - Network configuration
  - Instance detailed information
  - Save the configuration
6. Verification
  - Return to Inventory
  - Review installed software, agent details, and network metadata for each node

**Outcome**<br/>
You gain fleet-wide visibility into software and system state without manually logging into each server.

**Step 3 – Configure Patch Manager**

Patch Manager automates the process of patching managed nodes with both security and other updates. It supports recurring patching using patch policies across accounts and Regions.

1. Go to Systems Manager → Node Tools → Patch Manager
2. Choose Patch policies or Quick setup / Patching setup, depending on console view
3. Create a patch policy for a test group first
4. Target instances using tags, for example:
  - PatchGroup=Linux-Prod
  - PatchGroup=Windows-Prod
5. Define:
  - Scan schedule
  - Install schedule
  - Reboot option
  - Patch baseline selection
6. Save the policy

**Best-Practice Notes**<br/>
  - Start with a non-production patch group
  - Separate Linux and Windows into different patch groups
  - Schedule patching inside approved maintenance windows
  - Notify operations through EventBridge or SNS if your environment requires it

**Test**<br/>
  - Run a Scan first
  - Review compliance status
  - Then run Install
  - Confirm patch compliance improves after the job completes

**Outcome**<br/>

Your EC2 fleet can be patched centrally and on schedule instead of relying on manual SSH sessions.

**Step 4 – Configure State Manager**

State Manager keeps managed nodes in a state that you define.

1. Go to Systems Manager → Node Management → State Manager
2. Click Create association
3. Choose an Amazon-owned document such as:
  - AWS-RunShellScript for Linux
  - AWS-RunPowerShellScript for Windows
  - Or another Amazon-owned operational document
4. Define the command or configuration you want enforced, for example:
  - Ensure CloudWatch agent is installed
  - Ensure a package is present
  - Ensure a configuration file or service state is maintained
5. Select targets by tag
6. Set the schedule to run periodically
7. Create the association

**Example Scenario**<br/>
Use State Manager to ensure the CloudWatch agent is installed on all web servers and starts automatically after reboots.

**Outcome**<br/>
Configuration drift is reduced because Systems Manager keeps instances aligned with your baseline.

**Step 5 – Use Automation Documents**

Systems Manager Automation runbooks can perform operational tasks, approvals, and large-scale remediation, and can also be scheduled by State Manager.

1. Go to Systems Manager → Change Management / Automation
2. Click Execute automation
3. Review Amazon-owned runbooks
4. Select a suitable runbook for a maintenance or recovery task
5. Provide input parameters
6. Execute against a test instance or tagged fleet

Recommended Use Cases
  - Restart services
  - Collect troubleshooting data
  - Recover access
  - Apply operational fixes in a controlled, auditable way

**Outcome**<br/>
You now have repeatable, auditable operational runbooks instead of ad hoc server administration.

**Step 6 – Run Commands Across Multiple Instances**

1. Go to Systems Manager → Node Management → Run Command
2. Click the Run command
3. Select:
  - AWS-RunShellScript for Linux, or
  - AWS-RunPowerShellScript for Windows
4. Enter a test command such as:
  - uname -a
  - df -h
  - Get-Service
5. Target multiple instances by tag
6. Run the command
7. Review per-instance output

**Test**<br/>
Run one command on all application servers and verify results return in the console.

**Outcome**<br/>
You can execute operational commands fleet-wide without opening SSH.

**Final Project Outcome**

I have implemented:<br/>
  - SSM Inventory for asset visibility
  - Patch Manager for scheduled patching
  - State Manager for baseline enforcement
  - Automation runbooks for repeatable operations
  - Run Command for fleet-wide administration

This is the operational model mature AWS environments use to reduce manual access and improve auditability.
