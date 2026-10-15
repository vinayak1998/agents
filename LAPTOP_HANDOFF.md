# Laptop handoff — Agents course repo

Your work lives on your fork: https://github.com/vinayak1998/agents  
Course updates come from **upstream**: https://github.com/ed-donner/agents  

> **Privacy note:** The fork is **public**. Making a fork of a public course repo private disables it on free GitHub accounts. `1_foundations/twin/` includes personal files (resume / LinkedIn PDF). If that is a concern, remove those files from git history before sharing the URL, or copy them only via a separate private repo / cloud drive.

| Remote    | URL                                      | Role                          |
|-----------|------------------------------------------|-------------------------------|
| `origin`  | `https://github.com/vinayak1998/agents`  | Your fork — push here         |
| `upstream`| `https://github.com/ed-donner/agents`    | Course repo — pull updates    |

Personal progress branch: **`my-progress`** (do lab work here, not on `main`).

---

## 1. Set up the new laptop

### Prerequisites

- Git
- [GitHub CLI](https://cli.github.com/) (`gh`) or HTTPS credentials for GitHub
- Python / uv / whatever the course uses (see course README after clone)

### Clone your fork and restore remotes

```bash
# Sign in (once)
gh auth login

# Clone YOUR fork (not the course repo)
git clone https://github.com/vinayak1998/agents.git
cd agents

# Add the course repo as upstream
git remote add upstream https://github.com/ed-donner/agents.git

# Confirm remotes look like the table above
git remote -v

# Check out your work
git checkout my-progress
```

You should now have the same lab notebooks and `1_foundations/twin/` files you left on the company laptop.

### Optional: verify remotes match this layout

```bash
git remote -v
# origin    → vinayak1998/agents   (fetch + push)
# upstream  → ed-donner/agents     (fetch + push)
```

If you accidentally cloned `ed-donner/agents` instead:

```bash
git remote rename origin upstream
git remote add origin https://github.com/vinayak1998/agents.git
git fetch origin
git checkout my-progress
```

---

## 2. Day-to-day workflow

```bash
# Always work on your personal branch
git checkout my-progress

# After finishing a lab session
git add .
git commit -m "Describe what you finished"
git push origin my-progress
```

Keep `main` as a clean mirror of the course. Merge course updates *into* `my-progress` (next section) — don’t commit lab work on `main`.

---

## 3. Stay in sync with course updates

Run this whenever the instructor pushes new material:

```bash
# Fetch latest from the course
git fetch upstream

# Update local main to match the course
git checkout main
git merge upstream/main

# Optional: keep your fork's main updated too
git push origin main

# Bring course updates into your work branch
git checkout my-progress
git merge main

# Push the merged branch
git push origin my-progress
```

### If `git merge main` has conflicts

1. Open the conflicted files (often notebooks).
2. Keep *your* completed cells and take *new* cells/files from the course.
3. Then:

```bash
git add .
git commit -m "Merge course updates into my-progress"
git push origin my-progress
```

Notebooks conflict awkwardly; if a merge is messy, compare side-by-side in the IDE and prefer your executed work plus any new course cells.

### Alternative: rebase (cleaner history, rewrite local commits)

Only if you’re comfortable with rebase and nobody else uses `my-progress`:

```bash
git checkout my-progress
git fetch upstream
git rebase upstream/main
git push --force-with-lease origin my-progress
```

Prefer **merge** unless you know you want rebase.

---

## 4. Quick reference

| Goal                         | Commands                                              |
|-----------------------------|--------------------------------------------------------|
| Continue labs               | `git checkout my-progress`                             |
| Save work                   | `git add . && git commit -m "..." && git push`         |
| Pull course updates         | `fetch upstream` → update `main` → `merge` into branch |
| See what’s new upstream     | `git fetch upstream && git log main..upstream/main`    |

---

## 5. Notes

- The fork stays **public** (required for forks of public course repos on free GitHub). Treat twin PDFs as public unless you remove them.
- Do **not** open a PR of `my-progress` into `ed-donner/agents` unless you intentionally want to contribute back (and strip personal files first).
- On the old laptop, after migration you can delete the local clone; the source of truth is the fork on GitHub.
