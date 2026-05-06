# Module 01: Version Control Mastery (Git & GitHub)

## Why This Module

Git is the backbone of every DevOps workflow. Diego uses git for basic operations — this module builds the advanced skills needed for GitOps, collaborative development, and infrastructure-as-code workflows.

## Key Concepts

### Beyond Basic Git

- Rebasing vs merging (when and why)
- Interactive rebase for clean history
- Cherry-picking and bisect for debugging
- Stashing strategies for context switching
- Reflog as a safety net (connect to Diego's troubleshooting mindset)

### Branching Strategies

- **Trunk-based development**: Small, frequent merges to main (preferred for DevOps)
- **GitFlow**: Feature/release/hotfix branches (legacy, still seen in enterprise)
- **GitHub Flow**: Simple feature-branch model with PRs
- When to use each (team size, release cadence, risk tolerance)

### GitHub as a Platform

- Pull Requests as code review gates
- Branch protection rules and required checks
- GitHub Issues and Projects for work tracking
- CODEOWNERS for automated review assignment
- GitHub Releases and semantic versioning

### Git for Infrastructure

- Monorepo vs polyrepo strategies for IaC
- Commit message conventions (Conventional Commits)
- `.gitignore` patterns for Terraform state, secrets, build artifacts
- Signing commits for audit compliance
- Git hooks for pre-commit validation (linting, secrets scanning)

## Topics

1. Advanced git operations (rebase, cherry-pick, bisect)
2. Branching strategies and when to use each
3. Pull Request workflows and code review
4. GitHub features for teams (CODEOWNERS, branch rules, templates)
5. Git hooks and pre-commit frameworks
6. Commit signing and security
