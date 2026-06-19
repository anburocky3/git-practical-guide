# 📝 Conventional Commit Guide

We follow the **Conventional Commit** standard to keep commit history clean and understandable.

## Format

```text
<type>: <short description>
```

Example:

```bash
feat: create about page layout
fix: resolve navbar overlap issue
docs: update contribution guide
```

---

## Commit Types

### `feat`

Use when adding a **new feature**.

Examples:

```bash
feat: create about page
feat: add contact form
feat: implement dark mode
```

When to use:

- New page
- New component
- New functionality

---

### `fix`

Use when fixing a **bug or issue**.

Examples:

```bash
fix: resolve mobile navbar issue
fix: correct button alignment
fix: prevent form submission error
```

When to use:

- Bug fixes
- UI issues
- Unexpected behavior

---

### `refactor`

Use when improving code without changing functionality.

Examples:

```bash
refactor: extract navbar component
refactor: simplify authentication logic
```

When to use:

- Code cleanup
- Component extraction
- Better structure

---

### `docs`

Use for documentation changes.

Examples:

```bash
docs: update README
docs: add setup instructions
```

When to use:

- README updates
- Contribution guides
- Project documentation

---

### `style`

Use for formatting changes that do not affect functionality.

Examples:

```bash
style: format code using prettier
style: fix indentation
```

When to use:

- Code formatting
- Whitespace changes
- CSS formatting only

---

### `test`

Use when adding or updating tests.

Examples:

```bash
test: add login page tests
test: update validation test cases
```

When to use:

- Unit tests
- Integration tests
- E2E tests

---

### `chore`

Use for maintenance tasks.

Examples:

```bash
chore: update dependencies
chore: configure eslint
chore: update build pipeline
```

When to use:

- Dependency updates
- Build configuration
- Tooling changes

---

### `perf`

Use for performance improvements.

Examples:

```bash
perf: optimize image loading
perf: reduce bundle size
```

When to use:

- Faster rendering
- Better loading performance
- Query optimizations

---

## Referencing Issues

Always reference the issue number when applicable.

Example:

```bash
feat: create about page (#12)
fix: resolve navbar overlap (#14)
```

---

## Good Commit Messages

✅ Good

```bash
feat: create about page layout
fix: resolve footer alignment issue
refactor: extract reusable button component
docs: update branching strategy guide
```

❌ Bad

```bash
update
done
changes
final
new code
```

---

## Team Rule

> Write commit messages as if a new developer will read them six months from now.

A commit message should clearly explain **what changed**, without requiring someone to open the code. 🚀
