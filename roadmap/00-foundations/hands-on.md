# Module 00: Foundations — Hands-On Exercises

## Module Repository: `devops-foundations`

All deliverables for this module live in `repos/devops-foundations/` and on GitHub at `github.com/<username>/devops-foundations`.

---

## Pre-Exercise 0.0: GitHub Account Setup

**Objective**: Create a professional GitHub presence and connect it to the local development environment.

**Reference**: Follow the complete walkthrough in `roadmap/00-foundations/github-setup.md`.

**Validation**: All of the following succeed in the terminal:
- `gh auth status` shows authenticated
- `gh api user` returns Diego's GitHub profile JSON
- `git config --global user.name` and `user.email` match the GitHub account
- A test repo can be created and deleted via `gh repo create` / `gh repo delete`

**Important**: This step is required before any other exercise. Claude will refuse to proceed with module work until `gh auth status` confirms authentication.

---

## Exercise 0.1: Create the Foundations Repository

**Objective**: Create the first portfolio repository — `devops-foundations`.

**Context**: This repo will document the DevOps journey: skills assessment, environment setup, and learnings. It's also the first practice run of the per-module repo workflow.

**Steps**:
1. From `devops-roadmap/repos/`, create the repo:
   ```bash
   gh repo create devops-foundations --public \
     --description "DevOps learning journey: skills matrix, environment setup, and foundational concepts" \
     --clone
   cd devops-foundations
   ```
2. Create a polished `README.md` covering:
   - Project purpose (portfolio piece for DevOps roadmap)
   - About me (1 paragraph linking to LinkedIn)
   - Roadmap modules (link to other repos as they're created)
   - Tech stack covered across the journey
3. Add a `.gitignore` with common patterns for the tools used in this roadmap
4. Add a `LICENSE` file (MIT)
5. Make the initial commit and push:
   ```bash
   git add .
   git commit -m "chore: initialize devops-foundations repo"
   git push origin main
   ```
6. Add repo topics on GitHub: `devops`, `linux`, `learning-by-doing`

**Validation**: Repo is public on GitHub, README renders cleanly, repo appears at `github.com/<username>?tab=repositories`

**Stretch Goal**: Create your **profile README** (the special repo named after your username). Add a brief intro and a section listing this roadmap's repos as they're built.

---

## Exercise 0.2: Skills Matrix and DevOps Lifecycle Mapping

**Objective**: Document existing expertise mapped to DevOps lifecycle stages — provides honest baseline for prioritization.

**Steps**:
1. In the `devops-foundations` repo, create `docs/skills-matrix.md`
2. Create a table for each DevOps lifecycle stage (Plan, Code, Build, Test, Release, Deploy, Operate, Monitor):
   - What you already know (tools, practices, years of experience)
   - What you need to learn (specific gaps)
   - Priority (P0 critical / P1 important / P2 nice-to-have)
3. Add a "before / after" snapshot section that you'll update at the end of the roadmap
4. Commit:
   ```bash
   git add docs/skills-matrix.md
   git commit -m "docs: add skills matrix mapping current expertise to DevOps lifecycle"
   git push
   ```

**Validation**: Document is honest, specific, and committed to the repo. Recruiter could read it and understand your starting point.

---

## Exercise 0.3: Environment Setup and Verification

**Objective**: Install and verify all tools needed for the entire roadmap, then document the setup.

**Steps**:
1. Install and verify each tool with `--version`:
   - `terraform`, `ansible`, `ansible-lint`, `docker`, `kubectl`, `helm`, `gh`
   - `python3`, `pip`, `pre-commit`
   - `tflint`, `trivy` (security scanners)
   - `jq` and `yq` (JSON/YAML processing)
2. Create `docs/environment-setup.md` documenting:
   - OS and version
   - Each tool, its version, and the install command used
   - Any troubleshooting notes encountered during install
   - Output of `gh auth status` (redact tokens)
3. Create `scripts/verify-environment.sh` — a shell script that runs all `--version` commands and prints a green check or red X for each
4. Make it executable: `chmod +x scripts/verify-environment.sh`
5. Run it, capture output, save to `docs/verification-output.txt`
6. Commit:
   ```bash
   git add docs/ scripts/
   git commit -m "feat: add environment setup docs and verification script"
   git push
   ```

**Validation**: All tools respond to version commands, verification script runs cleanly, docs are reproducible by another engineer.

**Stretch Goal**: Add a section to the README linking to the verification script with badges (e.g., "Tools verified: ✓").

---

## Exercise 0.4: Document Your "Why"

**Objective**: Write a personal manifesto explaining the DevOps transition — useful for interviews, networking, and motivation.

**Steps**:
1. Create `docs/journey.md` with sections:
   - Where I'm coming from (Linux support background, key wins)
   - Why DevOps (technical and career motivations)
   - What I'm building toward (target role / responsibilities in 12 months)
   - How I'll measure success
2. Keep it under 500 words — concise wins
3. Commit:
   ```bash
   git add docs/journey.md
   git commit -m "docs: add personal journey statement"
   git push
   ```

**Validation**: Document is honest, specific, and would impress a hiring manager reading it cold.
