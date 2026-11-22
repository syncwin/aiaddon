# Agent factory workflow (plugin and skill changes)

Use when an agent (or several) builds or changes a plugin or skill and a human stays in charge. Brand agnostic: works with any agent, repo host, and CI.

## Steps

1. **Issue first.** Every change starts as a written issue: the problem in plain words plus acceptance criteria, each one checkable (a pass or a fail, never "better").
2. **Tests first.** Before editing, write or name the proof for each criterion: an eval case, a router case, or a validator check. The gate only knows what the tests know; a criterion with no test is not done. Never delete or weaken an existing test.
3. **Own worktree and branch.** The agent works in its own worktree on its own branch, makes the smallest change that meets the criteria, and opens a pull request that links the issue.
4. **CI runs.** Validator, selftest, router check, secret scan and evals. A failure goes back to the agent with the output. Bounded tries (two or three); then stop and report what failed and what was tried. No retry loops.
5. **Merge gate checklist.** All of: checks passed (none skipped or NOT RUN), review approved, and the diff matches the issue's scope (nothing extra).
6. **Human review on every pull request.** The requester is not the approver; a second person approves. No auto-merge without review.
7. **Holdout cases (optional, larger work).** Keep a few eval cases the building agent never sees; run them at review. A pass on visible cases with a holdout failure means the agent fitted the tests: send it back.
8. **Start small.** One agent, small well-described issues. Widen only after several clean reviewed pull requests. Never run a setup with no human review.

## Issue template

```
Problem: <what is wrong or missing, who is affected>
Acceptance criteria:
- <checkable statement>
Tests: <eval / validator check that proves each criterion>
Out of scope: <what must not change>
```
