# Module 03: Configuration Management (Ansible)

## Why This Module

Diego configures and troubleshoots Linux systems daily — manually. Ansible automates exactly what he already does, making his expertise repeatable, auditable, and scalable. Terraform creates the infrastructure; Ansible configures what runs on it.

## Key Concepts

### Terraform vs Ansible

| Terraform | Ansible |
|-----------|---------|
| Provisions infrastructure | Configures software on infrastructure |
| Declarative (desired state of resources) | Declarative playbooks, procedural execution |
| State-based (tracks what exists) | Stateless (checks current state each run) |
| Cloud APIs | SSH/WinRM to machines |

They complement each other: Terraform creates the server, Ansible configures it.

### Ansible Architecture

- **Control node**: Where you run Ansible (your machine or CI runner)
- **Managed nodes**: Target machines (no agent needed — agentless via SSH)
- **Inventory**: List of managed nodes (static files or dynamic from cloud APIs)
- **Modules**: Units of work (apt, yum, copy, template, service, etc.)
- **Playbooks**: YAML files defining desired state across hosts
- **Roles**: Reusable bundles of tasks, handlers, templates, vars
- **Galaxy**: Community marketplace for roles and collections

### Idempotency

- Running a playbook twice produces the same result
- Modules handle the "check if already done" logic
- Changed vs OK status — understand when Ansible actually makes changes
- Diego's analogy: like a checklist that skips already-completed items

### Inventory Management

- Static inventory (INI or YAML files)
- Dynamic inventory (scripts or plugins that query cloud APIs)
- Groups and group variables
- Host variables and precedence
- Patterns for targeting subsets of hosts

### Roles and Galaxy

- Standard role directory structure
- `defaults/` vs `vars/` precedence
- Handlers for service restarts
- Templates with Jinja2
- Ansible Galaxy for community roles
- Building and publishing your own roles

### Secrets with Vault

- Encrypting sensitive variables
- Vault passwords and password files
- Encrypting individual variables vs whole files
- Integration with external secret managers

## Topics

1. Installation and ad-hoc commands
2. Inventory (static, dynamic, patterns)
3. Playbooks (tasks, handlers, variables, conditionals, loops)
4. Roles (structure, dependencies, Galaxy)
5. Templates (Jinja2 filters, conditionals, loops)
6. Ansible Vault (secrets management)
7. Testing (ansible-lint, molecule, check mode)
8. Ansible + Terraform integration patterns
9. Performance (async, pipelining, mitogen)
10. AWX/Automation Platform (enterprise context)
