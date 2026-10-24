---
name: cleanup
description: Review the changed code for reuse, simplification, efficiency and altitude (root-cause depth) issues, then apply the fixes without changing behavior. Quality only; it does not hunt for bugs. Use it when the user asks to clean up, simplify, tidy or polish a diff, branch, PR or file before review or merge.
---

# cleanup

Improve the quality of the changed code. Do not hunt for correctness bugs; that is a separate code review. Keep behavior the same.

## Phase 0: get the diff

- The user may name a target: a PR number, a branch or a file path. If so, review that.
- Otherwise run `git diff @{upstream}...HEAD`. With no upstream, use `git diff main...HEAD` (or the repo's default branch), or `git diff HEAD~1`.
- If the range diff is empty or there are uncommitted changes, also run `git diff HEAD` and include the working tree. Cleanup often runs before the commit.
- The diff is the scope. Read the surrounding code as needed, but change code outside the diff only when a fix requires it.

## Phase 1: review four angles

If your agent can run subagents in parallel, start four at once, one per angle, and give each the diff and its angle. If it cannot, work through all four angles yourself, one after another. Never skip an angle.

Each finding has:

- `file` and `line`
- a one-line summary
- the concrete cost: what is duplicated, wasted or harder to maintain

### Reuse

- Flag new code that re-implements something the codebase already has.
- Search shared and utility modules and the files next to the change.
- Name the existing helper to call instead.

### Simplification

- Flag complexity the diff adds: state that is redundant or can be derived, copy-paste with small changes, deep nesting, dead code left behind.
- Name the simpler form that does the same job.

### Efficiency

- Flag wasted work the diff adds: repeated computation or I/O, independent operations run one after another, blocking work on startup or hot paths.
- Flag long-lived objects built from closures. They keep the whole enclosing scope alive, which leaks memory when that scope holds large values. Prefer a class or struct that copies only the fields it needs.
- Name the cheaper alternative.

### Altitude

- Check that each change fixes the root cause at the right depth, not a symptom with a fragile patch.
- Special cases added to shared infrastructure mean the fix is not deep enough.
- Prefer one simpler, more general change to the underlying mechanism, and name it.

## Phase 2: apply the fixes

- Wait for all four angles. Merge findings that point at the same line or mechanism.
- Fix each remaining finding directly in the code.
- Skip a finding when its fix would change intended behavior, needs changes far outside the diff, or is a false positive. Note the skip; do not argue with it.
- Run the project's checks (typecheck, lint, tests for the touched files) after the fixes, if the project has them.
- End with a short summary: what was fixed and what was skipped and why, or that the code was already clean.
- If you did the angles yourself instead of in parallel subagents, say so in the summary.
