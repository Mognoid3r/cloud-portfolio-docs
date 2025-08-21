# AWS Cloud Stack (Documentation-Only)

**What this is:** A high-level, sanitized overview of a personal AWS implementation.  
**What this is NOT:** No code, no identifiers, no secrets, and no proprietary business details.

## Architecture (sanitized)
CloudFront (edge, TLS via ACM) → S3 origins and Elastic Beanstalk app  
IAM (users/roles/policies for least privilege), Lambda (event-driven tasks), CodePipeline (GitHub → Beanstalk)

```mermaid
graph LR
  A[Users] -->|HTTPS (ACM)|CF[CloudFront]
  CF -->|Origin|S3A[S3 - Static Assets]
  CF -->|Origin|EB[Elastic Beanstalk - App]
  subgraph AWS_Account
    IAM[IAM: users/roles/policies]
    L[Lambda: automation/tasks]
    CP[CodePipeline: GitHub to Build/Deploy]
    LOGS[S3 - Access Logs]
  end
  CF --> LOGS
