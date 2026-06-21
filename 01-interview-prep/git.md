# Git, GitHub, and GitLab

## 1. Architecture & The Need
- **The Need**: Multiple engineers working on the same codebase simultaneously will overwrite each other's code without a tracking system.
- **Architecture**: A distributed Directed Acyclic Graph (DAG) of commits. Every developer has a full copy of the entire repository history locally.

## 2. Core Concepts: Git vs GitHub vs GitLab
- **Git**: The actual local engine and command-line tool. It runs on your laptop and tracks the history of your files offline.
- **GitHub**: A cloud hosting service owned by Microsoft. It holds the "remote" copy of your Git repo. Famous for massive open-source collaboration, Pull Requests (PRs), and GitHub Actions.
- **GitLab**: A competing cloud hosting service that focuses heavily on Enterprise. Its major differentiator is best-in-class, natively built-in CI/CD pipelines (`.gitlab-ci.yml`), and it can be self-hosted on a company's private servers.

## 3. Basic Daily Usage (Must-Know Commands)
- `git clone <url>`: Download the remote repo to your machine.
- `git status`: Check which files you have modified.
- `git add .`: Stage all modified files for the next commit.
- `git commit -m "fix: updated mapping logic"`: Wrap your staged changes into a commit node.
- `git push`: Upload your local commits to GitHub/GitLab.
- `git pull`: Download and merge the latest remote commits to your local machine.

## 4. Advanced Commands & Usage
- `git rebase -i HEAD~3`: Interactive rebase. Allows you to squash, edit, or delete the last 3 commits to clean up history before pushing a PR.
- `git cherry-pick <commit_hash>`: Grab a specific commit from another branch and apply it to your current branch without merging the whole history.
- `git reflog`: The emergency undo button. It tracks every move you make, allowing you to recover commits you accidentally deleted during a bad rebase.
- `git filter-branch` (or `git filter-repo`): Rewrite the entire repository history to permanently delete a file.

---

## Interview Question Deep Dive

### Q: "You accidentally committed a file containing PHI (Protected Health Information) to a shared remote branch. How do you remove it completely?"

**30-Second Answer**: A simple `git rm` and new commit is not enough because the PHI will still exist in the Git history. I must rewrite the repository history using `git filter-branch` or the `BFG Repo-Cleaner` to purge the file entirely, and then coordinate with the team to force push the clean history.

**2-Minute Answer**: Because HIPAA regulations are incredibly strict, pushing PHI to a remote repository is a major incident. If I just do `git rm patient_data.xml` and commit, anyone can still run `git checkout HEAD~1` and view the PHI. 

I have to rewrite the Git tree. I would use `git filter-branch --tree-filter 'rm -f patient_data.xml' HEAD`. This traverses every commit in history and deletes the file as if it never existed. Once the local history is clean, I must run `git push origin branch_name --force`. 

**Deep Dive Answer**: The technical fix is easy; the team coordination is the hard part. Because I force-pushed a rewritten history, the remote branch and my colleagues' local branches have diverged. If a colleague simply runs `git pull`, Git will try to merge their local history (which still contains the PHI) back into the remote, re-introducing the data leak. I must instruct every developer to delete their local branch and fetch a fresh copy from the remote.

**Real Example**: During integration deployments at Edifecs, we strictly parameterized all payloads. But when a bad profile configuration *was* merged and broke the staging environment, I used `git revert <commit_hash>` to safely create a new commit that undid the bad changes, rather than rewriting history, ensuring the team's workflow wasn't disrupted.

**Follow-up Questions**:
- *Interviewer*: "What is the difference between git merge and git rebase?" (Answer: Merge creates a new commit joining two histories. Rebase rewrites history by placing your feature branch commits directly on top of the main branch, creating a clean, linear history).
