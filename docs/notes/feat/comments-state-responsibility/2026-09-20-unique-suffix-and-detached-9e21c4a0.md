---
covers:
  - README.md
  - core/gate.mjs
  - core/instructions.md
  - skills/intent-notes/SKILL.md
  - tests/gate.test.mjs
---

# The hex suffix is back, and a detached HEAD files its notes under `detached`

## What this change was for

Review found two holes in the branch-directory rule. The directory separates branches, not notes: two notes on one branch, same day and slug, would collide, and two forks can carry the same branch name. And a detached HEAD has no branch name at all, while the change set already works there. This corrects the earlier note's claim that the branch directory replaces the hex.

## The approach, and what it rejected

The eight random hex characters return as the only thing that makes a name unique; the directory and the date are for organisation and order. A detached HEAD files under `detached`, with no commit id in the path: uniqueness no longer depends on where the note was written, and the commit is a fact git already keeps for the file. Rejected: a short content hash instead of random hex — it would have to be computed from a note that does not exist yet.

## How it is built

Wording in the instructions, the skill, and the README; the test now pins the suffix and the `detached` fallback. This branch's own notes were renamed to carry the suffix. The reminder string and the skill description were reworded from review at the same time: "leave comments", and comments that state responsibility rather than describe the change.
