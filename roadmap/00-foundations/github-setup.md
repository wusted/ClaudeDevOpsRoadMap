# GitHub Account Setup Guide

This guide walks Diego through setting up GitHub from zero. This is **Pre-Exercise 0.0** — must be completed before any other exercise. Once done, every subsequent module produces a public repo on this account.

## Why This Matters

Each module's deliverables become a public GitHub repository. By the end of the roadmap, Diego will have **9 portfolio-grade repositories** demonstrating a complete DevOps skill set — directly linkable from his CV, LinkedIn, and resume.

## Step 1: Create the GitHub Account

1. Go to <https://github.com/signup>
2. Use a professional email (not the work email — this is portable across jobs)
3. Choose a username that:
   - Is professional (e.g., `diego-chavarria`, `dchavarria`, `diegocr`)
   - Will appear in URLs (`github.com/<username>/repo-name`) — recruiters will see it
   - Is short and memorable
4. Verify the email
5. Skip the paid features — the free tier covers everything in this roadmap

## Step 2: Set Up the Profile

The profile is the first thing recruiters see. Treat it like a mini-resume.

1. Go to **Settings → Profile**
2. Add:
   - Real name (Diego Chavarria Rodriguez)
   - Profile photo (professional headshot)
   - Bio (1-line: "Senior Linux Engineer at Oracle | Building DevOps expertise")
   - Location, company, website (optional but recommended)
3. Create a **profile README** (special repo named after your username):
   - Repo name = exact GitHub username
   - Make it public, initialize with README
   - Content: brief intro, current focus, key projects, contact links
   - This shows up at the top of `github.com/<username>`

## Step 3: Configure Local Git

Open a terminal:

```bash
git config --global user.name "Diego Chavarria Rodriguez"
git config --global user.email "<the-email-you-used-for-github>"
git config --global init.defaultBranch main
git config --global pull.rebase false
```

Verify:

```bash
git config --global --list | grep user
```

## Step 4: Install the GitHub CLI (`gh`)

The `gh` CLI is what Claude will use to create repos and manage GitHub from the session.

**macOS:**
```bash
brew install gh
```

**Linux (Debian/Ubuntu):**
```bash
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list
sudo apt update && sudo apt install gh
```

**Windows:**
```powershell
winget install --id GitHub.cli
```

Verify:
```bash
gh --version
```

## Step 5: Authenticate the CLI

```bash
gh auth login
```

Choose:
- **GitHub.com** (not Enterprise)
- **HTTPS** (simpler than SSH for now)
- **Yes** authenticate Git with GitHub credentials
- **Login with a web browser**

Follow the browser prompt, paste the one-time code, authorize.

Verify:
```bash
gh auth status
gh api user
```

The second command should print your GitHub user info — that confirms the CLI can act on your behalf.

## Step 6: Optional but Recommended — SSH Keys

For long-term use, SSH keys are more convenient than HTTPS tokens.

```bash
ssh-keygen -t ed25519 -C "<your-github-email>" -f ~/.ssh/id_ed25519_github
gh ssh-key add ~/.ssh/id_ed25519_github.pub --title "<your-machine-name>"
```

Test:
```bash
ssh -T git@github.com
```

You should see: `Hi <username>! You've successfully authenticated...`

## Step 7: Connect to Claude Code

Claude Code runs in your terminal and inherits your shell environment. Once `gh auth status` shows you're logged in, Claude can run `gh` commands directly during sessions — no extra configuration needed.

If you use the Claude Code IDE extension (VS Code, JetBrains), the same auth applies. Just make sure the IDE's integrated terminal can run `gh auth status` successfully.

## Step 8: Enable 2FA (Important)

GitHub now requires 2FA for contributors to public repositories.

1. Go to **Settings → Password and authentication**
2. Enable two-factor authentication
3. Use an authenticator app (Authy, 1Password, Aegis, or similar)
4. Save the recovery codes in a secure location

## Step 9: Verify Everything Works

Final smoke test from Claude:

```bash
gh auth status                         # Should show authenticated
gh repo list                           # Lists your repos (probably empty)
gh repo create test-repo --public      # Create a test repo
cd test-repo
echo "# Test" > README.md
git add . && git commit -m "test"
git push origin main
gh repo delete test-repo --yes         # Clean up
```

If all of these work, you're ready to start Module 00 — Exercise 0.1.

## Troubleshooting

| Problem | Fix |
|---------|-----|
| `gh: command not found` | Install via Step 4 |
| `gh auth status` says "not logged in" | Re-run `gh auth login` |
| Push prompts for password | Run `gh auth setup-git` to use the CLI's stored credentials |
| `Permission denied (publickey)` | SSH key not added to GitHub — re-do Step 6 |
| 2FA blocks pushes | Use `gh auth login` (it handles 2FA via browser) instead of password |

## Next Step

Once verified, return to Module 00 hands-on exercises. Exercise 0.1 will be the first repo creation (`devops-foundations`).
