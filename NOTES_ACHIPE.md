1, fFor this project, I'd choose feature-branch workflow. Compared to trunk-based development, our team is small and not shipping multiple features simultaneously, so we don't need the discipline of constant integration into a single branch. Compared to Gitflow, we don't need the overhead of multiple long-lived branches (develop, release, hotfix) — that's built for larger teams with scheduled releases. Feature-branch workflow keeps main as the only long-lived branch, which fits a small team well.


Question2: 
* fix: add search
* docs: update notes
* feat: add team member search across name, role, department, and location
* chore: create .gitignore


question3: 
A scenario: a colleague pushes a commit, and afterward we realize the message or content isn't clean, so we're tempted to rebase to fix it. But if another colleague has already pulled that branch to base their own work on it, rebasing rewrites the commit history (new SHAs), causing their local branch to diverge from the rewritten one. When they pull again, they'll hit conflicting/duplicate commits, or Git will refuse to fast-forward. The rule of thumb: never rebase a branch that others have already pulled or built on — use merge instead, since it preserves history and is safe to share.


Personal question from this assignment:
1. How do you give permission to a collaborator ?
