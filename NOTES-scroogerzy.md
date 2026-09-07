## Assignment 1.3

### 1. Which rule mattered most, in practice

The branch protection rule requiring pull requests and approvals mattered most. It prevented direct changes from being pushed to `main` and ensured that changes were reviewed before being merged. We also experienced this rule directly when a direct push to `main` was rejected.

### 2. The conflict, from the inside

I was directly involved in the Task 8 conflict. My teammate and I edited the exact same line in `README.md` differently on separate branches. When we merged the branches, Git reported a content conflict. We inspected both versions, discussed which wording was clearer, and resolved the conflict together. The final merge commit preserved the genuine divergent history from both branches.

### 3. The rebase recovery

I was involved in the Task 9 rebase demonstration as Member A. After Member B had fetched my branch, I rebased my branch onto a new base, which rewrote the commit history. I then used `git push --force-with-lease`, which changed the remote branch history. When Member B fetched the updated branch, Git reported that the local branch and remote branch had diverged. Since Member B had no unique work to preserve, the branch was recovered using `git reset --hard origin/rebase/member-a`. This showed how a force-push after a rebase can disrupt another developer's local branch and why communication is important before rewriting shared history.

### 4. What I would change about our group's rules

I would keep the pull-request and approval requirements because they prevented direct changes to `main` and encouraged review. I would also make the team's rule against rebasing shared branches more explicit. The Task 9 demonstration showed that rewriting history and force-pushing can cause another developer's local branch to diverge unexpectedly. For shared branches, I would prefer communicating first and using `--force-with-lease` only when rewriting history is necessary.
