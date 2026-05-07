# Group Lesson: Everyone in the Same Repo

> **Status: deferred.** Run the [solo lesson](./LESSON-solo.md) first and let the class get comfortable with the loop before introducing this one. This lesson assumes every student is added as a collaborator on the repo so they can push directly — which adds real overhead and real conflicts. Per the May 7 prep call, we're holding it back until the solo flow is fluent: *"In the group, you're probably gonna hit conflicts… it's going to be noise and people are going to get derailed."* The content below is kept up to date with the solo lesson so it's ready when you are.

This is the same loop as the [solo lesson](./LESSON-solo.md), but with a twist: **everyone in the room is working on the same repo at the same time.** That's where `git pull` finally earns its keep — by the time your instructor merges the class's PRs at the end of the session, ten different changes will land on `main` at once and you'll pull them all down.

**Time:** ~25 minutes including review.
**You'll use all 6 slide commands plus** `git switch -c`, `gh pr create`, and a peek at peer review.

---

## Two rules — read these first

1. **Never push directly to `main`.** All work happens on a branch you create.
2. **Never merge a PR — not yours, not anyone else's.** Your instructor merges every PR from the GitHub UI on screen, so the whole class can see the queue and the merge flow together.

These are not arbitrary rules. They mirror how every real engineering team operates: the author opens the PR, someone else merges it. Building that habit on a tiny color change is far cheaper than building it on a load-bearing change later.

---

## Before you start

Get all of this done **before** the session — installing extensions live burns ~15 minutes you don't have.

- [ ] You've been added as a **collaborator** on `chagood8/git-interactive-explainer` (your instructor handled this; check your email or GitHub notifications and accept the invite)
- [ ] `git --version` returns 2.40+ and `gh auth status` shows you're logged in
- [ ] VS Code installed, with your **coding agent extension** (Codex, Claude Code, or Cursor) installed and signed in. For Codex specifically: Extensions panel → search "Codex" → first result with the blue check from OpenAI → sign in with your SSA email.
- [ ] **You've claimed a CSS variable from the table below.** Each person picks a different one so we don't all fight over the same line. Post your claim in the class chat.

### Variable claim board

| Variable | Current value | Claimed by |
|---|---|---|
| `--pink` | `#e05568` | _____ |
| `--blue` | `#5b7fe0` | _____ |
| `--gold` | `#c48a08` | _____ |
| `--bg` | `#f7f6f3` | _____ |
| `--text` | `#1a1917` | _____ |
| `--muted` | `#999490` | _____ |
| `--border` | `#e8e6e0` | _____ |
| `--surface` | `#ffffff` | _____ |
| `--pink-light` | `#fce8eb` | _____ |
| `--blue-light` | `#eaeefc` | _____ |

If we have more than 10 people, pair up — pairs will share a branch and that's a bonus exercise in coordination.

---

## Step 1 — Clone

In any terminal, run:

```bash
git clone https://github.com/chagood8/git-interactive-explainer.git
```

Then open VS Code → **File → Open Folder…** → pick the `git-interactive-explainer` folder you just cloned. In the file explorer on the left, **right-click the folder → Open in Integrated Terminal**. That terminal is already pointed at the project, so you don't have to `cd`. Use it for the rest of the lesson.

---

## Step 2 — Check status, then pull

```bash
git status
git pull
```

**Why we pull immediately:** in a group repo, `main` may have already moved since you cloned. Always pull `main` before you start work. Always.

---

## Step 3 — Branch, with a name nobody else will use

```bash
git switch -c XX-VARIABLE
```

Use **your initials**, then a dash, then **the variable you claimed**. Examples:

- `cmh-pink`
- `jrs-button-bg`
- `els-border`

**Why naming matters in a group:** if two people both make a branch called `color-change`, the second person to push gets blocked. Initials + element makes collisions impossible.

Confirm:
```bash
git status
```
You should see `On branch XX-VARIABLE`. **If it still says `main`, stop and re-run the switch command.** Editing files while on `main` is rule #1 broken.

---

## Step 4 — Have your coding agent make your change

Open your coding agent in VS Code. Pick a new color in plain English — "warm orange," "deep navy," "forest green," "neon magenta," anything — and paste this prompt with **your claimed variable** filled in:

> In `index.html`, change the value of the `--YOUR_VARIABLE` CSS variable to **[your color in plain words]**. Update only that one line in the `:root` block — leave the other variables alone. Show me the diff first, then apply it.

No hex codes needed. Let the agent figure out the right color value. The "show me the diff first, then apply it" wording does both in one shot — you see what's about to change, then it actually changes. If the agent stops after the diff and waits, just tell it "yes, apply it."

Then **open `index.html` in your browser** (double-click it, or right-click → Open With → your browser) to confirm your variable's element actually changed. If it looks unchanged, hard refresh (Ctrl+Shift+R / Cmd+Shift+R).

---

## Step 5 — Status, add, commit

```bash
git status
git add index.html
git commit -m "Change --VARIABLE to NEW_COLOR"
```

Use a real commit message — your classmates will read it during PR review.

---

## Step 6 — Push your branch

```bash
git push -u origin XX-VARIABLE
```

> If you see `! [remote rejected] main -> main (protected branch)`, you tried to push from `main` instead of your branch. Run `git status`, get on your branch, push again.

---

## Step 7 — Open a PR (and stop)

```bash
gh pr create --fill --web
```

In the browser, click **Create pull request**. **Do not click Merge.** Post the PR URL in the class chat so your classmates can find it for review.

---

## Step 8 — Review one classmate's PR (do not merge)

Pick a PR from the chat that isn't yours. Open it on GitHub. Click the **Files changed** tab.

For each PR you review:
- Does the change match the title?
- Did they only touch the variable they claimed?
- Click **Review changes** → leave a one-line comment → choose **Approve**.

**Approve, don't merge.** Approval is a signal to your instructor that the change looks good. Merging is a separate action that only the instructor takes.

**Why:** Phase 3 will require this on every change. Better to build the muscle on a tiny color swap than the first time it's load-bearing.

---

## Step 9 — Watch the instructor merge the queue

Your instructor will share their screen and open https://github.com/chagood8/git-interactive-explainer/pulls — every open PR from the class, all in one place. Then, one at a time:

1. They open a PR.
2. They walk through the diff and any review comments out loud.
3. They click **Merge pull request** → **Confirm merge**.
4. The PR's branch can be deleted from the UI button.

This is the moment to ask questions. What does "Squash and merge" mean? Why might you delete a branch after merging? What happens if there's a conflict? This is the part of the workflow you'll spend the most time around in any real engineering job.

---

## Step 10 — Pull `main` and see everyone's work

Once the instructor has merged the batch, run:

```bash
git switch main
git pull
git log --oneline -10
```

**This is the moment.** You'll see commits from people you've never met scrolling past in the log. Open `index.html` in your browser — it now reflects every classmate's merged change. That's a real shared codebase, the same mechanic that runs every team you'll ever work on.

---

## Bonus: cause a merge conflict on purpose

Want to see what conflicts look like in safe conditions? Coordinate with one other person:

1. Both of you `git switch main && git pull` to start clean.
2. Both of you `git switch -c <initials>-conflict-test`.
3. Both edit the **exact same line** in `index.html` to different values.
4. Commit and push your branches; both open PRs.
5. The instructor merges the first PR. Fine — it goes through.
6. The instructor tries to merge the second PR. GitHub says "This branch has conflicts that must be resolved." The instructor leaves the PR open and tells the second author to resolve it locally.
7. That author runs:
   ```bash
   git switch main
   git pull
   git switch <your-conflict-branch>
   git merge main
   ```
   Git marks the conflict in `index.html` with `<<<<<<<`, `=======`, `>>>>>>>` markers.
8. Edit the file to keep whichever value you want, remove the markers, then:
   ```bash
   git add index.html
   git commit -m "Resolve conflict with main"
   git push
   ```
9. The PR is now mergeable. The instructor merges it.

Conflict resolution is the most common "git is scary" moment. Now it isn't, and you've also seen exactly why letting a single human be the merger keeps the queue sane.

---

## Recap — what you used

| Command | Where |
|---|---|
| `git clone` | Step 1 |
| `git status` | Steps 2, 3, 5 |
| `git pull` | Steps 2, 10 (the meaningful one) |
| `git add` | Step 5 |
| `git commit -m` | Step 5 |
| `git push` | Step 6 |
| `git switch -c` | Step 3 |
| `gh pr create` | Step 7 |
| `git merge` (bonus) | Conflict resolution |

---

## Common stumbles

**`remote: Permission to chagood8/git-interactive-explainer.git denied`** — you weren't added as a collaborator yet. Ping your instructor.

**`! [remote rejected] main -> main (protected branch)`** — you tried to push to `main`. Get on your branch first.

**Two people claimed the same variable** — both will end up editing the same line, and one of you will have to resolve a conflict (see bonus section). The board exists to prevent this; check it before you start.

**My PR shows hundreds of changes, not one line** — your branch is based on an old `main`. Run `git switch main && git pull && git switch YOUR-BRANCH && git merge main`, resolve any conflicts, push again.

**I clicked Merge by mistake** — tell your instructor. They'll handle it. The teaching demo of seeing every PR get merged together still works for the rest.
