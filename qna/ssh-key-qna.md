# ❓ SSH Key – Frequently Asked Questions

This document addresses common questions about SSH keys, including key types, setup, and troubleshooting for Git and GitHub.

---

## 🔐 Key Types

### ❓ Which SSH key type should I use: Ed25519 or RSA, and why?

> ✅ **Ed25519**: Recommended for most users. It's modern, secure, smaller, and faster.  
> ❗ **RSA (4096-bit)**: Use only if you're working with older systems that don’t support Ed25519 (e.g., legacy servers or corporate firewalls).

| Feature     | Ed25519        | RSA (4096-bit) |
| ----------- | -------------- | -------------- |
| Security    | Strong         | Strong         |
| Performance | Faster         | Slower         |
| Key size    | Smaller (256b) | Larger (4096b) |
| Support     | Modern systems | Legacy systems |

### ✔️ Use Ed25519 unless:

- You need to connect to older systems that only support RSA.
- You work in a legacy enterprise environment.

---

## 🔑 Managing SSH Keys

### ❓ Can I use multiple SSH keys on the same system?

> Yes! You can manage multiple SSH keys using a `~/.ssh/config` file.

```text
Host github.com-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_personal

Host github.com-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_work
```

To clone a repository, use:

```bash
git clone git@github.com-personal:username/repo.git
```

---

## ❓ How do I know if my SSH key is added to the agent?

Run the following command:

```bash
ssh-add -l
```

If no identities are listed, add your key:

```bash
ssh-add ~/.ssh/id_ed25519
```

---

## ❓ How do I remove or regenerate an SSH key?

To delete and regenerate an SSH key:

```bash
# Delete the existing key
rm ~/.ssh/id_ed25519 ~/.ssh/id_ed25519.pub

# Generate a new key
ssh-keygen -t ed25519 -C "your_email@example.com"
```

---

## 🛠️ Troubleshooting

### ❓ I get "Permission denied (publickey)" — what’s wrong?

This error usually indicates:

- Your key hasn’t been added to GitHub.
- The SSH agent doesn’t have your key loaded.
- You’re connecting with the wrong identity.

Steps to resolve:

```bash
# Add key to agent
ssh-add ~/.ssh/id_ed25519

# Check SSH config
cat ~/.ssh/config

# Test connection
ssh -T git@github.com
```

---

### ❓ How do I test my SSH connection to GitHub?

Run the following command:

```bash
ssh -T git@github.com
```

If successful, you’ll see:

```text
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## 📚 Related Files

- [Setup SSH Key](/setup/ssh-key-setup.md)
- [Config Git](/setup/git-config.md)
- [Setup Multiple GitHub Accounts on Linux](/setup/linux-multiple-github-accounts-setup.md)

