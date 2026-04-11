# Industrial Setup Standard – Step-by-Step Solution

**Recovery Decision Standard**

Use this order of operations in production:

1. Prefer Session Manager if the instance is managed
2. Use supported Automation for lost key/password issues
3. Use user data updates only for suitable Linux recovery cases on EBS-backed instances
4. Use root EBS volume attach/swap when filesystem-level intervention is required
5. Preserve snapshots and logs before invasive recovery steps

EC2 user data can be updated after stopping an EBS-backed instance, and an EBS root volume can be attached to another instance for debugging or repair.

**Scenario A – Recover Linux Access with Session Manager**

1. Go to AWS Console → Systems Manager → Session Manager
2. Start a session to the affected instance if it appears as managed
3. Validate:
  - SSH daemon status
  - Authorised keys file
  - Security group and NACL rules
4. Repair access from inside the instance if needed
5. Document changes and close the incident

**Outcome**<br/>
Fastest and safest recovery path with no need to expose port 22.

**Scenario B – Lost SSH Key Recovery Using User Data**

AWS states that if the root volume is EBS-backed, you can stop the instance and update user data.

1. Go to EC2 → Instances
2. Select the Linux instance
3. Stop the instance
4. Choose Actions → Instance settings / Edit user data
5. Add a recovery script that injects a new public key into the target user’s authorized_keys
6. Save user data
7. Start the instance
8. Attempt SSH with the new key pair
9. Remove the recovery user data after successful access

**Best Practice**<br/>
Take an EBS snapshot before editing recovery settings.

**Outcome**br/>
You restore Linux access without rebuilding the instance.

**Scenario C – Recover Access Using AWSSupport-ResetAccess**

AWS provides the AWSSupport-ResetAccess Automation runbook for lost Linux SSH key access and Windows password/key-related recovery.

1. Go to Systems Manager → Automation
2. Click Execute automation
3. Search for AWSSupport-ResetAccess
4. Provide the affected instance ID
5. Review required parameters
6. Execute the runbook
7. Follow the outputs to connect to the recovered or replacement instance

**Outcome**<br/>
Supported AWS runbook used for a controlled, auditable recovery.

**Scenario D – Recover Using EBS Volume Swap / Attach**<br/>

AWS documents that an EBS root volume can be attached to another running instance for debugging or repair.

1. Stop the affected instance
2. Go to EC2 → Volumes
3. Locate the root EBS volume
4. Detach it from the affected instance
5. Attach it to a helper instance in the same Availability Zone
6. SSH or SSM into the helper instance
7. Mount the attached volume
8. Repair:
  - authorized_keys
  - sshd_config
  - file permissions
  - misconfigurations preventing login
9. Unmount the volume
10. Detach from the helper instance
11. Reattach to the original instance as the root volume
12. Start the original instance and test access

**Outcome**<br/>
Deep recovery for filesystem-level lockouts or configuration damage.

**Scenario E – Windows Password Recovery**

AWS documents that AWSSupport-ResetAccess can generate a new Windows Administrator password that you decrypt with the current EC2 key pair.

1. Go to Systems Manager → Automation
2. Execute AWSSupport-ResetAccess
3. Follow the documented outputs
4. Recover or reset Windows access
5. Test RDP or Session Manager access after recovery

**Outcome**<br/>
Windows administrative access was recovered through an AWS-supported workflow.

**Scenario F – EC2 Instance Connect Access**

EC2 Instance Connect is useful for short-lived, just-in-time SSH access on supported Linux distributions, but it depends on proper instance-side support and network access. AWS troubleshooting notes mention host key handling for EC2 Instance Connect on supported distributions.

1. Go to EC2 → Instances
2. Select a supported Linux instance
3. Click Connect
4. Choose EC2 Instance Connect
5. Test browser-based or CLI-based ephemeral key access

**Outcome**<br/>
Just-in-time SSH access validated for supported environments.

## Abuse Handling Standard

When an abuse alert or suspicious access event occurs:

1. Preserve evidence first:
  - Snapshot affected volumes
  - Retain CloudTrail, VPC Flow Logs, and Systems Manager outputs
2. Remove broad inbound exposure:
  - Restrict security groups
  - Disable unneeded public access
3. Prefer Session Manager for safe administrative access
4. Rotate credentials and keys
5. Review recent changes and CloudTrail events
6. Rebuild if a compromise is suspected rather than trusting a repaired host

**Outcome**<br/>
You recover access while maintaining forensic discipline and minimising further risk.

# Final Project Outcome

I have implemented:

- Linux recovery via Session Manager
- Lost key recovery using user data or AWS Automation
- EBS attach/swap recovery workflow
- Windows password recovery path
- EC2 Instance Connect testing
- Incident-oriented access recovery and abuse handling process
