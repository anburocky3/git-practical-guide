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
