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
2. What is th flow to do a pull request


Assignment 2.1 - Agile Fundamentals & Project Framing
=============================

Question 1

For a personal app like my Daily App, solo, worked on in short sessions, with scope I'm still figuring out, I'd use Kanban rather than Scrum. Scrum relies on committing to fixed-length sprints, but as a solo developer with irregular time and evolving requirements, I can't reliably estimate or commit to two weeks of planned work, especially when some features might change once I actually use the app. Kanban's continuous flow lets me pull the next most valuable task whenever I have time, re-prioritize instantly as I learn more, and skip ceremonies (sprint planning, standups, retros) that only add value when there's a team to coordinate.

For TrackFlow, the shared class project, I'd choose Scrum instead, and this is a genuine difference, not just preference. With a team and a shared deadline, the constraints that made Scrum a poor fit for solo work disappear: fixed sprints give the group a common rhythm, sprint reviews create checkpoints to catch misalignment early, and clear roles and ceremonies make ownership explicit, all of which matter far more with multiple people. Kanban's flexibility, which was an asset solo, becomes a risk in a team, since without sprint boundaries it's harder to know if everyone's on track for the deadline.

Question 2

The two values in tension are "early and continuous delivery of valuable software" and "working software as the primary measure of progress" (Value 1 / Principle 7) versus "trust motivated individuals" and "simplicity, maximizing the work not done" (Principle 5 / simplicity value).

The real decision: when building the shopping list/reminder part of my Daily App, do I build a full-featured list (categorized items, quantities, mark-as-bought, maybe pantry tracking) to deliver more visible value early? Or do I build the minimum, a flat, uncategorized list, and defer complexity until I know it's actually needed?

I'd lean toward simplicity: build the flat list first. As a solo developer with evolving scope, investing in structure before I know I need it risks wasted effort. The flat version still ships working software fast; I'm not sacrificing delivery speed, just deferring complexity until real usage tells me it's worth building.

Question 3

Critique of TaskBoard Pro (at least three problems):

Full spec sign off before any building begins violates "responding to change over following a plan" and Principle 2 ("welcome changing requirements, even late in development"). Locking the spec in Phase 1 and banning changes once design starts assumes you can know everything upfront, which Agile explicitly rejects.
No demos until the build phase is fully complete violates "working software over comprehensive documentation" and Principle 1 (satisfying the customer through early and continuous delivery) plus Principle 7 (working software as the primary measure of progress). Nine weeks of building with zero visibility means nobody can course correct if something's wrong.
One giant QA pass across all features simultaneously (Phase 4) means bugs and misunderstandings compound for nine weeks before anyone tests anything, the opposite of iterative, continuous delivery. Testing this late massively increases risk and rework.
Launch to all users at once (Phase 5) is a single big bang release with no earlier customer feedback loop, violating "customer collaboration over contract negotiation." There's no chance to learn from real users before everyone is exposed to whatever went wrong.

Agile redesign, first two iterations, for my meal planner/shopping list app:

Iteration 1 (Week 1 to 2): Build the smallest working version, a simple weekly view where I fill in what I'm cooking each day, plus a flat, uncategorized shopping list I fill in manually. No reminders yet, no categorization. Ship it, use it for real that week, see what's missing.

Iteration 2 (Week 3 to 4): Based on actually living with Iteration 1, add whatever proved genuinely necessary, likely a reminder or notification for shopping day, and maybe basic list persistence week to week (carrying over unbought items). Skip anything I didn't miss in practice.