# Day 35 – CloudFront Advanced Security

# Setup Guide – Industrial Standard Step-by-Step Solution

## Architecture Overview

This project uses:

- Amazon S3 private bucket
- Amazon CloudFront distribution
- Origin Access Control
- Geo-restriction
- Signed URLs
- Field-level encryption

Traffic pattern:

```text
User → CloudFront → OAC → Private S3 Bucket
```

---

## LAB 1 – Create Private S3 Origin Bucket

### Step 1 – Create Bucket

1. Go to **AWS Console → S3**
2. Click **Create bucket**
3. Bucket name:

```text
secure-content-origin-bucket
```

4. Keep **Block all public access** enabled
5. Enable default encryption
6. Click **Create bucket**

### Step 2 – Upload Test Content

Upload:

```text
index.html
premium-report.pdf
```

### Outcome

Content is stored in S3, but not publicly accessible.

---

## LAB 2 – Create CloudFront Distribution

### Step 1 – Open CloudFront

1. Search for **CloudFront**
2. Click **Create distribution**

### Step 2 – Configure Origin

Origin domain:

```text
secure-content-origin-bucket.s3.<region>.amazonaws.com
```

Origin type:

```text
Amazon S3
```

### Step 3 – Viewer Settings

Recommended:

- Viewer protocol policy: Redirect HTTP to HTTPS
- Allowed HTTP methods: GET, HEAD
- Cache policy: Managed-CachingOptimized

### Outcome

CloudFront distribution is created to serve S3 content globally.

---

## LAB 3 – Configure Origin Access Control

### Step 1 – Create OAC

During distribution setup or after creation:

1. Go to **Origins**
2. Select the S3 origin
3. Choose **Origin access**
4. Select **Origin Access Control**
5. Create a new OAC

### Step 2 – Update S3 Bucket Policy

CloudFront may provide a bucket policy. Apply it to the S3 bucket.

The policy should allow CloudFront service principal access to the bucket only through your distribution.

### Step 3 – Test

Try accessing the object directly from S3:

```text
https://bucket-name.s3.amazonaws.com/index.html
```

This should fail.

Now access through CloudFront:

```text
https://cloudfront-domain.cloudfront.net/index.html
```

This should work.

### Outcome

The bucket remains private while CloudFront can retrieve content securely.

---

## LAB 4 – Enable Geo-Restriction

### Step 1 – Open Distribution Settings

1. Go to **CloudFront → Distributions**
2. Select your distribution
3. Click **Security** or **Restrictions**

### Step 2 – Configure Geo Restriction

Choose one:

- Allow list
- Block list

Example:

```text
Allow only United Kingdom and Ireland
```

### Step 3 – Save Changes

Wait for CloudFront deployment to complete.

### Outcome

CloudFront enforces country-based content access controls.

---

## LAB 5 – Configure Signed URLs

### Step 1 – Create Key Group

1. Go to **CloudFront → Key management**
2. Create a public key
3. Create a key group
4. Add the public key to the key group

### Step 2 – Attach Key Group to Cache Behaviour

1. Open your distribution
2. Go to **Behaviours**
3. Edit the behaviour for premium content
4. Enable trusted key group
5. Select the key group

### Step 3 – Generate Signed URLs

Your application generates signed URLs using the private key.

Testing logic:

- Valid signed URL should work
- Expired signed URL should fail
- Modified signed URL should fail

### Outcome

Premium content is accessible only through time-limited signed URLs.

---

## LAB 6 – Configure Field-Level Encryption

### Step 1 – Create Public Key

1. Go to **CloudFront**
2. Open **Public keys**
3. Create or upload a public key

### Step 2 – Create Field-Level Encryption Profile

1. Go to **Field-level encryption**
2. Create profile
3. Add field names that require encryption

Example fields:

```text
creditCardNumber
nationalInsuranceNumber
```

### Step 3 – Attach Configuration

Associate the field-level encryption configuration with the relevant cache behaviour.

### Outcome

Sensitive request fields receive an additional encryption layer at the edge.

---

## LAB 7 – Final Validation

Validate:

- Direct S3 access is denied
- CloudFront access works
- Geo-restriction behaves as expected
- Signed URLs enforce access expiry
- Field-level encryption applies to intended fields

### Outcome

CloudFront is configured as a secure global delivery layer for private content.

---

## Final Project Outcome

You implemented:

- CloudFront distribution with S3 origin
- Origin Access Control
- Private S3 content delivery
- Geo-restriction
- Signed URLs
- Field-level encryption

This is a production-grade secure content delivery pattern.
