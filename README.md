
# SSH Setup Guide for Managing Multiple GitHub Accounts on One Machine (Windows)

This guide helps you generate, rename, and configure SSH keys to use **multiple GitHub accounts** from a single Windows PC.

---

## 📁 Step 1: Check Existing SSH Keys

```bash
ls ~/.ssh
```

Typical output:

```
id_ed25519
id_ed25519.pub
```

---

## 🔑 Step 2: Generate Separate SSH Keys

### GitHub Account 1 (e.g., 90s-it)

```bash
ssh-keygen -t ed25519 -C "9tisit@gmail.com" -f ~/.ssh/id_ed25519_90sit
```

### GitHub Account 2 (e.g., Nazmul-Islam-Naim)

```bash
ssh-keygen -t ed25519 -C "nazmulislam.bdb@gmail.com" -f ~/.ssh/id_ed25519_naim
```

---

## 🔐 Step 3: Add Keys to SSH Agent

Start agent and add keys:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519_90sit
ssh-add ~/.ssh/id_ed25519_naim
```

---

## ⚙️ Step 4: Configure `~/.ssh/config`

Create or edit the config file:

```bash
nano ~/.ssh/config
```

Add the following:

```ssh
# GitHub Account 1 - 90s-it
Host github-90sit
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_90sit

# GitHub Account 2 - Nazmul-Islam-Naim
Host github-naim
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_naim
```

---

## 🌐 Step 5: Add SSH Public Keys to GitHub

### Copy key to clipboard:

```bash
clip < ~/.ssh/id_ed25519_90sit.pub
clip < ~/.ssh/id_ed25519_naim.pub
```

### Add each key to GitHub at:

[https://github.com/settings/ssh/new](https://github.com/settings/ssh/new)

---

## 🚀 Step 6: Use Correct Host When Cloning or Updating Repos

### For 90s-it Account

```bash
git clone git@github-90sit:90s-it/your-repo.git
```

Or update existing remote URL:

```bash
git remote set-url origin git@github-90sit:90s-it/your-repo.git
```

### For Nazmul-Islam-Naim Account

```bash
git clone git@github-naim:Nazmul-Islam-Naim/your-repo.git
```

Or update existing remote URL:

```bash
git remote set-url origin git@github-naim:Nazmul-Islam-Naim/your-repo.git
```

---

## 🛠 Useful SSH Commands

### List loaded keys

```bash
ssh-add -l
```

### Remove a key from agent

```bash
ssh-add -d ~/.ssh/id_ed25519
```

### Remove all keys from agent

```bash
ssh-add -D
```

---

## 🧪 Test SSH Connections

```bash
ssh -T git@github-90sit
ssh -T git@github-naim
```

Expected output:

```
Hi 90s-it! You've successfully authenticated, but GitHub does not provide shell access.
Hi Nazmul-Islam-Naim! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## 🧹 Optional: Rename or Remove Default SSH Key

### Rename

```bash
mv ~/.ssh/id_ed25519 ~/.ssh/id_ed25519_old
mv ~/.ssh/id_ed25519.pub ~/.ssh/id_ed25519_old.pub
```

### Delete

```bash
rm ~/.ssh/id_ed25519 ~/.ssh/id_ed25519.pub
```

---

## ✅ You’re Ready!

Your system can now handle multiple GitHub accounts with different SSH keys smoothly 🎉.
