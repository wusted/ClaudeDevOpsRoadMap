# Module 04: CI/CD Pipelines (GitHub Actions)

## Why This Module

CI/CD is where DevOps becomes real — code changes automatically build, test, and deploy without manual intervention. Diego's incident management experience gives him insight into what goes wrong without automation. This module builds the pipelines that prevent those incidents.

## Key Concepts

### CI vs CD

- **Continuous Integration**: Every commit triggers automated build + test
- **Continuous Delivery**: Code is always in a deployable state (manual deploy trigger)
- **Continuous Deployment**: Every commit that passes tests deploys automatically
- Diego's context: CI catches the issues he currently finds during support escalations

### GitHub Actions Architecture

```
Event (trigger) → Workflow → Jobs → Steps → Actions
```

- **Workflow**: YAML file in `.github/workflows/`
- **Event**: What triggers the workflow (push, PR, schedule, manual)
- **Job**: A set of steps running on one runner (parallel by default)
- **Step**: Individual command or action
- **Action**: Reusable unit from the marketplace or custom
- **Runner**: The machine executing the job (GitHub-hosted or self-hosted)

### Workflow Design Patterns

- Branch-based workflows (different pipelines for PR vs merge)
- Environment promotion (dev → staging → production)
- Required checks as quality gates
- Matrix builds for cross-platform/version testing
- Reusable workflows for DRY pipelines
- Composite actions for shared step sequences

### Security in Pipelines

- Secrets management (repository, environment, organization secrets)
- OIDC for cloud authentication (no long-lived keys)
- Dependency scanning (Dependabot, CodeQL)
- Supply chain security (pinning action versions by SHA)
- Least-privilege principle for workflow permissions

### Infrastructure Pipelines

- Terraform plan on PR, apply on merge
- Ansible playbook execution from CI
- Infrastructure testing in pipeline (Terratest, InSpec)
- Cost estimation in PR comments (Infracost)
- Drift detection on schedule

## Topics

1. Workflow syntax and triggers
2. Jobs, steps, and runner environments
3. Actions marketplace and custom actions
4. Secrets, variables, and environments
5. Matrix builds and conditional execution
6. Artifacts, caching, and performance
7. Reusable workflows and composite actions
8. Deployment workflows (environments, approvals, rollbacks)
9. Self-hosted runners (when and why)
10. Complete infrastructure pipeline (Terraform + Ansible + Deploy)
