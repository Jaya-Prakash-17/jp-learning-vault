# Chapter: Version Control (Git, GitHub, GitLab)

## 1. Overview
Imagine five architects trying to draw the blueprints for a skyscraper on the exact same piece of paper at the exact same time. They would constantly erase each other's lines, draw over each other, and ruin the master design. They need a system where each architect can trace a copy of the blueprint, work on their section privately, and then flawlessly merge their additions back into the master copy.

In software engineering, **Version Control** is that system. It allows hundreds of developers to work on millions of lines of code simultaneously without overwriting each other. It acts as an immortal timeline of the codebase: if a new feature breaks the production server at 3:00 AM, engineers can instantly "time travel" the code back to the exact state it was in at 2:59 AM. The industry standard tool for this is **Git**.

## 2. Why This Exists
Historically, before Git became the standard, code collaboration was terrifying.

**The Pre-Git Era (Zip Files & SVN):**
1. **The Zip File Nightmare:** Developers literally zipped up their codebase (`project_v1.zip`, `project_final_v2.zip`, `project_actually_final.zip`) and emailed it to each other. Merging two developers' work meant manually opening two text files and copy-pasting lines.
2. **Centralized Version Control (SVN/CVS):** Tools like Subversion emerged, but they were *centralized*. There was one master server holding the history. If the server went down, nobody could work. If you lost internet connection, you couldn't save your versions.
3. **Branching was Expensive:** In older systems, creating an experimental "branch" meant literally copying the entire project folder on the hard drive, making it painfully slow.

**The Git Revolution:**
Linus Torvalds (the creator of Linux) was frustrated with these tools and built Git in 2005. He made it **Distributed**. Every single developer downloads the *entire* repository history to their local laptop. You can branch, commit, and time-travel offline.

## 3. Real World Analogy
**The Multi-Verse Timeline**

Git is like a science-fiction multi-verse. 
- The "Main" branch is the prime timeline (Production). 
- When you want to build a new feature, you create a "Branch." This literally splits reality, creating an alternate universe where you can break things without affecting the prime timeline.
- A "Commit" is a save-state snapshot of your universe.
- When your feature is perfect, you execute a "Merge," which permanently fuses your alternate universe back into the prime timeline.

## 4. Technical Definition
**Git** is a free, open-source Distributed Version Control System (DVCS) designed to handle everything from small to massive projects with speed and efficiency.
Under the hood, Git is a **Directed Acyclic Graph (DAG)** of commit objects, tracked via cryptographic SHA-1 hashes.

## 5. Internal Working (The Three Trees)
Git relies on a three-stage architecture locally on your laptop:

1. **The Working Directory:** The actual files you see and edit in your IDE (like VS Code).
2. **The Staging Area (Index):** A middle-ground buffer. When you finish editing 10 files, you might only want to bundle 3 of them into your next save-state. You `git add` those 3 files to the Staging Area.
3. **The Local Repository (.git directory):** When you run `git commit`, Git takes everything in the Staging Area, compresses it into a snapshot, assigns it a 40-character SHA-1 hash, and permanently stores it in the local database.

## 6. Architecture (Git vs GitHub vs GitLab)

A massive point of confusion for juniors is thinking Git and GitHub are the same thing. They are not.

```mermaid
flowchart LR
    subgraph Developer Laptop [Local Machine (Git)]
        Working[Working Directory]
        Staging[Staging Area]
        LocalRepo[Local Repository]
        Working -- "git add" --> Staging
        Staging -- "git commit" --> LocalRepo
    end

    subgraph Cloud [Remote Hosting (GitHub / GitLab)]
        RemoteRepo[Remote Repository\n(The Source of Truth)]
        CI[CI/CD Pipelines\n(Automated Testing)]
    end

    LocalRepo -- "git push" --> RemoteRepo
    RemoteRepo -- "git pull" --> LocalRepo
```

### Component Breakdown:
- **Git:** The raw engine. The command-line tool installed on your laptop.
- **GitHub:** A cloud website (owned by Microsoft) that hosts a "Remote" copy of your Git repository so developers can share code. Famous for massive open-source collaboration and Pull Requests.
- **GitLab:** A competing cloud/on-premise platform. Highly favored in Healthcare and Enterprise because companies can host it entirely on their own private servers, ensuring PHI never touches public clouds. Famous for its natively integrated CI/CD pipelines.

## 7. Lifecycle (The Daily Workflow)

1. **Clone (`git clone`):** Download the remote repository from GitLab to your laptop.
2. **Branch (`git checkout -b feature-login`):** Create your isolated alternate universe.
3. **Modify:** Write your integration code in your IDE.
4. **Stage (`git add .`):** Tell Git to prepare all modified files.
5. **Commit (`git commit -m "feat: added login"`):** Create the local save-state snapshot.
6. **Push (`git push origin feature-login`):** Upload your alternate universe to the GitLab server.
7. **Pull Request (PR) / Merge Request (MR):** You ask the Senior Engineers on GitLab to review your code.
8. **Merge:** Once approved, your code is fused into the `main` production branch.

## 8. Production Example

**Context:** Edifecs MapBuilder Collaboration

At an insurance company, five Integration Engineers are working on the massive 837 Claims MapBuilder logic.
Engineer A is adding logic for Institutional Claims (837I). Engineer B is adding logic for Professional Claims (837P).

If they used a shared network drive, Engineer B would overwrite Engineer A's `.map` file.
Instead, they use GitLab. 
- Engineer A branches to `feat/837I-mapping`.
- Engineer B branches to `feat/837P-mapping`.
Both modify the same master map file on their local laptops. When they push to GitLab and open Merge Requests, GitLab detects they edited the same file. It prompts the Lead Engineer to perform a **Merge Conflict Resolution**, explicitly deciding which lines of Engineer A's logic and Engineer B's logic to keep, seamlessly blending both features into production without data loss.

## 9. Code Examples

### The "Oops" Workflow (Fixing Mistakes)

```bash
# Scenario: You committed a file, but realized you forgot to add a small typo fix.
# Instead of making an ugly "fixed typo" commit, you amend the previous one.
git add fix.groovy
git commit --amend --no-edit

# Scenario: You are working on a feature, but a P1 production bug fires.
# You need to switch to the main branch instantly, but your current work is half-finished.
git stash        # Temporarily shelves your uncommitted changes
git checkout main
# ... fix the bug, commit, and push ...
git checkout feature-branch
git stash pop    # Brings your half-finished work back
```

## 10. Best Practices

1. **Write Semantic Commit Messages:** A commit message should explain *why* a change was made, not just *what* changed. Use prefixes like `feat:` (new feature), `fix:` (bug fix), or `chore:` (updating dependencies). E.g., `fix: added If-Exists logic to NM1 map to prevent NPE`.
2. **Commit Often, Push Often:** A commit is a save point. If you write code for 8 hours without committing, and your laptop crashes, you lose 8 hours of work.
3. **Never Push Directly to Main:** The `main` branch should be strictly protected. All code must go through a Pull Request/Merge Request so another human can review it before it reaches production.

## 11. Common Mistakes

1. **Committing Secrets/PHI:** The absolute worst mistake a junior can make is accidentally committing an AWS API key or a file containing Protected Health Information (PHI) to Git. Because Git is an immortal history tracker, simply deleting the file in the next commit doesn't work—hackers can just look at the previous commit to steal the key.
2. **Merge vs Rebase Confusion:** When updating your branch with the latest production code, `git merge main` creates a messy, diamond-shaped history graph. `git rebase main` rewrites your local history to make it look like you wrote your code sequentially *after* the latest production updates, creating a perfectly clean, linear history.
3. **Detached HEAD State:** When you use `git checkout <commit_hash>` to look at an old version of code, you are in a "Detached HEAD" state. If you start making new commits here without creating a new branch, those commits will become orphaned and eventually garbage-collected (deleted forever) by Git.

## 12. Troubleshooting

**Symptom 1: You try to `git push`, but Git rejects it saying "Updates were rejected because the remote contains work that you do not have locally."**
- *Root Cause:* A colleague pushed new code to the remote branch while you were working offline. Git refuses to let you overwrite their work.
- *Solution:* Run `git pull --rebase` to download their changes and neatly stack your new local commits on top of theirs, then run `git push`.

**Symptom 2: You accidentally did a bad `git rebase` and deleted 5 of your own commits.**
- *Root Cause:* Rebasing rewrites history. If you mess it up, normal Git commands can't see the old history.
- *Solution:* The lifesaver command is `git reflog`. It is a secret journal that tracks every single move your HEAD pointer makes, even deleted commits. You find the hash before your mistake and run `git reset --hard <hash>`.

## 13. Interview Questions

### Easy
**Q: What is the difference between Git and GitHub?**
> A: Git is the local, command-line version control engine installed on my machine. GitHub is a cloud-based hosting platform that stores remote copies of Git repositories and provides a web UI for collaboration and Pull Requests.

### Medium
**Q: Explain the difference between `git merge` and `git rebase`.**
> A: Both integrate changes from one branch into another. `git merge` creates a new "merge commit" that ties the two branch histories together, preserving the exact chronological history but making the graph messy. `git rebase` temporarily removes your feature commits, pulls the latest target branch, and replays your commits directly on top, creating a clean, linear history without extra merge commits.

### Hard
**Q: What is a `git cherry-pick` and when would you use it?**
> A: `cherry-pick` allows you to select a specific, single commit from an entirely different branch and apply it to your current branch without merging the rest of that branch's history. I would use this if a colleague fixed a critical pipeline bug on their experimental branch, and I need *only* that bug fix in my branch right now.

### Scenario-Based
**Q: A junior developer accidentally committed a test payload file containing real Patient PHI to the shared remote repository. They realized the mistake, ran `git rm patient_data.txt`, and pushed the new commit. Does this fix the HIPAA violation? How do you actually solve this?**
> A: No, that does not fix it. Git retains full history. Anyone pulling the repository can easily run `git checkout HEAD~1` and view the PHI. This is a massive security incident. 
> To solve this, I must rewrite the repository's deep history. I would use a tool like the `BFG Repo-Cleaner` or `git filter-branch --tree-filter 'rm -f patient_data.txt' HEAD` to completely purge the file from every single commit in the DAG. After purging it locally, I must run a highly dangerous `git push origin branch --force`. Finally, because I rewrote history, I must instruct all other developers to delete their local repositories and re-clone, otherwise they will re-introduce the PHI the next time they push.

## 14. Comparison Table

| Feature | SVN (Subversion) | Git |
| :--- | :--- | :--- |
| **Architecture** | Centralized (Single point of failure). | Distributed (Every dev has a full backup). |
| **Offline Work** | Impossible (Cannot commit offline). | Full support (Commit locally anytime). |
| **Branching** | Slow and heavy (Copies the directory). | Instant and lightweight (Pointer manipulation). |
| **Speed** | Slow (Requires network calls for history). | Blazing fast (Reads local disk). |
| **Industry Adoption** | Legacy systems only. | The absolute industry standard (99%+). |

## 15. Advanced Concepts

- **Git Hooks:** Scripts that run automatically before or after a Git command. A pre-commit hook can run a linter or a regex scanner to block a developer from committing code if it contains the word "password" or a 9-digit SSN.
- **Git Bisect:** A powerful debugging tool. If a bug was introduced sometime in the last 100 commits, `git bisect` uses a binary search algorithm to automatically checkout commits halfway through the history, asking you "Is it broken here?" to find the exact commit that caused the bug in $\log_2(N)$ steps.

## 16. Revision Cheat Sheet

*   **Git:** Local engine. **GitHub/GitLab:** Remote cloud hosts.
*   **The Three Trees:** Working Directory $\rightarrow$ `git add` $\rightarrow$ Staging Area $\rightarrow$ `git commit` $\rightarrow$ Local Repo.
*   **Merge vs Rebase:** Merge preserves exact history (messy graph). Rebase replays commits (clean linear graph).
*   **The Golden Rule of Rebase:** Never rebase a public branch that other people are working on, because you rewrite the history they rely on.
*   **PHI Leaks:** Deleting in a new commit is not enough. You must rewrite history using `git filter-branch` and force push.
*   **Reflog:** The ultimate undo button. Tracks history of your HEAD movements.
*   **Stash:** Temporarily shelves uncommitted work.

## 17. References
- [Pro Git (The Official Book - Free Online)](https://git-scm.com/book/en/v2)
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials)
- [GitHub Documentation: Removing sensitive data from a repository](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)
