# Solo Lesson: Your First Real Git Loop

You're going to clone a real repo, make a real change with the help of a coding agent, then **stop** and watch your instructor walk through what happens next — pushing a change, opening a pull request, merging it — using their own change as the demo. Every command below is copy-paste ready.

**Time:** ~15 minutes.
**You'll run 5 of the 6 slide commands** (`clone`, `status`, `add`, `commit`, `pull`) plus `git switch -c` to create a branch. You'll watch your instructor run the 6th — `git push` — plus `gh pr create` and the merge, all live on screen.

---

## Two rules — read these first

1. **You don't push in this lesson.** Cloning, branching, editing, and committing all stay on your machine. Your instructor will demo `git push` on screen using their own branch — you watch the command and the output.
2. **You don't open or merge a PR either.** Same reason — your instructor walks through `gh pr create` and the merge button on their own change so the whole class sees the flow once, cleanly, without 30 PRs piling up.

You'll see why this matters in the real world: in any team worth working on, push permissions are scoped tightly, and the person who writes the change is often not the person who merges it. We're building that habit on a tiny color change so you've already seen it once before it matters.

---

## What you need before you start

Get all of this done **before** the session — installing extensions live burns ~15 minutes you don't have.

- [ ] Terminal works (Windows Terminal, macOS Terminal, or VS Code's built-in terminal — all fine)
- [ ] `git --version` returns 2.40+
- [ ] VS Code installed
- [ ] **Codex extension installed** in VS Code (Extensions panel → search "Codex" → first result with the blue check from OpenAI), and you're signed in with your SSA email so the chat panel is ready to go. If your team uses a different agent (Claude Code, Cursor), the same rule applies: installed, signed in, ready before the session starts.
- [ ] You've picked a folder to clone into (your Desktop is fine)

---

## Step 1 — Clone the repo

In any terminal — VS Code's, Windows Terminal, macOS Terminal, doesn't matter — run:

```bash
git clone https://github.com/chagood8/git-interactive-explainer.git
```

**Why:** `git clone` copies the entire repo (files + every commit ever made) onto your machine and points it at GitHub as the "remote." This is how 99% of projects start on your laptop.

Now open VS Code, go to **File → Open Folder…**, and pick the `git-interactive-explainer` folder you just cloned. Then in the file explorer on the left, **right-click the folder → Open in Integrated Terminal**.

That gives you a terminal that's already pointed at the project — no `cd` to type, no risk of running git commands in the wrong directory. Use this terminal for the rest of the lesson.

The file you'll edit today is `index.html`.

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

If you just cloned, you'll see `Already up to date.` That's fine — `main` hasn't moved since you grabbed it seconds ago. **Always pull `main` before starting a new branch** anyway — that one habit prevents 80% of merge conflicts in real-world repos where someone else may have merged something in the last five minutes.

---

## Step 4 — Create your own branch (do not skip this)

```bash
git switch -c theme-XX
```

Replace `XX` with your initials (e.g. `theme-cmh`).

**Why:** A branch is a parallel timeline. You make changes here without touching `main`. The `-c` means "create it." (You may also see this written as `git checkout -b` — same thing, older syntax.)

Confirm:
```bash
git status
```
You should now see `On branch theme-XX`. **If it still says `On branch main`, stop and re-run the `git switch -c` command.** Never edit files while `git status` says you're on `main`.

---

## Step 5 — Let your coding agent make the change

Open your coding agent's chat panel in VS Code. Pick **one** of these themes:

- **Ocean** — blues and teals
- **Forest** — greens and earth tones
- **Sunset** — warm oranges and pinks
- **Monochrome** — grayscale
- **Retro** — 80s neon

Then paste this prompt, swapping in the theme you picked:

> In `index.html`, change the page's color theme to **[your theme]**. Show me the diff first, then apply it.

That's the whole prompt. No hex codes, no variable names — let the agent figure out which CSS variables to touch. The "show me the diff first, then apply it" wording does two things in one shot: you see what's about to change, then it actually changes. If the agent stops after the diff and waits, just tell it "yes, apply it."

Once it applies, **open `index.html` in your browser** (double-click it, or right-click → Open With → your browser) and confirm the page actually looks like the theme you picked. If it doesn't, hard refresh (Ctrl+Shift+R / Cmd+Shift+R) — the browser may be caching the old version.

**Why:** This is the core loop you'll use every day from Phase 1 onward — describe what you want in plain English, the agent edits the code, you verify visually. The reason we ask for the diff first is the safety habit: agents are fast and confident, and you want one beat to glance at what's about to land before it does.

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
git commit -m "Apply [theme] color theme"
```

Swap `[theme]` for whichever theme you picked, e.g. `Apply ocean color theme`.

**Why:** A commit is a permanent snapshot. The `-m` flag attaches a message so future-you (or your teammates) know why this change exists. **Write commit messages in the imperative**: "Apply X," not "Applied X."

---

## Step 9 — Stop. Watch your instructor push.

You're done with the typing part. ✅ Sit back.

Your instructor has been working on their own theme branch alongside the class — same steps you just did, on their machine. They're about to demo what comes next using **their** change, on screen:

```bash
git push -u origin theme-INSTRUCTOR
```

Watch the output. The branch is now on GitHub. **You're not a collaborator on this repo, which is why you can't push directly** — push permissions are scoped tightly on every real engineering team. Watching how it works once is the point.

---

## Step 10 — Watch the PR open and merge

Your instructor will then run:

```bash
gh pr create --fill --web
```

That opens a pull request in their browser. They'll click **Create pull request**, walk through the **Files changed** tab so you see the diff, then click **Merge pull request → Confirm merge**.

This is the moment to ask questions: What's "Squash and merge" vs. "Merge commit"? When would you delete a branch after merging? What if two PRs touch the same line? Phase 1 leans on this every day; better to ask now than the first time it's load-bearing.

---

## Step 11 — Sync `main` and see the change land

Once your instructor has merged their PR, come back to your terminal and run:

```bash
git switch main
git pull
git log --oneline -10
```

**This is where `git pull` finally does real work.** Your local `main` was behind GitHub's `main` because the merge happened on GitHub, not on your laptop. The pull brings the new commit down. You'll see your instructor's commit at the top of the log — a tiny but real demonstration that GitHub is the source of truth and your local copy catches up via `pull`.

Your own commit, by the way, is still sitting on your local `theme-XX` branch. It never went anywhere — and that's fine. It's a learning artifact. `git switch theme-XX && git log` will show it any time you want to see it.

You ran the writing half of the loop yourself. You watched the shipping half. That's a real division of labor — most engineers spend the bulk of their day on the writing half and gate the shipping half behind exactly the kind of review you just watched.

---

## Recap — the 6 slide commands in context

You ran 5 of them yourself; you watched your instructor demo the 6th.

| Command | Who ran it | When |
|---|---|---|
| `git clone` | You | Step 1 — got the project |
| `git status` | You | Steps 2, 4, 6 — checked state |
| `git pull` | You | Steps 3, 11 — synced from GitHub |
| `git add` | You | Step 7 — staged your change |
| `git commit -m` | You | Step 8 — snapshotted it |
| `git push` | Instructor | Step 9 — sent their branch up |

Plus the two "one step further" commands:

| Command | Who ran it | When |
|---|---|---|
| `git switch -c` | You | Step 4 — made a branch |
| `gh pr create` | Instructor | Step 10 — opened the PR |

---

## Common stumbles

**`fatal: not a git repository`** — your terminal isn't pointed at the cloned folder. In VS Code's file explorer, right-click the `git-interactive-explainer` folder → **Open in Integrated Terminal**, and run the command in that terminal.

**The agent showed the diff and just sits there** — the prompt asks it to apply after showing. If it's still waiting, type "yes, apply it" or click the **Apply** / **Accept** button in the agent panel.

**Browser still shows the old colors after the agent edit** — hard refresh: Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac).

**The agent only changed half the colors, or picked something off-theme** — undo with `git restore index.html`, then re-prompt with a clearer theme name (or pick a different theme).

**`git status` says `On branch main`** — you skipped Step 4 or the `git switch -c` failed. Run `git switch theme-XX` (your initials) to get back on your branch before you commit anything.
