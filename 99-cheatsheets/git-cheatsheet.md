# Git Cheat Sheet

### Core Concepts
- **Working Directory**: The actual files on your laptop.
- **Staging Area (Index)**: Files you've marked (`git add`) for the next commit.
- **Local Repo (HEAD)**: Your committed history.
- **DAG**: Directed Acyclic Graph. How Git structures history.

### Git vs Remote Hosts
- **Git**: Local CLI engine tracking the DAG.
- **GitHub**: Microsoft. Public/Open Source cloud hosting. PRs & Actions.
- **GitLab**: Enterprise. Built-in, native CI/CD pipelines.

### Daily Commands (Must Know)
| Command | Action |
| :--- | :--- |
| `git clone <url>` | Download remote repo. |
| `git status` | Show modified/untracked files. |
| `git add .` | Stage all changes. |
| `git commit -m "Msg"` | Save staged changes to history. |
| `git push / pull` | Upload to / Download from remote. |
| `git stash` | Save uncommitted work temporarily to switch branches. |

### Advanced History Rewriting
| Command | Action |
| :--- | :--- |
| `git rebase -i HEAD~3` | Interactively squash, edit, or delete the last 3 commits. |
| `git cherry-pick <hash>`| Grab one specific commit from another branch and apply it. |
| `git reflog` | The ultimate Undo. Recover "deleted" commits from bad rebases. |
| `git reset --soft HEAD~1`| Undo last commit, keep files staged. |
| `git reset --hard HEAD~1`| Undo last commit, destroy file changes entirely. |
| `git filter-branch` | Rewrite the entire history tree to permanently purge a file. |

### Interview Triggers
- 🚨 **"Merge vs Rebase"** ➡️ Trigger: Merge preserves exact historical timeline (messy graph). Rebase rewrites history to place your branch on top of main (clean linear graph).
- 🚨 **"Accidentally pushed PHI"** ➡️ Trigger: `git filter-branch` (or BFG Repo-Cleaner) to purge history. Force push. Instruct entire team to delete local branches and re-clone.
