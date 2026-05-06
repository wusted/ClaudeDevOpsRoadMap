# DevOps Roadmap — Handoff Document for Diego

This document captures the conversation and design decisions that produced the `devops-roadmap/` Claude Code project structure. Read this once, then start using the project from your Claude Code account.

---

## Original Request

The project was set up by a colleague who asked Claude to:

1. Create a Claude Code project structure for a DevOps Roadmap, following the visual structure example shown in a reference image (CLAUDE.md, README.md, docs/, .claude/, src/, etc.) and following best practices from the official Claude documentation: <https://code.claude.com/docs/en/claude-directory> and <https://code.claude.com/docs/en/memory>.
2. Tailor the roadmap specifically to **Diego Chavarria Rodriguez's** profile (Senior Linux Support Engineer at Oracle, LPIC-1, OCI Foundations, Splunk Certified Admin, CCNA coursework, 8+ years of IT experience).
3. Include the requested tools: **Terraform, Ansible, GitHub, GitHub Actions** — plus other relevant tools as appropriate.
4. Deliver the roadmap as **summary + hands-on**: summaries integrated into the project structure, hands-on exercises defined as plans/scenarios that Diego works through interactively with Claude.
5. **Every deliverable becomes portfolio evidence on Diego's GitHub account.** Each module produces a standalone public GitHub repository — directly linkable from his CV, LinkedIn, and resume.
6. Help Diego set up GitHub from scratch if he doesn't have an account, and connect it to his local Claude/IDE session.
7. The user launches Claude, picks up progress from previous sessions, and Claude acts as a Senior DevOps Engineer mentor — interactively, **not via canned prompts**.

---

## Profile Used to Tailor the Roadmap

```
Senior IT professional with more than 8 years of experience across Linux administration,
enterprise support, cloud technologies, and technical leadership.

Experience:
- Oracle - Senior Linux Support Engineer (April 2022 - April 2026)
  Linux OS troubleshooting, kernel crashes, boot/patching/filesystem issues,
  performance, log analysis, scripting, OCI + hybrid architectures.
- Sykes - Splunk Certified Engineer (Aug 2019 - Mar 2022)
  Distributed Splunk troubleshooting (forwarders, indexers, search heads, clustering).
- Sykes - Sonos Subject Matter Expert / Technical Support (Oct 2018 - Aug 2019)

Certifications:
- LPIC-1 (Certified Linux Administrator)
- Splunk Enterprise Certified Admin
- Splunk Core Certified Power User
- Oracle Cloud Infrastructure 2025 Certified Foundations Associate

Trainings:
- CISCO CCNA1, CCNA2, CCNA3, IT Essentials

Languages: English C1, Spanish C2
```

The roadmap explicitly skips foundational topics Diego already masters (basic Linux, networking fundamentals, monitoring philosophy) and goes deeper on what's new (declarative IaC, GitOps, CI/CD design, container orchestration, cloud architecture).

---

## Tools Covered in the Roadmap

**Required by the user**: Terraform, Ansible, GitHub, GitHub Actions

**Added because they fit Diego's trajectory**:
- **Docker** — natural extension of his Linux process/filesystem/namespace knowledge
- **Kubernetes** — leverages his networking (CCNA) and Linux admin background
- **Prometheus + Grafana** — translates his Splunk monitoring expertise to cloud-native observability
- **AWS** — broadens beyond his OCI experience to multi-cloud
- **Helm, ArgoCD** — modern Kubernetes deployment patterns
- **Pre-commit, ansible-lint, Trivy, Infracost** — quality and security gates

---

## Portfolio Strategy: One GitHub Repo Per Module

Every module produces a **public GitHub repository** in `repos/<repo-name>/` locally and at `github.com/<username>/<repo-name>` remotely. Each repo is:

- Standalone and independently linkable from a resume
- Polished with a recruiter-grade README, architecture diagrams, and documentation
- Built progressively across 3-6 sessions (one commit per exercise minimum)
- Configured with appropriate `.gitignore`, `LICENSE`, and topics

| Module | Repo |
|--------|------|
| 00 - Foundations | `devops-foundations` |
| 01 - Version Control | `git-mastery-lab` |
| 02 - Infrastructure as Code | `terraform-aws-infra` |
| 03 - Configuration Management | `ansible-automation` |
| 04 - CI/CD Pipelines | `github-actions-cicd` |
| 05 - Containers | `docker-applications` |
| 06 - Container Orchestration | `kubernetes-platform` |
| 07 - Monitoring | `observability-stack` |
| 08 - Cloud Architecture | `cloud-architecture-capstone` |

By the end, Diego will have 9 public repositories demonstrating a complete DevOps skill set — directly verifiable by any hiring manager.

---

## Project Structure (Final)

```
devops-roadmap/
├── CLAUDE.md                              # Loaded every session: role, protocol, portfolio strategy
├── HANDOFF.md                             # This file
├── .claude/
│   ├── settings.json                      # Permissions (DevOps tools allowed; git/brew prompt)
│   ├── rules/                             # Topic-scoped instructions (DRY, path-scoped)
│   │   ├── teaching-style.md              # Calibrated to Diego's existing skills
│   │   ├── terraform.md                   # Path-scoped (loads only for .tf or Module 02)
│   │   ├── ansible.md                     # Path-scoped (loads only for .yml or Module 03)
│   │   ├── github-actions.md              # Path-scoped (loads only for .github or Module 04)
│   │   └── hands-on.md                    # Format and pedagogy for exercises
│   ├── skills/                            # Slash commands for the workflow
│   │   ├── next-lesson/SKILL.md           # /next-lesson — pick up where you left off
│   │   ├── review/SKILL.md                # /review — quiz on past topics
│   │   ├── challenge/SKILL.md             # /challenge — get a hands-on exercise
│   │   ├── progress/SKILL.md              # /progress — dashboard view
│   │   └── setup-repo/SKILL.md            # /setup-repo — create the module's GitHub repo
│   └── agents/
│       └── devops-mentor.md               # Subagent for code review and architecture feedback
├── roadmap/
│   ├── README.md                          # Overview, module table, repo strategy
│   ├── 00-foundations/                    # DevOps mindset, env setup
│   │   ├── summary.md
│   │   ├── github-setup.md                # Complete GitHub account + CLI setup walkthrough
│   │   └── hands-on.md                    # 4 exercises producing the devops-foundations repo
│   ├── 01-version-control/                # → git-mastery-lab repo (4 exercises)
│   ├── 02-infrastructure-as-code/         # → terraform-aws-infra repo (6 exercises)
│   ├── 03-configuration-management/       # → ansible-automation repo (6 exercises)
│   ├── 04-ci-cd/                          # → github-actions-cicd repo (6 exercises)
│   ├── 05-containers/                     # → docker-applications repo (5 exercises)
│   ├── 06-orchestration/                  # → kubernetes-platform repo (6 exercises)
│   ├── 07-monitoring/                     # → observability-stack repo (6 exercises)
│   └── 08-cloud-architecture/             # → cloud-architecture-capstone repo (6 exercises)
├── repos/                                 # Cloned module repositories live here
│   └── README.md                          # Repo strategy and naming reference
└── progress/
    └── tracker.md                         # Session log, module status, repo URLs
```

---

## How It Works (For Diego)

### One-time setup (Module 00 — start here)

1. Install Claude Code: <https://code.claude.com/docs/en/quickstart>
2. Copy the entire `devops-roadmap/` directory to your machine.
3. From inside the directory, run `claude` to start a session.
4. **Tell Claude**: "I'm starting from scratch — walk me through the GitHub setup before any exercises."
5. Claude will follow `roadmap/00-foundations/github-setup.md`:
   - Create a GitHub account (if you don't have one)
   - Configure git locally
   - Install and authenticate `gh` CLI
   - Set up 2FA and (optionally) SSH keys
   - Verify the integration works end-to-end

### Every subsequent session

1. From inside `devops-roadmap/`, run:
   ```
   claude
   ```
2. Claude automatically reads `CLAUDE.md` and `progress/tracker.md` and knows where you left off.
3. Use these slash commands:
   - `/next-lesson` — Continue to the next topic
   - `/challenge` — Get a hands-on exercise for the current module
   - `/review` — Quiz yourself on completed material
   - `/progress` — See your dashboard
   - `/setup-repo` — Create a new module's GitHub repo (used when starting a new module)
4. All work happens inside `repos/<current-module-repo>/` — never edit files in the roadmap directories.
5. At session end, Claude updates `progress/tracker.md`, ensures changes are committed, and pushes to GitHub.

### Mentoring style

Claude is configured to act as a **Senior DevOps Engineer mentor**, not a tutor. It will:
- Skip basics you already know (Linux, networking, monitoring philosophy)
- Connect new concepts to your existing experience (e.g., Splunk → Prometheus, OCI → AWS)
- Always pair theory with hands-on practice
- Use the Socratic method during exercises — ask guiding questions before giving answers
- Treat every exercise as portfolio work: code quality, README clarity, and commit history all count
- Track everything in `progress/tracker.md` so each session resumes naturally

---

## Design Decisions (For Reference)

### Why one repo per module

- **Resume**: Each repo is a focused, individually-linkable project recruiters can review
- **Isolation**: Mistakes or experiments in one module don't pollute others
- **CI/CD**: Each repo gets its own GitHub Actions workflows, demonstrating real-world habits
- **Standalone reusability**: Future Diego (or anyone else) can clone any single repo without context

### Why path-scoped rules

Following the official Claude Code docs (`.claude/rules/*.md` with `paths:` frontmatter), topic-specific guidance only loads when relevant — Terraform rules don't pollute context when working on Ansible. This keeps the session-start context small and focused.

### Why a `progress/tracker.md`

Auto memory in `~/.claude/projects/` is per-machine and not portable. A `progress/tracker.md` in the project directory works across machines, can be shared with mentors, and survives `/compact`.

### Why skills, not commands

Per current Claude docs, skills (`skills/<name>/SKILL.md`) are the recommended pattern over single-file commands. They support bundled supporting files if extensions are needed later.

### Why a `devops-mentor` subagent

Code review and architecture feedback benefit from a fresh context. The subagent runs in isolation and won't pollute the main learning conversation with verbose review output.

### Why no parent git repo

The `devops-roadmap/` parent is **not** a git repo because nested git repos cause headaches. Each `repos/<module>/` is its own independent repo with its own GitHub remote.

### Permissions

`.claude/settings.json` pre-allows the DevOps tools (`terraform`, `ansible`, `docker`, `kubectl`, `gh`, `python`, `pip`) so Claude doesn't prompt for every command. **`git` and `brew` were intentionally left out** — those will prompt for confirmation, which is safer for a learning environment.

---

## Suggested First Session

When Diego launches Claude for the first time, suggested starting prompt:

> "Hi, I'm Diego. I don't have a GitHub account yet. Walk me through the complete setup before any roadmap exercises, then start /next-lesson when I'm ready."

Claude will:
1. Open `roadmap/00-foundations/github-setup.md` and guide Diego step by step
2. Verify each step (account, git config, `gh` auth, 2FA, optional SSH)
3. After verification succeeds, run `/setup-repo` to create the `devops-foundations` repo
4. Begin Module 00 hands-on exercises

If Diego already has a GitHub account, suggested prompt:

> "Hi, I'm Diego. I have a GitHub account but the `gh` CLI isn't set up yet. Help me authenticate and verify, then start /next-lesson."

---

## Module Summary at a Glance

| # | Module | Repo | Exercises | Builds On |
|---|--------|------|-----------|-----------|
| 00 | Foundations & Mindset | `devops-foundations` | 4 (incl. GitHub setup) | Existing Linux/cloud knowledge |
| 01 | Version Control Mastery | `git-mastery-lab` | 4 | Basic git usage |
| 02 | Infrastructure as Code | `terraform-aws-infra` | 6 | Cloud experience (OCI) |
| 03 | Configuration Management | `ansible-automation` | 6 | Linux administration |
| 04 | CI/CD Pipelines | `github-actions-cicd` | 6 | Git + Terraform + Ansible |
| 05 | Containers | `docker-applications` | 5 | Linux process/filesystem |
| 06 | Container Orchestration | `kubernetes-platform` | 6 | Docker + networking |
| 07 | Monitoring & Observability | `observability-stack` | 6 | Splunk experience |
| 08 | Cloud Architecture & Integration | `cloud-architecture-capstone` | 6 | OCI + all previous modules |

**Estimated effort**: ~30-48 sessions of 60-90 minutes each (2-4 months at 3 sessions per week).

**Final portfolio**: 9 public GitHub repositories ready to link from CV, LinkedIn, and job applications.

---

## What to Do If Something Doesn't Work

- **Claude doesn't seem to know the project**: Make sure you launched `claude` from inside the `devops-roadmap/` directory, not a parent.
- **A slash command doesn't show up**: Restart the session. Skills are loaded at session start.
- **Progress isn't being tracked**: Ask Claude directly: "Update the progress tracker with what we just did."
- **`gh auth status` says not logged in mid-session**: Run `gh auth login` again from a regular terminal, then return to Claude.
- **You want a different teaching style**: Edit `.claude/rules/teaching-style.md` to suit you. Claude reads it next session.
- **You want to skip ahead**: Tell Claude: "Skip to Module 04, Exercise 4.3." It will adjust and update the tracker.
- **A repo on GitHub got messy**: Tell Claude: "Reset the X repo to commit Y." Claude can use `git reset` interactively.

---

## Reference: Documentation Used

- Claude Code project structure: <https://code.claude.com/docs/en/claude-directory>
- Memory and persistent context: <https://code.claude.com/docs/en/memory>
- Skills: <https://code.claude.com/docs/en/skills>
- Subagents: <https://code.claude.com/docs/en/sub-agents>
- GitHub CLI: <https://cli.github.com/manual/>

---

## Conversation Log Summary

This handoff was generated after a design session that:

1. Reviewed the official Claude Code documentation for `.claude/` directory and memory patterns.
2. Took Diego's profile as input to calibrate teaching depth.
3. Decided on the 9-module structure (00-08), with summary + hands-on per module.
4. Created path-scoped rules for DRY topic-specific guidance.
5. Created 5 slash command skills for the interactive workflow (including `/setup-repo`).
6. Created a `devops-mentor` subagent for isolated code review.
7. Set permissions to pre-allow DevOps tools while keeping `git` and `brew` confirmation-gated.
8. Wrote ~50 hands-on exercises across 9 modules, all building progressively.
9. **Restructured the deliverable model**: every module produces its own portfolio-grade GitHub repository in `repos/<repo-name>/`, with comprehensive GitHub onboarding in Module 00.

Good luck Diego — this is structured to take you from Senior Linux Support to a complete DevOps engineer over a few months. Lean on Claude, do every exercise, commit and push everything, and at the end you'll have 9 public repos that prove the journey.
