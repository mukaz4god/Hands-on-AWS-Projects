**1️⃣ Create a Separate AWS Account (Free Tier)**

1. Go to: https://aws.amazon.com/
2. Click Create an AWS Account

3. Use:
      * A new email (not personal work email)
      * Strong password (password manager recommended)
4. Select Personal Account (unless you have a registered company)
5. Enter payment details (required for Free Tier)
6. Complete phone verification

**2️⃣ Secure the Root Account (CRITICAL)**
Why? => Root has unlimited power. It should never be used for daily work.

**Steps**

1. Log in as Root user
2. Go to IAM → Security Credentials
3. Enable MFA on root:
    * Choose Virtual MFA
    * Use Google Authenticator / Authy
4. Store:
    * Root email
    * MFA recovery codes
    * Password securely

🚫 Rule: Root account is now locked away, and the root account is now protected against compromise.


**3️⃣ Create an IAM Admin User (No Root Usage)**

**Steps**
1. Go to IAM → Users → Create User
2. Username: admin-user
3. Select:
      * AWS Management Console access
4. Attach policy:
    * AdministratorAccess
5. Create user (**admin-user** in my case and this can be any name you prefer)
6. Log out from root
7. Log in as admin-user
8. Enable MFA for this user as well

**Note:** All future AWS actions happen via IAM, not root. You can also enable a console login for the admin user if console access is needed.

**4️⃣ Set AWS Budgets & Billing Alerts (VERY IMPORTANT)**
Why? => Misconfigured resources can cost £££ overnight.

**Steps**

1. Go to Billing → Budgets
2. Create budget:
    * Type: Cost Budget
    * Monthly limit: $5 (Free Tier safety)
3. Add alerts (fixed or set threshold if need be):
    * 50% threshold → email (your email address to get the alert)
    * 80% threshold → email (your email address to get the alert)
    * 100% threshold → email (your email address to get the alert)
4. Verify billing alerts are enabled in Billing Preferences


**5️⃣ Enable AWS CloudTrail (All Regions)**
Why?: CloudTrail is your security black box for 
* Who did what?
* When? and
* From where?

**Steps**

1. Go to CloudTrail
2. Create trail
3. Settings:
   * Apply to All Regions
   * Enable Management Events
   * Read + Write
4. Create new S3 bucket for logs
5. Enable log file validation

The steps allow full audit trail for investigations & compliance.

**6️⃣ Enable IAM Access Analyzer**
Why? To Detects publicly exposed resources and Over-permissive IAM policies.

**Steps**

1. Go to IAM → Access Analyzer
2. Create analyzer
3. Scope: Account

This allows proactive detection of risky access configurations.
