# Module 02: Infrastructure as Code (Terraform)

## Why This Module

Diego manages infrastructure manually and through console UIs. Terraform codifies that knowledge into repeatable, versionable, reviewable infrastructure definitions. This is the core DevOps skill that transforms operations into engineering.

## Key Concepts

### Declarative Infrastructure

- You describe WHAT you want, not HOW to get there
- Terraform computes the diff between current and desired state
- Contrast with shell scripts (imperative): Terraform is idempotent by design
- Diego's analogy: like a desired-state configuration vs a runbook

### Terraform Architecture

```
Providers → Resources → State → Plan → Apply
```

- **Providers**: Plugins that talk to cloud APIs (AWS, OCI, GitHub, Docker)
- **Resources**: The infrastructure objects you manage
- **State**: Terraform's record of what exists (critical to understand)
- **Plan**: Preview of changes before execution
- **Apply**: Execute the changes

### State Management

- Local state (development only)
- Remote state (S3 + DynamoDB, Terraform Cloud, etc.)
- State locking (prevent concurrent modifications)
- State drift detection and remediation
- Importing existing infrastructure into state

### Module Design

- Root module vs child modules
- Input variables, output values, local values
- Module composition patterns
- Terraform Registry (public modules)
- When to build custom modules vs use community ones

### Environments and Workspaces

- Directory-per-environment pattern
- Terraform workspaces (use cases and limitations)
- Variable files per environment (`.tfvars`)
- Backend configuration per environment

### Testing and Validation

- `terraform validate` and `terraform fmt`
- `terraform plan` as a test (plan in CI, apply on merge)
- Terratest for integration testing
- Policy as Code (Sentinel, OPA/Rego)
- Cost estimation (Infracost)

## Topics

1. HCL syntax and resource basics
2. Providers and authentication
3. State management (local, remote, locking)
4. Variables, outputs, data sources
5. Modules (structure, composition, registry)
6. Environments and workspaces
7. Importing existing infrastructure
8. Testing and CI integration
9. Advanced patterns (for_each, dynamic blocks, depends_on)
10. Terraform + GitHub Actions integration
