# 🚀 Git & GitHub Quick Reference Guide

A concise step-by-step guide for beginners to manage code with Git and GitHub.

---

## 1. Install & Setup Git

Check if Git is installed:
```bash
git --version
```

Configure your identity (one-time setup):
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

---

## 2. Create a Repository on GitHub

- Go to [GitHub](https://github.com) → “New Repository”
- Give it a name (e.g., `my-project`)
- Copy the repository URL (HTTPS or SSH)

---

## 3. Clone Repository to Local Machine

```bash
git clone https://github.com/username/my-project.git
cd my-project
```

> Replace the URL with your actual repository link.

---

## 4. Add Files to Staging Area

Stage all modified/new files:
```bash
git add .
```

> Or stage specific files:  
> `git add filename.ext`

---

## 5. Commit Your Changes

Create a commit with a descriptive message:
```bash
git commit -m "feat: initial commit"
```

✅ Use conventional commit prefixes like:
- `feat:` for new features
- `fix:` for bug fixes
- `docs:`, `style:`, `refactor:`, etc.

---

## 6. Push Code to Remote (GitHub)

Push your committed changes to the remote branch:
```bash
git push origin main
```

> Replace `main` with `master` if your default branch is named `master`.

---

## 7. Always Pull Before Starting Work

Fetch and merge latest changes from remote:
```bash
git pull origin main
```

> ⚠️ Do this before creating a new branch or making changes — avoids conflicts later!

---

## 8. Create and Switch to a New Feature Branch

```bash
git switch -c branch-name
```

> This creates a new branch and switches to it in one command.  
> Example: `git switch -c feature/login-page`

---

## 9. Develop, Commit, and Push on Feature Branch

After making changes:
```bash
git add .
git commit -m "feat: add login functionality"
git push origin branch-name
```

> Replace `branch-name` with your actual branch name (e.g., `feature/login-page`)

---

## 10. Switch Back to Main Branch

```bash
git switch main
```

> Always return to `main` before merging other branches.

---

## 11. Merge Feature Branch into Main

```bash
git merge branch-name
```

> If there are **merge conflicts**, resolve them manually in the files, then:
> ```bash
> git add .
> git commit -m "fix: resolve merge conflicts"
> ```

---

## 12. Push Merged Result to Remote Main

```bash
git push origin main
```

> Now your feature is live in the main branch on GitHub.

---

## 📝 Best Practices & Notes

✅ **Do NOT develop directly on `main`**  
→ Always create a new branch for each feature or bug fix.

✅ **Always `git pull origin main` before starting work**  
→ Ensures you’re working on the latest codebase.

✅ **Write clear, meaningful commit messages**  
→ Helps you and your team understand changes later.

✅ **Push feature branches to remote**  
→ Enables backup, collaboration, and Pull Requests on GitHub.

✅ **Use Pull Requests (PRs) on GitHub for team projects**  
→ Safer and more transparent than merging locally.

---

## 🧩 Bonus: Common Commands Cheat Sheet

| Task                        | Command                          |
|-----------------------------|----------------------------------|
| Check status                | `git status`                     |
| View commit history         | `git log --oneline`              |
| List branches               | `git branch`                     |
| Delete local branch         | `git branch -d branch-name`      |
| Undo last commit (soft)     | `git reset --soft HEAD~1`        |
| Discard local file changes  | `git restore filename`           |