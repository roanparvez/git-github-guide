# 🔐 SSH Key Setup for GitHub

This guide helps you set up SSH keys to securely connect to GitHub without entering your username and password each time.

---

## ✅ Step 1: Check for Existing SSH Keys

Before generating a new key, check if one already exists:

```bash
ls -al ~/.ssh
```

Look for files named `id_ed25519.pub`, `id_rsa.pub`, or similar.

---

## 🧰 Step 2: Generate a New SSH Key

### Generate Ed25519 Key (Recommended)

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

### Generate RSA Key (Alternative)

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

**When prompted:**

- Press `Enter` to accept the default save location.
- Choose a passphrase or leave it blank for no passphrase.

---

## 💼 Step 3: Add Your SSH Key to the SSH Agent

Start the agent and add your key:

```bash
# Start the agent
eval "$(ssh-agent -s)"

# Add the key
ssh-add ~/.ssh/id_ed25519
```

Replace `id_ed25519` with the actual filename if you used a custom one.

---

## 🌐 Step 4: Add Your SSH Public Key to GitHub

1. Copy the public key:

   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```

2. Add the key to GitHub:
   - Navigate to **Settings** → **SSH and GPG Keys** → **New SSH Key**.
   - Provide a title (e.g., "Personal Linux").
   - Paste the contents of your `.pub` key file.

---

## 🧪 Step 5: Test the SSH Connection

Test your connection to GitHub:

```bash
ssh -T git@github.com
```

Expected output:

```plaintext
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## ⚙️ Optional: SSH Config for Multiple Keys

If you use **multiple GitHub accounts**, configure SSH for each account:

1. Open the SSH config file:

   ```bash
   nano ~/.ssh/config
   ```

2. Add configurations for each account:

   ```text
   # Personal GitHub
   Host github.com-personal
     HostName github.com
     User git
     IdentityFile ~/.ssh/id_ed25519_personal

   # Work GitHub
   Host github.com-work
     HostName github.com
     User git
     IdentityFile ~/.ssh/id_ed25519_work
   ```

3. Save (`CTRL + S`) and exit (`CTRL + X`).

To clone a repository, use:

```bash
git clone git@github.com-personal:username/repo.git
```

---

## 📚 Related Guides

- [Git Configuration Guide](./git-config.md)
- [Multiple GitHub Accounts Setup](./linux-multiple-github-accounts-setup.md)

---

## ✅ Summary

SSH keys provide a secure, passwordless way to connect with GitHub. Use `Ed25519` for better security, add your public key to GitHub, and configure multiple keys with an SSH config file for seamless account management.
