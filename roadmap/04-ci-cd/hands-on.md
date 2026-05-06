# Module 04: CI/CD Pipelines — Hands-On Exercises

## Module Repository: `github-actions-cicd`

All deliverables for this module live in `repos/github-actions-cicd/` and on GitHub at `github.com/<username>/github-actions-cicd`. Create it with `/setup-repo` before starting Exercise 4.1.

The repo's README should describe it as a portfolio of GitHub Actions workflows demonstrating CI/CD patterns: matrix builds, reusable workflows, environment-based deployments, and complete infrastructure pipelines integrating Terraform and Ansible.

Note: Some exercises reference Terraform/Ansible code from earlier modules. Either copy the relevant code into this repo or use git submodules to reference the earlier repos — Diego's choice.

---

## Exercise 4.1: First GitHub Actions Workflow

**Objective**: Create a basic CI pipeline that lints and validates code.

**Context**: Start simple. A workflow that validates your Terraform and Ansible code on every push.

**Steps**:
1. Create `.github/workflows/validate.yml` in `devops-lab`
2. Trigger on push to any branch and on PR to main
3. Jobs:
   - `terraform-validate`: Run `terraform fmt -check` and `terraform validate`
   - `ansible-lint`: Run ansible-lint on all playbooks
4. Both jobs should run in parallel
5. Push a commit with a formatting error and observe the failure
6. Fix and push again — observe the green check

**Validation**: Workflow triggers on push, catches lint errors, passes when fixed

---

## Exercise 4.2: Matrix Builds and Caching

**Objective**: Test across multiple configurations and optimize build speed.

**Steps**:
1. Create a workflow that tests Ansible playbooks against multiple OS versions using matrix:
   ```yaml
   strategy:
     matrix:
       os: [ubuntu-22.04, ubuntu-24.04]
       ansible-version: ["2.15", "2.16"]
   ```
2. Add caching for pip dependencies
3. Add a timeout-minutes to prevent runaway jobs
4. Add `continue-on-error` for one matrix combination (mark as experimental)
5. Observe the matrix visualization in GitHub

**Validation**: Matrix generates 4 job combinations, caching works on second run (faster)

---

## Exercise 4.3: Secrets and Environment-Based Deployment

**Objective**: Build a deployment pipeline with environment promotion and approvals.

**Steps**:
1. Create GitHub environments: `dev`, `staging`, `production`
2. Add protection rules: `production` requires manual approval
3. Add environment-specific secrets (e.g., different AWS accounts or regions)
4. Create a deployment workflow:
   - On push to main: deploy to dev automatically
   - Manual trigger: deploy to staging
   - Manual trigger with approval: deploy to production
5. Use environment variables to customize deployment per environment
6. Test the full promotion flow

**Validation**: Dev deploys automatically, staging is manual, production requires approval click

---

## Exercise 4.4: Reusable Workflows

**Objective**: Create DRY pipelines using reusable workflows and composite actions.

**Context**: Teams maintain many repositories. Reusable workflows prevent copy-pasting the same pipeline everywhere.

**Steps**:
1. Create a reusable workflow (`.github/workflows/terraform-reusable.yml`) with `workflow_call` trigger
2. Accept inputs: working directory, terraform version, environment
3. Steps: init → validate → plan → (conditional) apply
4. Create a composite action for Ansible deployment (multiple steps bundled)
5. Use both in a main workflow that orchestrates the full deployment
6. Test calling the reusable workflow with different inputs

**Validation**: One workflow definition serves multiple environments/projects via inputs

---

## Exercise 4.5: Full Infrastructure Pipeline

**Objective**: Build a complete end-to-end pipeline: validate → plan → deploy → configure → verify.

**Context**: This is the capstone for Modules 02-04. Everything connects.

**Steps**:
1. Create a workflow that:
   - On PR: terraform fmt, validate, plan (post plan as PR comment)
   - On merge to main: terraform apply → generate Ansible inventory → run Ansible playbook
   - Post-deployment: health check (curl the deployed service)
2. Handle failures: if Ansible fails, should Terraform be rolled back? Implement your decision
3. Add Infracost to show cost diff in PR comments
4. Add notification (GitHub issue or PR comment) on deployment success/failure
5. Test with a PR that adds a new resource

**Validation**: Complete pipeline from PR to deployed+configured infrastructure with visibility at every stage

---

## Exercise 4.6: Scheduled Workflows and Drift Detection

**Objective**: Use scheduled workflows for operational tasks.

**Steps**:
1. Create a workflow triggered by cron schedule (daily)
2. Run `terraform plan` and detect if there's drift (exit code check)
3. If drift detected: open a GitHub Issue with the plan output
4. Add a manual dispatch workflow for emergency operations
5. Create a workflow that runs security scanning (trivy, checkov) weekly

**Validation**: Scheduled workflow runs on time, drift creates an issue, security scan reports findings
