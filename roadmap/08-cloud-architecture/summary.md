# Module 08: Cloud Architecture & Integration

## Why This Module

Diego has OCI Foundations certification and works with hybrid cloud at Oracle. This module broadens that to multi-cloud architecture (AWS primary) and connects all previous modules into production-grade systems. This is the capstone — designing complete infrastructure, not just using individual tools.

## Key Concepts

### Cloud Architecture Principles

- Well-Architected Framework (5 pillars):
  1. Operational Excellence (automation, observability)
  2. Security (least privilege, encryption, compliance)
  3. Reliability (fault tolerance, disaster recovery)
  4. Performance Efficiency (right-sizing, scaling)
  5. Cost Optimization (reserved instances, spot, right-sizing)

### AWS Core Services (with OCI parallels)

| AWS | OCI Equivalent (Diego knows) | Purpose |
|-----|-----|-----|
| VPC | VCN | Network isolation |
| EC2 | Compute Instances | Virtual machines |
| S3 | Object Storage | Object storage |
| RDS | DB Systems | Managed databases |
| EKS | OKE | Managed Kubernetes |
| IAM | IAM | Identity and access |
| CloudWatch | Monitoring | Observability |
| Route53 | DNS | DNS management |
| ALB/NLB | Load Balancer | Traffic distribution |

### Infrastructure Patterns

- **Three-tier architecture**: Web → App → Data
- **Microservices on Kubernetes**: Service mesh, API gateway
- **Serverless patterns**: Lambda, API Gateway, DynamoDB
- **Event-driven architecture**: SQS, SNS, EventBridge
- **Multi-region deployment**: Active-active, active-passive

### Security Architecture

- IAM design (roles, policies, least privilege)
- Network security (VPC design, NACLs, security groups)
- Encryption (at rest, in transit, KMS)
- Secrets management (AWS Secrets Manager, HashiCorp Vault)
- Compliance and audit (CloudTrail, Config)

### Cost Management

- Reserved vs On-Demand vs Spot instances
- Auto-scaling policies
- Cost allocation tags
- Budget alerts
- Right-sizing tools
- Infracost in CI pipelines

### Disaster Recovery

- RPO (Recovery Point Objective) and RTO (Recovery Time Objective)
- Backup strategies (snapshots, cross-region replication)
- DR patterns (pilot light, warm standby, multi-site active-active)
- Chaos engineering (Game Days)

## Topics

1. AWS core services (VPC, EC2, S3, RDS, IAM)
2. Infrastructure design patterns
3. Security architecture (IAM, encryption, network)
4. High availability and fault tolerance
5. Auto-scaling and performance
6. Cost optimization strategies
7. Disaster recovery and backups
8. Multi-cloud considerations (AWS + OCI)
9. Complete project: Design and deploy a production system
10. Architecture review and documentation
