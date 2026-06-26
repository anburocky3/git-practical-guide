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
