# Solo Lesson: Your First Real Git Loop

You're going to clone a real repo, make a real change with the help of a coding agent, and propose it back to GitHub through a pull request. Every command below is copy-paste ready — paste it into your terminal exactly as written.

**Time:** ~15 minutes.
**You'll use all 6 slide commands** (`clone`, `status`, `add`, `commit`, `push`, `pull`) plus two new ones: `git switch` to branch, and `gh pr create` to open the pull request.

---

## Two rules — read these first

These apply to **every** lesson in this repo, both solo and group:

1. **Never push directly to `main`.** All your work happens on a branch you create.
2. **Never merge your own PR.** You open it. Your instructor reviews and merges from the GitHub UI in front of the class — that's the teaching moment.

You'll see why this matters in the real world: in any team worth working on, the person who writes the change is not the person who merges it. Building that habit now costs you nothing.

---

## What you need before you start

- [ ] Terminal open (Windows Terminal, macOS Terminal, or VS Code's built-in terminal — all fine)
- [ ] `git --version` returns 2.40+
- [ ] `gh --version` works, and `gh auth status` says you're logged in
- [ ] VS Code installed, with your **coding agent** (Claude Code, Codex, Cursor, etc.) signed in
- [ ] You've picked a folder to clone into. Suggestion: `cd ~` or `cd Documents`

---

## Step 1 — Clone the repo

```bash
git clone https://github.com/chagood8/git-interactive-explainer.git
```

**Why:** `git clone` copies the entire repo (files + every commit ever made) onto your machine and points it at GitHub as the "remote." This is how 99% of projects start on your laptop.

```bash
cd git-interactive-explainer
code .
```

VS Code opens with the project. The file you'll edit today is `index.html`.

---

## Step 2 — Take stock with `git status`

```bash
git status
```

**Expected output:**
```
On branch main
Your branch is up to date with 'origin/main'.
nothing to commit, working tree clean
```

**Why:** `git status` is the safest command in git — it never changes anything. Run it constantly. It tells you what branch you're on, what's changed, and what's staged.

---

## Step 3 — Pull to make sure you have the latest `main`

```bash
git pull
```

If you just cloned, you'll see `Already up to date.` That's fine. If other students have had PRs merged since your clone, this brings their work down. **Always pull `main` before starting a new branch** — that one habit prevents 80% of merge conflicts.

---

## Step 4 — Create your own branch (do not skip this)

```bash
git switch -c color-change-XX
```

Replace `XX` with your initials (e.g. `color-change-cmh`).

**Why:** A branch is a parallel timeline. You make changes here without touching `main`. The `-c` means "create it." (You may also see this written as `git checkout -b` — same thing, older syntax.)

Confirm:
```bash
git status
```
You should now see `On branch color-change-XX`. **If it still says `On branch main`, stop and re-run the `git switch -c` command.** Never edit files while `git status` says you're on `main`.

---

## Step 5 — Let your coding agent make the change

Open your coding agent's chat panel in VS Code. Paste this prompt:

> In `index.html`, change the `--pink` CSS variable (currently `#e05568`) to teal (`#0d9488`). Update only the `--pink` definition in the `:root` block — leave `--pink-light` alone. Show me the diff before applying.

Accept the change. Then **open `index.html` in your browser** (double-click it, or right-click → Open With → your browser) and confirm the pink accents are now teal.

**Why:** This is the core loop you'll use every day from Phase 1 onward — describe what you want, the agent edits the code, you verify visually.

---

## Step 6 — See what changed

```bash
git status
```

You'll see:
```
modified:   index.html
```

Optional but useful:
```bash
git diff
```
This shows the exact lines that changed. Press `q` to quit if it pages.

---

## Step 7 — Stage the change

```bash
git add index.html
```

**Why:** Staging is git's "ready for the next commit" pile. You can stage some files and not others — that's how you make focused commits.

---

## Step 8 — Commit

```bash
git commit -m "Change accent color to teal"
```

**Why:** A commit is a permanent snapshot. The `-m` flag attaches a message so future-you (or your teammates) know why this change exists. **Write commit messages in the imperative**: "Change X," not "Changed X."

---

## Step 9 — Push your branch to GitHub

```bash
git push -u origin color-change-XX
```

**Why:** `git push` sends your commits up to GitHub. The `-u origin <branch>` part links your local branch to a new remote branch with the same name. You only need `-u` the first time you push a new branch — after that, plain `git push` works.

> If you ever see an error like `! [remote rejected] main -> main (protected branch)`, that's the safety net working — you tried to push to `main` instead of your branch. Re-run `git status`, confirm you're on your branch, push again.

---

## Step 10 — Open a pull request, then **stop**

```bash
gh pr create --fill --web
```

**Why:** A pull request is a formal proposal: "I'd like to merge my branch into main." `--fill` auto-uses your commit message as the PR title/body. `--web` opens your browser so you can hit the green button to file it.

(If `gh` isn't working, GitHub also shows a yellow "Compare & pull request" banner the first time you visit the repo after pushing — that works too.)

In the browser, click **Create pull request**. **Do not click Merge.** Your PR is now sitting in the queue at https://github.com/chagood8/git-interactive-explainer/pulls alongside everyone else's.

You're done with the active part of the lesson. ✅

---

## Step 11 — (Later) After your instructor merges PRs, sync `main`

Your instructor will walk through the open PRs in class, review them on screen, and merge them through the GitHub UI. Once they've merged your PR (and your classmates'), come back to your terminal and run:

```bash
git switch main
git pull
git log --oneline -10
```

**This is where `git pull` finally does real work.** Your local `main` was behind GitHub's `main` because the merges happened on GitHub, not on your laptop. The pull brings everything down at once. You'll see your commit alongside your classmates' commits in the log — a real shared history.

You ran the entire professional git loop: branch → change → commit → push → PR → (someone else reviews and merges) → pull. That's the workflow real teams use, every day.

---

## Recap — the 6 slide commands in context

| Command | When you used it |
|---|---|
| `git clone` | Step 1 — got the project |
| `git status` | Steps 2, 4, 6 — checked state |
| `git pull` | Steps 3, 11 — synced from GitHub |
| `git add` | Step 7 — staged your change |
| `git commit -m` | Step 8 — snapshotted it |
| `git push` | Step 9 — sent it up |

Plus the two "one step further" commands:

| Command | When you used it |
|---|---|
| `git switch -c` | Step 4 — made a branch |
| `gh pr create` | Step 10 — opened the PR |

---

## Common stumbles

**`git push` says "src refspec main does not match any"** — you're not on a branch with commits. Run `git status` to check.

**`! [remote rejected] main -> main (protected branch)`** — you tried to push to `main`. Get on your branch (`git switch color-change-XX`) and try again.

**`gh: command not found`** — install with `brew install gh` (Mac) or `winget install GitHub.cli` (Windows), then `gh auth login`.

**Your coding agent edited the wrong color variable** — undo with `git restore index.html` and try a more specific prompt.

**Browser still shows the old color after the agent edit** — hard refresh: Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac).

**You accidentally clicked Merge on your own PR** — tell your instructor. Not the end of the world; just breaks the teaching demo for one PR.
