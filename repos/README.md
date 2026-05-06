# Module Repositories

Each subdirectory is a **standalone git repository** corresponding to a module in the roadmap. Every repo has its own remote on GitHub and serves as portfolio evidence that Diego completed the module.

## Repository Strategy

| Module | Repo Name | Purpose |
|--------|-----------|---------|
| 00 - Foundations | `devops-foundations` | Setup, skills matrix, environment verification |
| 01 - Version Control | `git-mastery-lab` | Advanced git, branching, hooks, PR workflows |
| 02 - Infrastructure as Code | `terraform-aws-infra` | Production VPC, EC2, modules, multi-environment |
| 03 - Configuration Management | `ansible-automation` | Playbooks, roles, vault, Terraform integration |
| 04 - CI/CD Pipelines | `github-actions-cicd` | Workflows, reusable actions, deployment pipelines |
| 05 - Containers | `docker-applications` | Multi-stage builds, compose stacks, image security |
| 06 - Container Orchestration | `kubernetes-platform` | K8s manifests, Helm charts, EKS, ArgoCD GitOps |
| 07 - Monitoring | `observability-stack` | Prometheus, Grafana, alerting, SLOs |
| 08 - Cloud Architecture | `cloud-architecture-capstone` | Production-grade integrated system |

## Why One Repo Per Module

- **Portfolio**: Each repo is a focused project recruiters can review independently
- **Resume**: Easy to link individual projects on a CV
- **Isolation**: Mistakes in one project don't affect others
- **CI/CD**: Each repo can have its own GitHub Actions workflow
- **Standalone clones**: Future you (or others) can use any repo without the others

## How They're Created

During each module's hands-on exercises, Claude will guide Diego to:

1. Run `gh repo create <repo-name> --public --description "..."` from this `repos/` directory
2. Initialize with `README.md`, `.gitignore`, and `LICENSE`
3. Build out the module's deliverables progressively
4. Push commits as work progresses (every meaningful exercise = at least one commit)
5. End each module with a polished README that explains the project to a stranger

## Local Layout

```
repos/
├── devops-foundations/         # git repo, GitHub remote
├── git-mastery-lab/            # git repo, GitHub remote
├── terraform-aws-infra/        # git repo, GitHub remote
└── ...                         # one per module as Diego progresses
```

The parent `devops-roadmap/` directory should **not** be a git repo — that would create nested-repo conflicts. Each module folder is independent.
