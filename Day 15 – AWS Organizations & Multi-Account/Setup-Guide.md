# Industrial Setup Standard – Step-by-Step Solution

**LAB 1 – Create AWS Organization**<br/>
1. AWS Console → AWS Organizations
2. Click Create organization
- Select: ```Enable all features```

**Outcome**<br/>
Organisation created with full governance capability

**LAB 2 – Create Multiple Accounts**<br/>
1. Organizations → Accounts → Add account
2. Choose: ```Create account```

Create:
- dev-account
- prod-account

**Outcome**<br/>
Accounts isolated by environment

**LAB 3 – Create Organizational Units (OUs)**<br/>
1. Go to Organize accounts
2. Create OUs:
 - Development
 - Production
3. Move accounts into respective OUs

**Outcome**<br/>
Logical grouping for governance

**LAB 4 – Apply Service Control Policies (SCPs)**<br/>
1. Go to Policies → Service Control Policies
2. Create policy:

Example (deny EC2 termination):
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "ec2:TerminateInstances",
      "Resource": "*"
    }
  ]
}
```
3. Attach to OU

**Outcome**<br/>
Centralized restriction enforced

**LAB 5 – Enable Consolidated Billing**<br/>
1. Organizations → Billing
2. Confirm: ```Consolidated billing enabled```

**Outcome**<br/>
Single bill across accounts

**Final Project Outcome**<br/>
- Multi-account architecture implemented
- Central governance via SCPs
- Cost visibility via consolidated billing
