# ⚙️ Git Configuration Guide

This guide helps you configure Git to suit your workflow. It covers global and local settings, identity configuration, aliases, and editor preferences.

---

## 🧾 1. Set Your User Identity

This info is stored in every Git commit.

### Global (applies to all repos):

```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

### Local (overrides global in the current repo):

```bash
git config user.name "Work Name"
git config user.email "work_email@example.com"
```

## 🛠️ 2. Common Global Settings

```
# Set default branch name
git config --global init.defaultBranch main

# Use VS Code (or any editor) as Git's editor
git config --global core.editor "code --wait"

# Enable helpfull color output
git config --global color.ui auto
```

## ✨ 3. Useful Git Aliases

Aliases help you run commands faster:

```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm commit
git config --global alias.st status
git config --global alias.last "log -1 HEAD"
```

You can now use:

```bash
git co main
git cm -m "Add feature"
```

## 📁 4. View Current Config

```bash
# View all settings
git config --list

# View global settings
git config --global --list
```

## 🧹 5. Remove a Config Setting

```bash
# Unset a global setting
git config --global --unset user.email
```

## 💬 Pro Tip

Use a different Git identity per project by setting local configs inside each repository:

```bash
cd ~/projects/work-repo/
git config user.name "Work Name"
git config user.email "work@example.com"
```

## 📚 Resources

- [Git Official Config Docs](https://git-scm.com/docs/git-config)
- See also: [ssh-key-setup.md](./ssh-key-setup.md) and [linux-multiple-accounts-setup.md](./linux-multiple-accounts-setup.md)
