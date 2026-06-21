# Amazon Web Services (AWS) Overview

## Definition
AWS is the world’s most comprehensive and broadly adopted cloud platform, offering over 200 fully featured services from data centers globally.

## Why it exists
Before cloud computing, companies had to buy physical servers (CapEx), wait months for them to be delivered, rack them, and guess how much power they needed. AWS shifted this to OpEx—renting compute power by the millisecond with infinite scalability. You can spin up 1,000 servers for Black Friday and turn them off on Saturday, only paying for what you use.

## Commands (AWS CLI)
- `aws configure`: Set up your Access Key, Secret Key, and Default Region.
- `aws s3 ls`: List all S3 buckets.
- `aws s3 cp file.txt s3://my-bucket/`: Upload a file to S3.
- `aws ec2 describe-instances`: List your running virtual machines.

## Architecture
- **Regions & AZs**: A Region is a physical location (e.g., `us-east-1` in Virginia). Inside a Region are Availability Zones (AZs), which are distinct, separate data centers with redundant power and networking.
- **VPC (Virtual Private Cloud)**: Your logically isolated slice of the AWS network. This is where you define public subnets (internet-facing) and private subnets (databases).
- **IAM (Identity and Access Management)**: The security perimeter. Users, Roles, and Policies dictating exactly who can access what.

## Interview Questions
**Q: "What is the difference between EC2, ECS/EKS, and Lambda?"**
*Answer*: They are three tiers of compute. 
1. **EC2 (IaaS)**: A raw virtual machine. You manage the OS, patching, and scaling. Maximum control, maximum overhead.
2. **ECS/EKS (Containers)**: You give AWS a Docker container. AWS handles running it across a cluster. Less overhead, highly scalable.
3. **Lambda (Serverless)**: You just write a function (Python/Node). AWS executes it when triggered and scales it instantly. You pay only for the exact milliseconds it runs. Zero OS overhead.

**Q: "You created an S3 bucket and uploaded a PDF, but the public URL says 'Access Denied'. Why?"**
*Answer*: By default, S3 buckets block all public access for security. To make the PDF public, I must disable "Block Public Access" at the bucket level and attach a Bucket Policy granting `s3:GetObject` permissions to `*` (everyone), or explicitly make the object public via ACLs.

## Cheat Sheet (Core Services)
| Service | Purpose | Analogy |
| :--- | :--- | :--- |
| **EC2** | Virtual Machines | A rented computer |
| **S3** | Object Storage | An infinitely large hard drive for files |
| **RDS** | Relational Database | Managed SQL (Postgres/MySQL) |
| **Lambda** | Serverless Compute | Code that runs only when triggered |
| **SQS** | Message Queue | A buffer to hold messages between microservices |
| **SNS** | Pub/Sub Notifications | Sending alerts (Email/SMS) or fanning out data |
| **CloudWatch**| Monitoring & Logging | The dashboard for logs and metrics |
