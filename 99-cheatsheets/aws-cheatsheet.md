# AWS Cheat Sheet

### Core Concepts
- **CapEx vs OpEx**: Shift from buying physical servers (CapEx) to renting compute by the millisecond (OpEx).
- **Region**: Geographic location (e.g., us-east-1).
- **Availability Zone (AZ)**: Redundant, physically separate data centers within a Region.
- **VPC**: Virtual Private Cloud. Your isolated networking perimeter.

### Core Services
| Category | Service | Purpose / Analogy |
| :--- | :--- | :--- |
| **Compute** | **EC2** | Raw Virtual Machines (IaaS). High management overhead. |
| **Compute** | **ECS / EKS**| Managed Docker container orchestration. |
| **Compute** | **Lambda** | Serverless. Run code without provisioning OS. Pay per millisecond. |
| **Storage** | **S3** | Object storage. Infinite hard drive for flat files/backups. |
| **Database**| **RDS** | Managed Relational SQL Database (Postgres, MySQL). |
| **Database**| **DynamoDB**| Managed NoSQL Key-Value database. Single-digit ms latency. |
| **Messaging**| **SQS** | Queue. Decouples microservices (Buffer for burst traffic). |
| **Messaging**| **SNS** | Pub/Sub. Push notifications, fan-out architecture. |
| **Security**| **IAM** | Identity and Access Management. Users, Roles, Policies. |

### CLI Commands
| Command | Action |
| :--- | :--- |
| `aws configure` | Set up Access Key, Secret Key, and Region. |
| `aws s3 ls` | List all S3 buckets. |
| `aws s3 cp file.txt s3://bucket/`| Upload a file to S3. |
| `aws ec2 describe-instances` | Get JSON data about running EC2 VMs. |

### Interview Triggers
- 🚨 **"S3 Access Denied"** ➡️ Trigger: S3 blocks public access by default. Fix by disabling "Block Public Access" and attaching a Bucket Policy granting `s3:GetObject` to `*`.
- 🚨 **"EC2 vs Lambda"** ➡️ Trigger: EC2 = Always on, you patch the OS, pay per hour. Lambda = Event-driven, AWS patches the OS, pay per 100ms execute time.
