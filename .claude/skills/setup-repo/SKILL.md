---
description: Create and initialize the GitHub repository for the current or specified DevOps module
argument-hint: <module-number-or-name>
---

Read `progress/tracker.md` to identify the current module (or use $ARGUMENTS if specified).

Map the module to its repo name from the table in CLAUDE.md.

Steps:

1. Check if the repo already exists:
   - Look for `repos/<repo-name>/` locally
   - Check `gh repo view <username>/<repo-name>` remotely
   - If both exist, skip creation and confirm with Diego that he wants to continue work in it

2. If the repo doesn't exist, create it:
   - Run from `repos/`: `gh repo create <repo-name> --public --description "<module-description>" --clone`
   - Description should be one sentence summarizing what the module covers
   - The `--clone` flag creates the local copy automatically

3. Initialize the repo with quality scaffolding:
   - `README.md` with: title, description, prerequisites, repo structure, how to use
   - `.gitignore` appropriate for the module's tools (Terraform, Ansible, Docker, etc.)
   - `LICENSE` (MIT by default unless Diego prefers otherwise)
   - Optional: `.editorconfig`, `.pre-commit-config.yaml` if relevant

4. Make the initial commit:
   - `git add .`
   - `git commit -m "chore: initialize <repo-name> for DevOps roadmap module <NN>"`
   - `git push origin main`

5. Configure repo settings via `gh`:
   - Add topics: `gh repo edit --add-topic devops --add-topic <module-tools>`
   - Enable issues, disable wiki (or vice versa per Diego's preference)

6. Update `progress/tracker.md` with the repo URL

7. Confirm to Diego: repo is live at `https://github.com/<username>/<repo-name>` and ready for the module's exercises
