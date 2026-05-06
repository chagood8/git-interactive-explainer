# Solo Lesson: Your First Real Git Loop

You're going to clone a real repo, make a real change with the help of a coding agent, and ship it back to GitHub through a pull request. Every command below is copy-paste ready — paste it into your terminal exactly as written.

**Time:** ~15 minutes.
**You'll use all 6 slide commands** (`clone`, `status`, `add`, `commit`, `push`, `pull`) plus two new ones: `git switch` to branch, and `gh pr create` to open the pull request.

---

## What you need before you start

- [ ] Terminal open (Windows Terminal, macOS Terminal, or VS Code's built-in terminal — all fine)
- [ ] `git --version` returns 2.40+
- [ ] `gh --version` works, and `gh auth status` says you're logged in
- [ ] VS Code installed, with **Claude Code** signed in
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

## Step 3 — Pull (just to see what a no-op pull looks like)

```bash
git pull
```

**Expected:** `Already up to date.`

**Why:** `git pull` asks GitHub "anything new?" and brings it down. Right now there's nothing new — but you'll run this again at the end and it'll do real work.

---

## Step 4 — Create your own branch

```bash
git switch -c color-change-XX
```

Replace `XX` with your initials (e.g. `color-change-cmh`).

**Why:** A branch is a parallel timeline. You make changes here without touching `main`. The `-c` means "create it." (You may also see this written as `git checkout -b` — same thing, older syntax.)

Confirm:
```bash
git status
```
You should now see `On branch color-change-XX`.

---

## Step 5 — Let Claude Code make the change

Open the Claude Code chat panel in VS Code. Paste this prompt:

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

---

## Step 10 — Open a pull request

```bash
gh pr create --fill --web
```

**Why:** A pull request is a formal proposal: "I'd like to merge my branch into main." `--fill` auto-uses your commit message as the PR title/body. `--web` opens your browser so you can hit the green button.

(If `gh` isn't working, GitHub also shows a yellow "Compare & pull request" banner the first time you visit the repo after pushing — that works too.)

In the browser, click **Create pull request**, then **Merge pull request**, then **Confirm merge**.

---

## Step 11 — Bring the merged change back down

```bash
git switch main
git pull
```

**Why:** Now `git pull` does real work. Your local `main` was behind GitHub's `main` (because the merge happened on GitHub, not on your laptop). This brings it down. Run `git log --oneline -5` to see your commit at the top of the history.

You're done. You ran the entire professional git loop on your first day.

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

**`gh: command not found`** — install with `brew install gh` (Mac) or `winget install GitHub.cli` (Windows), then `gh auth login`.

**Claude Code edited the wrong color variable** — undo with `git restore index.html` and try a more specific prompt.

**Browser still shows pink after the agent edit** — hard refresh: Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac).
