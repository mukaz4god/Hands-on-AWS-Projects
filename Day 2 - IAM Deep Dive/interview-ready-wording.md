**“I built a real AWS environment where I demonstrated the security impact of over-permissive IAM roles on EC2, then remediated it using least-privilege policies and validated the fix with controlled testing OR “I built an AWS IAM security case study where I demonstrated how over-permissive EC2 IAM roles can lead to unintended S3 access, then remediated the issue using least-privilege policies and validated the fix through hands-on testing.”**



**Note: That sentence alone is interview gold.**

## STAR Method Answer

**Situation:**
EC2 instances were granted broad S3 access for convenience.

**Task:**
Identify risk and enforce least privilege without breaking functionality.

**Action:**
Tested the permissions, demonstrated unauthorized access, redesigned IAM policies, and revalidated access.

**Result:**
Reduced blast radius, blocked unauthorized access, and aligned permissions with business needs.
