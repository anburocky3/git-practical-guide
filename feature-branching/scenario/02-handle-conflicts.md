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
