# Question: Can you recover a locked EC2 instance without rebuilding it?

**Answer:** Yes. My preferred order is Session Manager first, then AWS-supported Automation such as AWSSupport-ResetAccess, then EBS root-volume repair if filesystem intervention is needed. For EBS-backed instances, user data can also be updated after stopping the instance, which makes recovery possible in some Linux scenarios.

# Question: Can AWS recover a lost EC2 private key?

**Answer:** No. AWS states that EC2 does not keep a copy of the private key, so the original private key cannot be recovered. The correct approach is to use supported recovery methods to regain access.

# Question: How do you respond if there is also an abuse alert?

**Answer:** I preserve evidence, restrict exposure, use Systems Manager where possible, rotate keys or credentials, and review logs before deciding whether to repair or rebuild. For suspected compromise, I prefer rebuilding from a trusted baseline after preserving evidence.
