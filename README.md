# CLOUD IDENTITY COMPROMISE INVESTIGATION

**Project Summary:**

Conducted a cloud-native forensic investigation into a simulated identity compromise involving leaked long-term AWS programmatic access keys (AKIA...). Using a dedicated compromised IAM identity (compromised-dev) with restricted read-only permissions, a threat actor executed unauthorized management-plane reconnaissance (ListBuckets) and attempted resource abuse by spinning up high-powered compute instances (RunInstances) via AWS CloudShell. To analyze the incident, multi-region AWS CloudTrail telemetry was ingested into an encrypted Amazon S3 evidence bucket (forensic-trail-bucket-718). Amazon Athena was deployed with native CloudTrailSerde schemas to flatten and parse gzipped JSON logs, allowing investigators to reconstruct a precise chronological timeline and verify that the compute provisioning attempt failed gracefully due to an invalid AMI ID.   

**Learning Points:**

1. **Cloud Control Plane Telemetry & Logging:** Mastered the architecture of AWS CloudTrail audit logs, configuring immutable multi-region management-plane event capture to track external API calls, user identities, and source IP addresses.
2. **Serverless Log Parsing with Amazon Athena:** Utilized Amazon Athena and Hive DDL to construct external tables mapping to nested, gzipped JSON files in S3, employing the native CloudTrailSerde parser to perform SQL-based forensic queries.
3. **IAM Identity Compromise & API Forensics:** Simulated and investigated a realistic credential leak scenario, tracing malicious activity from initial storage enumeration (ListBuckets) to unauthorized infrastructure abuse (RunInstances).
4. **Error Analysis & Impact Verification:** Analyzed Athena errorMessage fields to validate threat actor failures (e.g., InvalidAMIID.NotFound), proving that malicious compute requests were rejected and required no manual resource teardown.
5. **PICERL Incident Response Framework in Cloud:** Executed a structured cloud forensic lifecycle, moving from preparation (S3/CloudTrail setup) and identification (Athena SQL analysis) to containment (credential invalidation) and lessons learned.
6. **Cloud Security Hardening & Best Practices:** Identified critical architectural improvements, emphasizing the transition from long-term programmatic access keys to short-term dynamic credentials via AWS STS, and establishing automated containment pipelines with GuardDuty and EventBridge.  
