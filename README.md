# Git Interactive Explainer

A single-file, browser-based teaching tool for the core git mental model — working directory, staging area, local repo, remote repo — with the everyday commands that move files between them.

## Run it

Open `index.html` in any modern browser. No build, no server, no dependencies. Double-click works on every OS.

## Lessons

This repo doubles as the demo target for two hands-on lessons in **Phase 0** of the applied learning program:

- **[LESSON-solo.md](./LESSON-solo.md)** — work alone through clone → branch → edit → commit, then hand the branch to your instructor to push and PR live. ~15 minutes.
- **[LESSON-group.md](./LESSON-group.md)** — *(deferred)* same loop, but everyone in the room is committing at the same time, so `git pull` actually does something. ~25 minutes. Run after the class is fluent on the solo flow.

Both lessons cover the 6 commands from Phase 0 slide 7 (`clone`, `status`, `add`, `commit`, `push`, `pull`) plus `git switch -c` for branching and `gh pr create` for opening pull requests. In the solo lesson the instructor demos `git push` and `gh pr create` on screen; students run the other five themselves.

**Workflow rules**: students never merge their own PRs. The instructor walks through the open PR queue at https://github.com/chagood8/git-interactive-explainer/pulls and merges from the GitHub UI on screen — that's the teaching moment. In the solo lesson, students don't push either; the instructor pushes their branches in front of the class so everyone sees the same PR queue without having to add 30 collaborators.

## What students change

The lessons walk you through editing one CSS color variable in `index.html` using your coding agent (Claude Code, Codex, Cursor, or similar) and shipping it back through GitHub. Tiny change, full pipeline.
