# CloudFront Advanced Security

## Case Study – Secure Global Content Delivery

### Business Scenario

A media company stores premium downloadable content in Amazon S3. Customers around the world need fast access, but the content must not be publicly accessible directly from S3.

The company also has licensing restrictions that require some content to be available only in specific countries. Premium files must be protected using signed URLs, and sensitive form fields must receive extra protection where applicable.

### Security Requirements

- S3 bucket must remain private.
- CloudFront must serve content globally.
- Origin Access Control must secure S3 origin access.
- Geo-restrictions must control country-level access.
- Signed URLs must protect premium content.
- Field-level encryption should protect sensitive request fields.

### Your Role

You are the Edge Security / Cloud Security Engineer responsible for implementing secure global content delivery using CloudFront and S3.

### Project Goal

Build a secure CloudFront distribution with a private S3 origin and advanced access controls.
