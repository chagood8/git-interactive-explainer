# Git Interactive Explainer

A single-file, browser-based teaching tool for the core git mental model — working directory, staging area, local repo, remote repo — with the everyday commands that move files between them.

## Run it

Open `index.html` in any modern browser. No build, no server, no dependencies. Double-click works on every OS.

## Lessons

This repo doubles as the demo target for two hands-on lessons in **Phase 0** of the applied learning program:

- **[LESSON-solo.md](./LESSON-solo.md)** — work alone through clone → branch → edit → commit, then stop and watch the instructor demo push, PR, and merge using their own change. ~15 minutes.
- **[LESSON-group.md](./LESSON-group.md)** — *(deferred)* same loop, but everyone in the room is committing at the same time, so `git pull` actually does something. ~25 minutes. Run after the class is fluent on the solo flow.

Both lessons cover the 6 commands from Phase 0 slide 7 (`clone`, `status`, `add`, `commit`, `push`, `pull`) plus `git switch -c` for branching and `gh pr create` for opening pull requests. In the solo lesson the instructor demos `git push` and `gh pr create` on screen; students run the other five themselves.

**Workflow rules**: students never merge their own PRs. In the solo lesson, students don't push either — the instructor demos `git push`, `gh pr create`, and the merge live in front of the class using their own one change, so everyone sees the flow once cleanly without 30 collaborators or 30 PRs piling up.

## What students change

In the solo lesson, students pick from five plain-named themes (Ocean, Forest, Sunset, Monochrome, Retro) and have a coding agent (Codex, Claude Code, Cursor, etc.) repaint `index.html` accordingly. Tiny change, real workflow up to commit, then watch the rest.
