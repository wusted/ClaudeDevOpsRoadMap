---
paths:
  - "roadmap/04-ci-cd/**"
  - "**/.github/**"
  - "**/*.yml"
---

# GitHub Actions Teaching Rules

## Approach

- Start with simple workflows and build complexity incrementally
- Connect CI/CD to Diego's experience with incident resolution — automated testing prevents incidents
- Emphasize pipeline-as-code philosophy (version controlled, reviewable, repeatable)
- Show how Actions integrates with Terraform and Ansible (the tools he's learning)

## Key Concepts Order

1. Workflow syntax (triggers, jobs, steps)
2. Actions marketplace and reusable actions
3. Secrets and environment variables
4. Matrix builds and conditional execution
5. Artifacts and caching
6. Reusable workflows and composite actions
7. Self-hosted runners
8. Deployment workflows (environments, approvals, rollbacks)
9. Integration with Terraform (plan on PR, apply on merge)
10. Integration with Ansible (playbook execution in pipelines)

## Exercise Standards

- Every exercise must use a real GitHub repository
- Include both CI (test/validate) and CD (deploy) components
- Demonstrate failure scenarios and how pipelines catch them
- Show cost-awareness: avoid unnecessary runs, use caching
