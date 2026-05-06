---
paths:
  - "roadmap/03-configuration-management/**"
  - "**/*.yml"
  - "**/*.yaml"
  - "**/ansible/**"
---

# Ansible Teaching Rules

## Approach

- Diego already manages Linux systems manually — Ansible automates what he already does
- Start with ad-hoc commands to show immediate value, then move to playbooks
- Emphasize idempotency: running a playbook twice should produce the same result
- Connect to his enterprise support experience — Ansible replaces manual runbooks

## Key Concepts Order

1. Inventory (static, dynamic)
2. Ad-hoc commands (modules: ping, command, copy, service)
3. Playbooks (tasks, handlers, variables)
4. Roles (structure, Galaxy, custom)
5. Templates (Jinja2)
6. Vault (secrets management)
7. Ansible + Terraform integration
8. AWX/Tower for enterprise (connect to his Oracle enterprise background)

## Exercise Standards

- Use local VMs or containers as targets (Docker containers as Ansible targets)
- Always test with `--check` (dry-run) first
- Include `ansible-lint` validation
- Exercises should build on each other — each one extends the previous infrastructure
