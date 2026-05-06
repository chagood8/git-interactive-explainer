# Git Interactive Explainer

A single-file, browser-based teaching tool for the core git mental model — working directory, staging area, local repo, remote repo — with the everyday commands that move files between them.

## Run it

Open `index.html` in any modern browser. No build, no server, no dependencies. Double-click works on every OS.

## Lessons

This repo doubles as the demo target for two hands-on lessons in **Phase 0** of the applied learning program:

- **[LESSON-solo.md](./LESSON-solo.md)** — work alone through the full clone → branch → edit → commit → push → PR loop. ~15 minutes.
- **[LESSON-group.md](./LESSON-group.md)** — same loop, but everyone in the room is committing to this repo at the same time, so `git pull` actually does something. ~25 minutes.

Both lessons cover the 6 commands from Phase 0 slide 7 (`clone`, `status`, `add`, `commit`, `push`, `pull`) plus `git switch -c` for branching and `gh pr create` for opening pull requests.

## What students change

The lessons walk you through editing one CSS color variable in `index.html` (using Claude Code as the coding agent) and shipping it back through GitHub. Tiny change, full pipeline.
