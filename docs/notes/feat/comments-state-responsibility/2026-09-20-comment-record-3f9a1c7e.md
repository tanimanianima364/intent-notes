---
covers:
  - .claude-plugin/marketplace.json
  - .claude-plugin/plugin.json
  - .codex-plugin/plugin.json
  - README.md
  - core/gate.mjs
  - core/instructions.md
  - package.json
  - skills/intent-notes/SKILL.md
  - tests/gate.test.mjs
---

# Comments state responsibility; notes are short and filed under the branch

## What this change was for

The docstring record had two jobs — what a thing is for, and why it works that way — and the second overlapped the note, pulling docstrings toward mechanics that rot. The record on the code is now a comment stating responsibility only, two or three sentences for a file and for each function. Notes are filed under `docs/notes/<branch>/` and kept to a few sentences per section.

## The approach, and what it rejected

Approach and rejected alternatives stay in the note, where they are dated and immutable; a comment that repeats them is the copy that drifts. The branch directory replaces the random hex as what keeps two branches apart; the date prefix stays because the reader sorts notes by file name. Rejected: dropping the code-level record, since without the hook a reader opening a file has no pointer to its purpose. Rejected: enforcing either length cap in the hook, which cannot see comments at all and would reintroduce the gate this design removed.

## How it is built

Wording only: the injected instructions, the skill, the README, the reminder string in `core/gate.mjs`, and the four manifests. The test pins the `## Comments` heading, the absence of `docstring`, and the branch-directory path. `core/notes.mjs` already walks subdirectories; a note's id is still its file name, so a date-and-slug must not repeat across branches. Refines `2026-09-13-intent-records-5966e5e4` rather than superseding it.
