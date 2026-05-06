# DevOps Roadmap for Diego Chavarria Rodriguez

## Objective

Transform strong Linux administration and enterprise support skills into a complete DevOps engineering skillset, with **9 portfolio-grade GitHub repositories** as evidence — one per module, ready to link from a CV, LinkedIn, or resume.

## Modules and Their Repositories

| # | Module | Repo | Tools | Builds On |
|---|--------|------|-------|-----------|
| 00 | Foundations & Mindset | `devops-foundations` | Setup, Git, GitHub | Existing Linux/cloud knowledge |
| 01 | Version Control Mastery | `git-mastery-lab` | Git, GitHub | Basic git usage |
| 02 | Infrastructure as Code | `terraform-aws-infra` | Terraform | Cloud experience (OCI) |
| 03 | Configuration Management | `ansible-automation` | Ansible | Linux administration |
| 04 | CI/CD Pipelines | `github-actions-cicd` | GitHub Actions | Git + Terraform + Ansible |
| 05 | Containers | `docker-applications` | Docker | Linux process/filesystem knowledge |
| 06 | Container Orchestration | `kubernetes-platform` | Kubernetes, Helm, ArgoCD | Docker + networking (CCNA) |
| 07 | Monitoring & Observability | `observability-stack` | Prometheus, Grafana | Splunk experience |
| 08 | Cloud Architecture & Integration | `cloud-architecture-capstone` | AWS, multi-cloud | OCI + all previous modules |

## Pre-Roadmap Setup

**Module 00 begins with `roadmap/00-foundations/github-setup.md`** — a complete walkthrough for:
- Creating a GitHub account (if Diego doesn't have one)
- Configuring git locally
- Installing and authenticating the `gh` CLI
- Setting up SSH keys and 2FA
- Connecting GitHub to the local Claude/IDE session

This is required before any other exercise.

## Learning Path Design

Each module contains:
- `summary.md`: Concepts, theory, and architecture explanations (reference material)
- `hands-on.md`: Structured exercises with scenarios, steps, and validation — all deliverables go to that module's GitHub repo

## Estimated Effort

- 9 modules, 3-6 sessions per module
- Each session: 60-90 minutes
- Total: ~30-48 sessions (2-4 months at 3 sessions per week)
- Output: 9 public GitHub repositories + a complete portfolio

## How to Use

1. Launch Claude from the `devops-roadmap/` project directory
2. First session: complete `github-setup.md` — once
3. Use `/setup-repo` to create each module's GitHub repo when you reach that module
4. Use `/next-lesson` to continue where you left off
5. Use `/challenge` to get hands-on exercises
6. Use `/review` to test knowledge retention
7. Use `/progress` to see the dashboard
8. All progress is tracked automatically in `progress/tracker.md`

## Portfolio Outcome

By the end of the roadmap, Diego's GitHub profile will show:

- 9 focused, well-documented public repositories
- A pinned profile README highlighting the journey
- Real CI/CD workflows running on his projects
- Architecture diagrams, ADRs, and runbooks
- Evidence of Terraform, Ansible, Docker, Kubernetes, GitHub Actions, and AWS competency
- A capstone project integrating everything in a production-grade system

This is what hiring managers look for when evaluating DevOps candidates: not just claims, but verifiable, runnable, well-documented work.
