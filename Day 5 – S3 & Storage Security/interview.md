## Interview Ready Wording

**Question: How do you secure data stored in Amazon S3?** <br/>
**Answer:** I implement multiple security controls including blocking public access, enabling server-side encryption using SSE-S3 or SSE-KMS, applying bucket policies to enforce least-privilege access, enabling versioning to protect against accidental deletion, and enabling access logging for auditing and monitoring.

**Question: What is the difference between SSE-S3 and SSE-KMS?** <br/>
**Answer:** SSE-S3 uses AWS-managed encryption keys automatically handled by Amazon S3. SSE-KMS uses AWS Key Management Service which provides greater control over encryption keys, including key rotation, access policies, and auditing through CloudTrail.

**Question: Why enable versioning in S3?** <br/>
**Answer:** Versioning protects against accidental data deletion or overwriting by maintaining multiple versions of an object. It is especially important in production systems where data integrity and recovery are critical.
