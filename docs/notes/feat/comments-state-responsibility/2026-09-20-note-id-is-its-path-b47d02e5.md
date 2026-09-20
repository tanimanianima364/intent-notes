---
covers:
  - core/instructions.md
  - core/notes.mjs
  - skills/intent-notes/SKILL.md
  - tests/covering.test.mjs
---

# A note's id is its path under docs/notes, so same-named notes on two branches stay apart

## What this change was for

Review reproduced the failure: two branches each filed `2026-09-20-retry-policy.md` under their own directory, merged cleanly, and a note superseding the HTTP one reported the database one replaced as well. The id was the bare file name, and a rule asking authors not to repeat a name cannot be kept by branches that cannot see each other.

## The approach, and what it rejected

The id is the note's path relative to `docs/notes` without `.md`, and a `supersedes` entry matches it exactly. A flat note keeps the id it always had, so every existing reference still resolves. Rejected: falling back to a bare file name when it is unique across directories — resolution would then change when an unrelated branch adds a note, which is the same fault arriving later. A reference that matches nothing marks nothing superseded, which is the safe side.

## How it is built

One function derives the id from the note's path; the map from superseded id to superseding file is unchanged. One test files two same-named notes under different directories and supersedes one of them; another checks that a bare name does not reach a nested note.
