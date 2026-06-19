# Git Setup and Configuration

This guide helps new contributors install and configure Git before contributing to the repository.

---

# Install Git

## Windows

Download Git:

https://git-scm.com/download/win

Verify installation:

```bash
git --version
```

Expected:

```text
git version 2.x.x
```

---

## macOS

Install using Homebrew:

```bash
brew install git
```

Verify:

```bash
git --version
```

---

## Ubuntu / Debian

```bash
sudo apt update
sudo apt install git
```

Verify:

```bash
git --version
```

---

## Fedora

```bash
sudo dnf install git
```

---

# Configure Git Identity

Git uses your name and email in commits.

Set your username:

```bash
git config --global user.name "Your Name"
```

Set your email:

```bash
git config --global user.email "you@example.com"
```

Verify:

```bash
git config --global --list
```

Example:

```text
user.name=Gokul
user.email=gokul@example.com
```

---

# Configure Default Branch

Modern repositories use:

```text
main
```

Configure Git:

```bash
git config --global init.defaultBranch main
```

---

# Configure Editor

VS Code:

```bash
git config --global core.editor "code --wait"
```

---

# Generate SSH Key (Recommended)

Check existing keys:

```bash
ls ~/.ssh
```

Generate new key:

```bash
ssh-keygen -t ed25519 -C "you@example.com"
```

Start SSH Agent:

```bash
eval "$(ssh-agent -s)"
```

Add key:

```bash
ssh-add ~/.ssh/id_ed25519
```

Copy public key:

```bash
cat ~/.ssh/id_ed25519.pub
```

Add it to GitHub:

GitHub → Settings → SSH and GPG Keys

---

# Verify GitHub Connection

```bash
ssh -T git@github.com
```

Expected:

```text
Hi username! You've successfully authenticated.
```

---

# Clone Repository

HTTPS:

```bash
git clone https://github.com/ORG/REPO.git
```

SSH:

```bash
git clone git@github.com:ORG/REPO.git
```

---

# Useful Git Commands

## Check Status

```bash
git status
```

## Pull Latest Changes

```bash
git pull
```

## Create Branch

```bash
git checkout -b feat/12-about-page
```

## Push Branch

```bash
git push -u origin feat/12-about-page
```

## Fetch Remote Branches

```bash
git fetch --all
```

---

# Recommended Git Aliases

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm commit
```

Usage:

```bash
git st
git co main
git br
```

---

# Verify Setup

Run:

```bash
git --version

git config --global --list
```

If both work correctly, your Git setup is complete.
