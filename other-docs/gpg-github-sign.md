Here is a **simple, clear guide** to:
1️⃣ Create a GPG key
2️⃣ Add it to GitHub
3️⃣ Enable Git signing
4️⃣ Sign commits & tags

---

# ✅ **1. Install GPG**

### **Linux / WSL**

```sh
sudo apt update
sudo apt install gnupg
```

### **Mac**

```sh
brew install gnupg
```

### **Windows**

Install **Gpg4win**:
[https://gpg4win.org/](https://gpg4win.org/)

---

# ✅ **2. Create a GPG Key**

Run:

```sh
gpg --full-generate-key
```

Choose the options:

1. **Key type:**
   Select: `1) RSA and RSA`

2. **Key size:**
   Type: `4096`

3. **Expiration:**
   Usually: `0` (no expiry)

4. **Name, Email:**
   Use the **same email as your GitHub account**
   Example: `test@example.com`

When asked for a passphrase → set a strong one.

---

# ✅ **3. List your GPG keys**

```sh
gpg --list-secret-keys --keyid-format=long
```

Output looks like:

```
sec   rsa4096/ABCD1234EFGH5678 2025-11-19
      uid   [ultimate] Your Name <you@example.com>
ssb   rsa4096/1122334455667788 2025-11-19
```

Your **GPG key ID** is:
➡️ `ABCD1234EFGH5678`

---

# ✅ **4. Export your public key**

GitHub needs your **public** key (not private).

```sh
gpg --armor --export ABCD1234EFGH5678
```

Copy the entire output:

```
-----BEGIN PGP PUBLIC KEY BLOCK-----
...
-----END PGP PUBLIC KEY BLOCK-----
```

---

# ✅ **5. Add GPG key to GitHub**

Go to:

**GitHub → Settings → SSH and GPG keys → New GPG key**
Paste your exported key.

---

# ✅ **6. Configure Git to use your GPG key**

### Set signing key

```sh
git config --global user.signingkey ABCD1234EFGH5678
```

### Enable auto-sign commits

```sh
git config --global commit.gpgsign true
```

### Set gpg program (Linux / Mac)

```sh
git config --global gpg.program gpg
```

### Windows (Gpg4win)

```sh
git config --global gpg.program "C:/Program Files (x86)/GnuPG/bin/gpg.exe"
```

---

# ✅ **7. Sign a commit**

```sh
git commit -S -m "My signed commit"
```

If auto-signing is enabled, just:

```sh
git commit -m "My commit"
```

Git will ask for your GPG passphrase.

---

# ✅ **8. Sign a git tag**

```sh
git tag -s v1.0.0 -m "Signed release tag"
```

Verify tag:

```sh
git tag -v v1.0.0
```

---

# 🔍 **9. Verify signature on GitHub**

Push your commits:

```sh
git push
```

On GitHub → the commit will show:

🟢 **Verified** badge (if everything is correct)

---

