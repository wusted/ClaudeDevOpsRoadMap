# Module 03: Configuration Management — Hands-On Exercises

## Module Repository: `ansible-automation`

All deliverables for this module live in `repos/ansible-automation/` and on GitHub at `github.com/<username>/ansible-automation`. Create it with `/setup-repo` before starting Exercise 3.1.

The repo's README should describe it as a portfolio of Ansible playbooks, roles, and Terraform integration patterns demonstrating idempotent configuration management. Include the Docker-based lab environment for reproducibility.

Replace earlier paths like `devops-lab/ansible/...` with in-repo equivalents (e.g., `lab-environment/`, `playbooks/`, `roles/`).

---

## Exercise 3.1: Ansible with Docker Targets

**Objective**: Set up an Ansible lab using Docker containers as managed nodes (no cloud cost).

**Context**: Docker containers simulate servers for safe Ansible practice. This is how DevOps teams test playbooks locally before running against production.

**Steps**:
1. Create `devops-lab/ansible/lab-environment/`
2. Write a Dockerfile that builds an SSH-enabled Ubuntu container
3. Create a `docker-compose.yml` with 3 containers (web1, web2, db1)
4. Build and start the containers
5. Create a static inventory file mapping container names to groups: `[webservers]`, `[databases]`
6. Test connectivity: `ansible all -m ping -i inventory.ini`
7. Run ad-hoc commands: install a package, copy a file, restart a service

**Validation**: All 3 containers respond to ping, ad-hoc commands succeed

---

## Exercise 3.2: First Playbook — Web Server Setup

**Objective**: Write a playbook that configures a web server from scratch.

**Steps**:
1. Create `devops-lab/ansible/playbooks/webserver.yml`
2. Tasks:
   - Update apt cache
   - Install nginx
   - Copy a custom `index.html` using a template (include hostname, date)
   - Configure nginx with a custom server block
   - Ensure nginx is started and enabled
   - Open firewall port 80 (if ufw is available)
3. Use handlers to restart nginx only when config changes
4. Run the playbook against `[webservers]` group
5. Verify nginx is serving the custom page
6. Run the playbook again — verify no changes (idempotency)

**Validation**: Nginx serves custom page, second run shows 0 changed tasks

---

## Exercise 3.3: Roles and Variable Precedence

**Objective**: Refactor the webserver playbook into a proper role with configurable variables.

**Steps**:
1. Create role structure: `ansible-galaxy init roles/webserver`
2. Move tasks, handlers, templates, and defaults into the role
3. Define variables in `defaults/main.yml` (port, server_name, document_root)
4. Override variables per host using `host_vars/`
5. Override per group using `group_vars/`
6. Create a site.yml that applies roles to groups
7. Deploy with different configurations per container

**Validation**: Same role produces different configs based on variable precedence. Can explain the precedence order.

---

## Exercise 3.4: Ansible Vault and Secrets

**Objective**: Manage sensitive data securely in Ansible.

**Steps**:
1. Create a vault-encrypted variable file with a simulated database password
2. Use the encrypted variable in a playbook (e.g., configure a database connection file)
3. Run the playbook with `--ask-vault-pass`
4. Set up a vault password file for automation (not committed to git!)
5. Encrypt a single variable inline with `ansible-vault encrypt_string`
6. Add vault password file to `.gitignore`
7. Demonstrate that the encrypted file can be committed safely

**Validation**: Playbook runs with vault, encrypted data is in git without exposing secrets

---

## Exercise 3.5: Terraform + Ansible Integration

**Objective**: Provision infrastructure with Terraform and configure it with Ansible automatically.

**Context**: This is the production pattern — Terraform creates, Ansible configures.

**Steps**:
1. Use Terraform to provision an EC2 instance (from Module 02 exercise)
2. Output the instance IP from Terraform
3. Generate a dynamic Ansible inventory from Terraform output (use `terraform output -json`)
4. Write a playbook that configures the instance (install packages, configure services)
5. Create a shell script or Makefile that runs: `terraform apply` → generate inventory → `ansible-playbook`
6. Test the full workflow end-to-end

**Validation**: Single command provisions AND configures infrastructure. Instance is fully configured after one run.

---

## Exercise 3.6: Ansible Linting and Testing

**Objective**: Add quality gates to Ansible code.

**Steps**:
1. Install and configure `ansible-lint`
2. Run it against all playbooks and fix violations
3. Install Molecule for role testing
4. Create a Molecule scenario for the webserver role
5. Run `molecule test` (creates container, applies role, verifies, destroys)
6. Add ansible-lint to the pre-commit hooks from Module 01

**Validation**: `ansible-lint` passes with no warnings, Molecule test completes the full cycle
