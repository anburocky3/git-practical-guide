As the Repo Owner, your primary goal is protecting `main` while allowing Saran and Gokul to move fast without stepping on each other's keyboards. To do that, we are going to enforce a **Trunk-Based / GitFlow Hybrid**.

- `main` = Production. Locked. Nobody pushes here directly.
- `develop` = Integration. The shared reality. Must always compile and run.
- `feature/*` = Disposable isolation booths.

Here is how your team handles the four most common real-world scenarios.

---

## Scenario 1: The Clean Feature (Saran & The Squash)

Saran is assigned to build the _Contact Page_.

1. **Saran cuts his branch:**

```bash
git checkout develop
git pull origin develop
git checkout -b feature/saran-contact-page

```

2. **Saran gets messy.** Over 3 days, he makes 5 local commits:

- `wip: started layout`
- `added form inputs`
- `forgot the submit button lol`
- `fixed css padding`
- `actually fixed the css this time`

3. **Saran opens a Pull Request to `develop`.**

#### The Tech Lead Decision (Anbu):

- **Bad Practice (Standard Merge):** You click _Merge_. `develop` now permanently inherits 5 garbage commit messages. Six months from now, someone `git blame`s a bug and sees _"actually fixed the css this time"_.
- **Best Practice (Squash & Merge):** You select **Squash and Merge**. GitHub compresses Saran’s 5 messy commits into **one single, beautifully written commit** on `develop`:
  > `feat(contact): add responsive contact form (#42)`

Saran’s chaotic local journey is erased; the company's master timeline stays pristine.

---

## Scenario 2: The Collision (Gokul vs. Saran)

On Monday morning:

- Gokul is building `feature/gokul-auth`
- Saran is building `feature/saran-header`
- **Both of them edit `src/App.jsx**` to register their components.

1. **10:00 AM:** Gokul finishes first. His PR is approved, squashed, and merged into `develop`.
2. **11:00 AM:** Saran finishes his header. He pushes his branch and opens a PR.
3. **GitHub blocks Saran's PR:** `This branch has conflicts that must be resolved.`

#### The Best Practice Protocol:

Junior devs panic here and tag the Lead (_"Anbu bro please fix"_). **Rule #1 of the repo: The author of the PR fixes their own conflicts locally.**

Saran must pull Gokul's merged reality into his isolated booth:

```bash
# 1. Update local develop
git checkout develop
git pull origin develop

# 2. Bring develop into his feature branch
git checkout feature/saran-header
git merge develop

```

Terminal spits out: `CONFLICT (content): Merge conflict in src/App.jsx`.

Saran opens VS Code and sees the collision markers:

```javascript
<<<<<<< HEAD
import Header from './components/Header';
=======
import AuthModal from './components/AuthModal';
>>>>>>> develop

```

Saran realizes _both_ imports need to exist. He manually edits the file to:

```javascript
import Header from "./components/Header";
import AuthModal from "./components/AuthModal";
```

He stages the fix and pushes:

```bash
git add src/App.jsx
git commit -m "chore: resolve import collision with develop"
git push origin feature/saran-header

```

GitHub instantly detects the update, drops the red warning, and turns the PR green for your review.

---

## Scenario 3: The Long Haul (Gokul & The Rebase)

Gokul is assigned a monster task: _Stripe Payment Integration_ (`feature/gokul-payments`). It takes him 7 days.

During those 7 days, you and Saran merge 18 different PRs into `develop`. Gokul’s branch is now ancient history. If Gokul runs `git merge develop` every afternoon to stay updated, his branch history will become a spiderweb of 6 separate _"Merge branch develop into feature/gokul-payments"_ commits.

#### The Best Practice: The Morning Rebase

Every morning at 9:30 AM, Gokul runs this sequence:

```bash
git checkout develop
git pull origin develop

git checkout feature/gokul-payments
git rebase develop

```

**What `rebase` does conceptually:**
Git temporarily lifts Gokul's 4 payment commits off the desk, fast-forwards his branch to the exact tip of today's `develop`, and then **re-plays his 4 commits back down onto the top of the deck**, one by one.

**The Catch:** Because rebasing rewrites the cryptographic hashes of his commits, GitHub will reject his standard push that evening. Gokul must use the safety-override push:

```bash
git push --force-with-lease origin feature/gokul-payments

```

_(Lead Note: Teach them `--force-with-lease` strictly. Standard `--force` is blind; `--force-with-lease` double-checks the server to make sure Gokul isn't accidentally overwriting code a teammate pushed to his branch an hour ago)._

---

## The Tech Lead's Cheat Sheet

Pin this matrix in your team's Discord/Slack:

| Strategy           | What it does to history               | Best used for...                         | The Golden Rule                              |
| ------------------ | ------------------------------------- | ---------------------------------------- | -------------------------------------------- |
| **Squash & Merge** | Condenses a branch into 1 commit      | Merging completed Feature PRs            | Write a clear, semantic commit title         |
| **Rebase**         | Re-plays commits on top of new code   | Keeping a private feature branch updated | **NEVER** rebase a shared branch             |
| **Standard Merge** | Preserves all commits and ties a knot | Merging `develop` up into `main`         | Use when exact chronological history matters |
