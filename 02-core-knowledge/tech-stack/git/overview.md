# Git Overview

## Definition
Git is a distributed Version Control System (VCS) that tracks changes in source code over time. 

## Why it exists
To prevent the "Final_Final_v2_USE_THIS_ONE" folder structure. It allows multiple developers to work on the exact same codebase simultaneously without overwriting each other's work, providing a complete, auditable history of who changed what, when, and why.

## Commands
- `git clone <url>`: Download a repository to your local machine.
- `git status`: See what files are modified or untracked.
- `git add .`: Move all changes into the Staging Area.
- `git commit -m "msg"`: Save the staged changes as a node in the history tree.
- `git push origin main`: Upload local commits to the remote server (GitHub/GitLab).
- `git pull`: Fetch remote changes and merge them into your local branch.
- `git rebase -i HEAD~3`: Interactively squash or edit the last 3 commits.
- `git cherry-pick <hash>`: Pull a specific commit from another branch into yours.

## Architecture
- **Distributed DAG**: Every developer has a full copy of the entire repository locally. Commits form a Directed Acyclic Graph.
- **The Three States**:
  1. **Working Directory**: Your actual files on disk.
  2. **Staging Area (Index)**: Files marked to go into the next commit.
  3. **Local Repository (HEAD)**: The committed history.
- **Git vs GitHub/GitLab**: Git is the local CLI engine. GitHub is Microsoft's public cloud hosting. GitLab is a competitor heavily focused on built-in CI/CD pipelines.

## Interview Questions
**Q: "What is the difference between git merge and git rebase?"**
*Answer*: `git merge` takes two branches and ties them together with a new "merge commit," preserving the exact historical timeline but creating a messy graph. `git rebase` rewrites history by picking up your feature branch and placing it directly on top of the `main` branch, resulting in a perfectly clean, linear history.

**Q: "You committed PHI (Protected Health Information) to a remote branch. How do you remove it?"**
*Answer*: I cannot just delete the file and commit again; the PHI is still in the history. I must rewrite the repository history using `git filter-branch` or `BFG Repo-Cleaner` to purge it completely, and then force push (`git push -f`).

## Cheat Sheet
| Task | Command |
| :--- | :--- |
| Undo last commit (keep files) | `git reset --soft HEAD~1` |
| Undo last commit (destroy files) | `git reset --hard HEAD~1` |
| Save work without committing | `git stash` |
| Bring back stashed work | `git stash pop` |
| The "Undo" for bad rebases | `git reflog` |
