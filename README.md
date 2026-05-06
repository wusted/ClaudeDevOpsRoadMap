# Claude DevOps Roadmap

A Claude Code project that delivers a personalized DevOps learning journey through interactive sessions, hands-on exercises, and a portfolio of nine GitHub repositories.

Designed for engineers transitioning from Linux administration / enterprise support into a complete DevOps role.

## What This Is

This repository is a **Claude Code project structure** — not a tutorial. When you launch Claude from inside this directory, it acts as a Senior DevOps Engineer mentor, picks up where you left off, and guides you through the roadmap interactively.

By the end, you'll have **nine standalone public GitHub repositories** that demonstrate Terraform, Ansible, GitHub Actions, Docker, Kubernetes, Prometheus + Grafana, and AWS — directly linkable from a CV or LinkedIn.

## Quick Start

```bash
git clone https://github.com/wusted/ClaudeDevOpsRoadMap.git devops-roadmap
cd devops-roadmap
claude
```

First message to Claude:

> Hi, walk me through the GitHub setup before any roadmap exercises, then start /next-lesson when I'm ready.

Claude will:
1. Read `CLAUDE.md` for the session protocol
2. Walk you through `roadmap/00-foundations/github-setup.md` (account, `gh` CLI, 2FA, smoke test)
3. Run `/setup-repo` to create the first portfolio repo (`devops-foundations`)
4. Begin Module 00 hands-on exercises

## Roadmap Overview

| # | Module | Portfolio Repo |
|---|--------|----------------|
| 00 | Foundations & Mindset | `devops-foundations` |
| 01 | Version Control Mastery | `git-mastery-lab` |
| 02 | Infrastructure as Code | `terraform-aws-infra` |
| 03 | Configuration Management | `ansible-automation` |
| 04 | CI/CD Pipelines | `github-actions-cicd` |
| 05 | Containers | `docker-applications` |
| 06 | Container Orchestration | `kubernetes-platform` |
| 07 | Monitoring & Observability | `observability-stack` |
| 08 | Cloud Architecture & Integration | `cloud-architecture-capstone` |

Estimated effort: ~30-48 sessions of 60-90 minutes each (2-4 months at 3 sessions/week).

## Project Structure

```
devops-roadmap/
├── CLAUDE.md              # Session protocol and rules (loaded every session)
├── HANDOFF.md             # Full design notes and onboarding guide
├── README.md              # This file
├── .claude/
│   ├── settings.json      # Permissions for DevOps tools
│   ├── rules/             # Path-scoped teaching rules
│   ├── skills/            # /next-lesson, /challenge, /review, /progress, /setup-repo
│   └── agents/            # devops-mentor subagent for code review
├── roadmap/
│   ├── README.md          # Full module breakdown
│   └── 00-foundations/ ... 08-cloud-architecture/
├── repos/                 # Per-module portfolio repos created during the journey
└── progress/
    └── tracker.md         # Cross-session progress log
```

## Documentation

- **[HANDOFF.md](HANDOFF.md)** — Complete design rationale, profile context, and usage guide
- **[roadmap/README.md](roadmap/README.md)** — Module breakdown and learning path
- **[roadmap/00-foundations/github-setup.md](roadmap/00-foundations/github-setup.md)** — GitHub account onboarding for new users
- **[repos/README.md](repos/README.md)** — Repo naming strategy and rationale

## Requirements

- [Claude Code](https://code.claude.com/docs/en/quickstart)
- Git
- A terminal (macOS, Linux, or Windows with WSL)
- Tools installed during Module 00: `gh`, `terraform`, `ansible`, `docker`, `kubectl`, `helm`, `python3`

## Built With Claude

This project structure was generated through a Claude Code session that combined the official Claude Code documentation patterns (`CLAUDE.md`, path-scoped rules, skills, subagents) with a tailored DevOps curriculum.

## License

MIT
