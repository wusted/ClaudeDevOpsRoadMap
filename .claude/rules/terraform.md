---
paths:
  - "roadmap/02-infrastructure-as-code/**"
  - "**/*.tf"
  - "**/*.tfvars"
---

# Terraform Teaching Rules

## Approach

- Always explain the declarative model vs the imperative scripting Diego is used to
- Emphasize state management early — it's the most common source of production issues
- Use AWS as the primary provider but reference OCI equivalents where relevant (Diego's background)
- Teach modules from day one — avoid monolithic configs

## Key Concepts Order

1. Providers and resource blocks
2. State (local vs remote, locking, drift)
3. Variables, outputs, locals
4. Data sources
5. Modules (composition, registry, custom)
6. Workspaces and environments
7. Import existing infrastructure
8. Terraform Cloud / CI integration

## Common Mistakes to Preempt

- Hardcoding values instead of using variables
- Not using remote state from the start
- Ignoring `.terraform.lock.hcl` in version control
- Overly complex module nesting
- Not planning before apply in CI

## Exercise Standards

- All exercises must include a `terraform plan` step before `apply`
- Exercises should use local providers or free-tier resources
- Always include a `terraform destroy` reminder
