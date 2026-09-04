## Question 1 — Choosing a workflow for this sprint

Since we are 4 people working on one small codebase over a
short sprint, we chose a feature-branch workflow rather than Gitflow or
trunk-based development, and the reason starts with what problem each
alternative is actually built to solve. Gitflow's separate `develop`,
`release`, and `hotfix` branches exist to manage multiple release lines in
parallel — something we don't have, since we're shipping once, from one
small repo, over a few days. Introducing that scaffolding would mean
coordinating extra branch types and merge steps for a problem that doesn't
exist in this project, at real cost to a sprint where every hour matters.
Trunk-based development sits at the other extreme: everyone commits
directly to `main`, or to branches so short-lived they're merged within
minutes, relying on strong CI and often feature flags to keep `main` always
shippable. That speed is appealing, but it only works safely with tooling
and discipline we don't have in place, and it directly conflicts with what
Part 3 asks us to configure — a required pull request and review before
anything reaches `main`. Trunk-based's entire premise is minimizing the
ceremony before a merge; branch protection's entire premise is adding a
checkpoint before one. The two don't fit together. Feature-branch is the
middle path that actually matches our constraints: each of us gets an
isolated branch to work on in parallel without stepping on each other's
changes, and the branch-into-pull-request-into-review-into-merge shape is
exactly the unit that GitHub's branch protection rules, our required CI
check, and our CODEOWNERS routing are all designed around. It's not the
workflow with the most structure or the least — it's the one sized to a
three-to-four person group with one short sprint and one shared codebase.

---

## Question 2 — Auditing your own history

Looking back at `git log --oneline`, five commits stand out as worth
reclassifying. `f573297`, "Added verification workflow," maps cleanly onto
`ci` — it's the commit that actually adds the `.github/workflows/verify.yml`
pipeline, so there's no ambiguity there. `38d719f`, "Add reviewer note to
README," is just as clean a fit for `docs` — a pure documentation edit with
no behavioural change behind it. `60e10d4`, "added status badge," sits
closer to the line: it's technically a README edit, which points to `docs`,
but the reason for making it was to surface CI status, which points to
`ci`. I don't think there's a wrong answer here so much as a real ambiguity,
and it's worth naming rather than papering over.

The commit that doesn't map cleanly onto any single type is `ab50530`,
"Temporarily renamed notes file," along with its paired follow-up,
`2caeb24`, "temporarily changed notes file now restored." Neither is really
product work in the sense `feat`, `fix`, `docs`, or `chore` assume — they're
a deliberate, throwaway action taken specifically to prove the CI check
fails and recovers, per the assignment's own "Proving It Changed" step. If I
had to force a label onto it, `test` is the closest stretch, but it's not a
comfortable fit either, and that discomfort is the point: Conventional
Commits is built around durable changes to a project, not verification steps
performed on the pipeline itself. A commit that resists a clean label here
is really telling me it's doing something categorically different from the
rest of the log, not that it's a badly scoped feature commit.

The fifth commit worth flagging is `aaeac44`, "reflection of assignment."
The type itself is a reasonable, if weak, fit for `docs`, but the real
problem is the message — it isn't imperative mood, and it doesn't say what
changed or where. That same vagueness shows up again in `8aa28ad`, "Updated
NOTES.md for assignment 1.2," and `656a59a`, "Updated NOTES.md." Three
separate commits sharing that exact weakness — naming the file touched
instead of describing the change inside it — suggests this wasn't a one-off
slip but a habit worth fixing before the next assignment.

---

## Question 3 — Where your group's rebase risk lives

The moment this risk shows up most concretely is scripted directly into
Part 3's Task 9 — one member creates a branch, a second member fetches or
pulls it, and the first member then rebases and force-pushes anyway. But the
same risk appears earlier and less deliberately in Task 7's cross-review
step: the moment a reviewer checks out someone's PR branch locally to
actually run it before approving, that branch now has a second person
depending on its current commit history, and if the author rebases and
force-pushes after that point — even just to tidy things up before
merging — the reviewer's local copy is left pointing at commits that no
longer exist on the remote.

What goes wrong follows directly from what rebase actually does: it
rewrites every commit's parent, which changes its SHA. The reviewer's local
branch still points at the old SHAs, so their next `git pull` doesn't
recognize the new rebased commits as the same work — it sees two unrelated
histories and tries to merge them, which typically reintroduces the
pre-rebase commits alongside the rebased ones, duplicating work and often
creating conflicts on lines that were already resolved once. If the
reviewer instead tries to push their own follow-up commits, that push gets
rejected outright, and if someone reaches for `--force` to clear the
rejection, it can clobber the author's rebased history entirely.

The right response isn't a recovery trick so much as a rule: never rebase a
branch once someone else has fetched or pulled it. Shared is the line where
rebase stops being safe and merge takes over. If a shared branch genuinely
needs cleanup, that has to start with communication — telling everyone with
a local copy before the history changes, not after — and only then should
they run `git fetch` followed by `git reset --hard origin/<branch>` to
realign, and only once they've confirmed they have no unique local commits
they'd lose in the process.

---

## Question 4 — Designing our group's rules, before configuring them



