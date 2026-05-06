# Module 08: Cloud Architecture — Hands-On Exercises

## Module Repository: `cloud-architecture-capstone`

All deliverables for this module live in `repos/cloud-architecture-capstone/` and on GitHub at `github.com/<username>/cloud-architecture-capstone`. Create it with `/setup-repo` before starting Exercise 8.1.

This is the **capstone project** — the most important repo in the portfolio. It integrates everything from Modules 02-07 into a production-grade system: VPC design, HA application deployment, security hardening, CI/CD, and observability. The README must be polished to recruiter-grade quality with architecture diagrams, ADRs, cost analysis, and runbooks.

Replace earlier paths like `devops-lab/terraform/production-vpc/` with in-repo equivalents.

---

## Exercise 8.1: Production VPC Design

**Objective**: Design and deploy a production-grade VPC with Terraform.

**Steps**:
1. Create `devops-lab/terraform/production-vpc/`
2. Design a VPC with:
   - 3 Availability Zones
   - Public subnets (load balancers, bastion)
   - Private subnets (application tier)
   - Isolated subnets (databases, no internet)
   - NAT Gateway for private subnet internet access
   - VPC Flow Logs enabled
3. Implement as a Terraform module with configurable CIDR blocks
4. Add security groups for each tier
5. Deploy and verify routing tables
6. Document the architecture with a diagram (draw.io or ASCII)

**Validation**: VPC deployed, routing correct, tiers isolated, flow logs capturing, documented

---

## Exercise 8.2: Highly Available Application Deployment

**Objective**: Deploy a fault-tolerant application across multiple AZs.

**Steps**:
1. Using Terraform, deploy:
   - Application Load Balancer (public subnets)
   - Auto Scaling Group with launch template (private subnets)
   - RDS Multi-AZ instance (isolated subnets)
   - ElastiCache Redis for session management
2. Configure health checks at ALB and ASG level
3. Configure auto-scaling policies (CPU-based, request-count-based)
4. Test fault tolerance: terminate an instance, verify traffic shifts
5. Test scaling: generate load, observe scale-out
6. Configure with Ansible post-provisioning (application deployment)

**Validation**: Application survives instance failure, scales under load, multi-AZ operational

---

## Exercise 8.3: Security Hardening

**Objective**: Implement security best practices across the infrastructure.

**Steps**:
1. IAM: Create roles with least-privilege policies (no `*` permissions)
2. Network: Implement NACLs as additional defense layer
3. Encryption: Enable encryption at rest (EBS, RDS, S3) and in transit (TLS)
4. Secrets: Move all credentials to AWS Secrets Manager, reference from Terraform
5. Audit: Enable CloudTrail, AWS Config rules
6. Scanning: Run ScoutSuite or Prowler against the account
7. Fix all critical and high findings
8. Document the security posture

**Validation**: No critical security findings, encryption everywhere, least-privilege IAM, audit trail active

---

## Exercise 8.4: CI/CD for the Complete Stack

**Objective**: Build the full deployment pipeline integrating all modules.

**Context**: This is the ultimate capstone — everything comes together.

**Steps**:
1. GitHub Actions workflow that:
   - On PR: Terraform plan, Ansible lint, Docker build+scan, cost estimate
   - On merge: Terraform apply → Build & push Docker image → Deploy to EKS via Helm → Run Ansible for non-K8s config → Health check verification
2. Implement rollback strategy: if deployment fails, revert to previous version
3. Add Slack/email notifications for deployment status
4. Create separate workflows for infrastructure vs application changes
5. Implement environment promotion: dev → staging → production with approvals

**Validation**: Complete pipeline from code commit to production deployment, rollback works, visibility at every stage

---

## Exercise 8.5: Monitoring the Complete System

**Objective**: Implement full observability for the production deployment.

**Steps**:
1. Deploy Prometheus + Grafana on the EKS cluster (from Module 07)
2. Create dashboards for:
   - Infrastructure (nodes, pods, network)
   - Application (RED metrics)
   - Business (request counts, user actions)
3. Define SLOs: 99.9% availability, p99 latency < 500ms
4. Configure alerts based on error budget burn rate
5. Create a runbook document for each alert
6. Simulate an incident and practice the response workflow

**Validation**: Complete observability stack, SLOs defined, alerts tested, runbook documented

---

## Exercise 8.6: Architecture Documentation and Review

**Objective**: Document the complete system for handoff and review.

**Steps**:
1. Create architecture decision records (ADRs) for key decisions
2. Draw complete architecture diagram (use draw.io, Mermaid, or similar)
3. Document:
   - System overview and components
   - Deployment process
   - Disaster recovery procedure
   - Cost breakdown and optimization opportunities
   - Security controls
4. Conduct a self-review using the AWS Well-Architected Framework questions
5. Write a post-mortem template for future incidents
6. Identify areas for improvement (next iteration)

**Validation**: Complete documentation package that a new team member could use to understand and operate the system
