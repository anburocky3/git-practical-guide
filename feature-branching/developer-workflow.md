#### **1. The Core Merge Strategies Explained**

| Strategy           | What It Does                                                                                          | When to Use It                                                                                                                   |
| ------------------ | ----------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| **Rebase**         | Rewrites history to place your commits neatly on top of the latest target branch. Changes commit IDs. | **Locally only.** When Gokul or Saran need to update their active `feature/*` branch with the latest changes from `develop`.     |
| **Squash & Merge** | Compresses all commits from a PR into **one** single, clean commit on the target branch.              | Merging a `feature/*` branch PR into `develop`. It keeps the `develop` history readable without the "wip" or "typo fix" commits. |
| **Standard Merge** | Ties two branches together with a "merge commit." Preserves exact, chronological history.             | Merging `develop` into `main` for a production release. You want the exact, audited history of everything going into production. |

#### **2. Step-by-Step Developer Workflow**

**Phase 1: Feature Development (The Rebase Phase)**
When a developer (e.g., Saran) is working on a feature and `develop` gets updated by someone else, Saran should update his local branch using `rebase`.

1. Saran ensures his local `develop` is up to date: `git checkout develop && git pull`
2. Saran switches to his feature branch: `git checkout feature/contact-page`
3. Saran rebases onto develop: `git rebase develop`
4. _Why?_ This keeps his feature branch clean and up-to-date without creating messy merge loops. Because `feature/contact-page` is _his_ branch, rewriting its history is safe.

**Phase 2: Opening the Pull Request**
Before opening a PR, the developer must ensure their code is conflict-free.

1. The developer pushes their branch to origin. (If they just rebased, they must use `git push --force-with-lease origin feature/branch-name`).
2. The PR is opened against `develop`.
3. The PR title must clearly state the feature (e.g., `feat: add contact page UI`).

**Phase 3: Review and Merge (The Squash Phase)**
As the tech lead, you review the code.

1. Once approved, **do not use standard merge or rebase**.
2. Click **Squash and Merge** in the GitHub/GitLab UI.
3. _Why?_ This takes Saran's 12 small commits and turns them into 1 perfect, atomic commit on `develop`. The `develop` timeline remains pristine.

**Phase 4: Production Release (The Standard Merge Phase)**
When `develop` is stable and it is time to deploy to production.

1. Open a PR from `develop` to `main`.
2. Use a **Standard Merge** (Create a merge commit).
3. _Why?_ `main` must reflect reality. A standard merge preserves the exact IDs of the squashed features that were tested on `develop`, creating a clear release milestone.

#### **3. Handling PR Conflicts**

If GitHub blocks a PR due to a conflict, the burden of fixing it falls on the developer who opened the PR, not the reviewer.

- The developer must pull the latest `develop` to their local machine.
- They merge `develop` into their feature branch locally (`git merge develop`).
- They resolve the conflicts in their code editor, commit the fix, and push back to their feature branch.
- The PR will automatically update and unblock.
