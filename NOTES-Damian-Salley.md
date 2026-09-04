# Damian Salley - Assignment 1.3 Notes

## Part 1 - Written Decisions

### Question 1 - Workflow Choice

I would choose the feature-branch workflow because each person works on their own separate branch and then creates a pull request to merge their changes into `main`. This allows everyone in the group to work in parallel without directly changing "main"

Gitflow would be unnecessarily complicated because there would be multiple branches for different jobs, such as development and releases, which we do not really need for this small, short sprint.

Trunk based could work because our changes are small and short-lived, but I would rather use feature branches because each person's work stays separate and can be reviewed in a pull request before being merged into "main".

### Question 2 - Conventional Commits

Five commits from my previous assignments can be reclassified as:

1. "Add README application description"
   - "docs: add README application description"
   - This is a documentation change because it updates the README.

2. "Display team member count"
   - "feat: display team member count"
   - This adds new functionality to the application.

3. "Resolve README merge conflict"
   - "chore: resolve README merge conflict"
   - This was mainly repository maintenance because I was resolving a Git conflict rather than fixing application behaviour.

4. "Add repository verification workflow"
   - "chore: add repository verification workflow"
   - This adds repository and development tooling rather than functionality for the user.

5. "Restore required notes file"
   - "chore: restore required notes file"
   - This restored a required repository file so that the verification process could work correctly.

The commit that does not map completely cleanly to one type is "Resolve README merge conflict". It could also be seen as documentation-related because the conflict happened in the README, but the main purpose of the commit was resolving a repository conflict. This shows that commit messages should describe one clear purpose where possible.

### Question 3 - Rebase Risk

A problem could happen if I push a branch, another teammate fetches or pulls that branch, and I then rebase the branch and force-push it without telling them.

Rebasing rewrites the commit history and creates new commit hashes. My teammate would still have the old commits locally, while the remote branch would contain the rewritten commits. Their local branch would therefore diverge from the remote branch.

I should communicate with the teammate before rebasing shared work and avoid rewriting a branch while somebody else is using it. If the teammate has no unique local work after this happens, they could fetch the latest remote history and reset their branch to match the remote branch.

### Question 4 - Repository Rules

I would require pull requests before merging into "main", require one approval, require the CI status checks to pass, disallow force-pushes to "main", and require CODEOWNERS review where it applies.

Pull requests and reviews help prevent unreviewed work from going directly into `main`. Required status checks prevent broken changes from being merged. Force-pushes should be disabled because they can rewrite shared history.

I would require only one approval because the group is small. Requiring two approvals could slow down the sprint if one team member is unavailable. One approval gives us review protection without making the workflow too difficult for a small group.