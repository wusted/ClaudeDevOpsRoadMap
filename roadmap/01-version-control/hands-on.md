# Module 01: Version Control — Hands-On Exercises

## Module Repository: `git-mastery-lab`

All deliverables for this module live in `repos/git-mastery-lab/` and on GitHub at `github.com/<username>/git-mastery-lab`. Create it with `/setup-repo` before starting Exercise 1.1.

The repo's README should describe it as a sandbox demonstrating advanced git workflows, branching strategies, PR templates, and pre-commit automation.

---

## Exercise 1.1: Advanced Git Operations

**Objective**: Practice rebase, cherry-pick, and bisect in a controlled scenario.

**Context**: In DevOps, clean git history makes rollbacks and auditing possible. These skills are critical when managing infrastructure changes.

**Steps**:
1. Create a feature branch in `devops-lab` with 5+ commits (mix good and intentionally "bad" ones)
2. Use interactive rebase to squash, reorder, and edit commit messages
3. Create a second branch, cherry-pick a specific commit from the first
4. Use `git bisect` to find which commit introduced a "bug" (a deliberate bad change)
5. Practice using `git reflog` to recover from a "mistake"

**Validation**: Clean commit history, successful cherry-pick, bisect identifies the correct commit

---

## Exercise 1.2: Branch Protection and PR Workflow

**Objective**: Set up a professional GitHub repository workflow.

**Steps**:
1. Enable branch protection on `main`:
   - Require PR reviews (1 reviewer)
   - Require status checks to pass
   - Require linear history
2. Create a PR template (`.github/pull_request_template.md`) with sections: Description, Changes, Testing, Checklist
3. Create an issue template for bugs and features
4. Set up CODEOWNERS file assigning yourself to `terraform/` and `ansible/` directories
5. Make a PR following the workflow and verify protections work

**Validation**: Cannot push directly to main, PR template renders correctly, CODEOWNERS assigns reviewer

---

## Exercise 1.3: Pre-commit Hooks and Secrets Scanning

**Objective**: Automate code quality checks before commits reach the repository.

**Steps**:
1. Install `pre-commit` framework
2. Create `.pre-commit-config.yaml` with hooks for:
   - Trailing whitespace and file endings
   - YAML/JSON validation
   - Terraform fmt
   - Ansible-lint
   - Secret detection (gitleaks or detect-secrets)
3. Test by attempting to commit a file with a fake AWS key
4. Verify the hook blocks the commit

**Validation**: Pre-commit blocks bad commits, passes on clean ones

---

## Exercise 1.4: Conventional Commits and Changelog

**Objective**: Adopt a commit message standard that enables automated releases.

**Steps**:
1. Install commitizen or similar tool
2. Configure for Conventional Commits format
3. Make 10+ commits following the convention (feat, fix, docs, chore)
4. Generate a CHANGELOG.md automatically from commit history
5. Create a GitHub Release with release notes

**Validation**: All commits follow convention, CHANGELOG is generated, release exists on GitHub
