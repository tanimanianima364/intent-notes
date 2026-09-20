---
name: intent-notes
description: Record why the current change was made — a note under docs/notes plus the comments stating what each changed file and function is responsible for. Use when the user asks to account for a current change, to write the note for it, or explicitly requests intent notes.
---

# Intent Notes

Record the change this branch has made. The change is everything this branch has done that its base has not — committed and uncommitted alike. Print it by running the exact change set command the active Intent Notes session instructions supply, which runs the same code the hook runs. Do not write a `git diff` of your own instead: resolving the base branch and naming both halves of a rename are easy to get wrong in a one-liner, and a change set that disagrees with the hook's is worse than none. If no session instructions are present, say so rather than guessing at a command.

This check was asked for, so it does not get skipped as mechanical. Produce both records.

**The comments.** On every file and function the branch added or meaningfully changed, leave a comment in the language's own convention stating its responsibility — what it was meant to achieve for its caller — in two or three sentences at most, for the file and for each function alike. How it works, and why that way, belong in the note. Do not restate the code: a comment that narrates the steps costs a reader time and rots as soon as the code moves. Match the density of the surrounding file.

**The note.** Write `docs/notes/<branch>/YYYY-MM-DD-<short-slug>-<8 random hex characters>.md` — `<branch>` as `git branch --show-current` prints it, or `detached` when it prints nothing — with front matter listing, under `covers`, every repository-relative path it accounts for, and under `supersedes`, any earlier note this change invalidates, named by its path under docs/notes without `.md`. Head the body with a single `#` line naming what the change did — that is the note's title, and the hook shows it when naming the note before a later edit. Then cover three things in `##` sections: what the change was for in the user's terms, the approach and at least one alternative that was rejected and why, and how it is built — which pieces are load-bearing and which are incidental. A few sentences each; say only what the diff cannot.

Look for the notes covering each changed path before writing anything — `grep -rlF -- "<path>" docs/notes`, fixed-string so a name holding `[`, `.` or `*` is not read as a pattern — and read them. A change that contradicts a recorded intent is fine, and is when a note superseding the old one is owed.

Never edit or delete an existing note to make it agree with new work. A note records what was believed when it was written; a change that contradicts one writes a new note that supersedes it.

`covers` is the only part a machine reads, so keep it exact, and never widen it to a path the note does not actually explain.

Ask the user nothing. This skill puts no question to anyone: it is a record you leave, not a test you set. When both records are written, say briefly what you recorded and where.
