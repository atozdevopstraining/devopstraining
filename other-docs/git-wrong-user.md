If **Git is taking the wrong username**, it means one of these is wrong:

* Global Git config
* Local repo Git config
* Your SSH key is linked to another GitHub account
* Credential manager stored wrong username

Below are all fixes depending on the cause.

---

# ✅ **1. Check what username Git is using**

Run:

```sh
git config --global user.name
git config --global user.email
```

Then check local repo settings:

```sh
git config --local user.name
git config --local user.email
```

If local and global conflict → **local overrides global**.

---

# ✅ **2. Fix Git username globally**

```sh
git config --global user.name "Correct Name"
git config --global user.email "correct-email@example.com"
```

---

# ✅ **3. Fix Git username only for the current repository**

(In repo folder)

```sh
git config user.name "Correct Name"
git config user.email "correct-email@example.com"
```

---

# ⚠️ **4. If GitHub shows commits under the wrong user**

This happens if:

* You used an email **not added** to your GitHub account
* You used someone else’s GPG/SSH identity

Fix: Add the email you used into GitHub:

GitHub → Settings → Emails → **Add Email**

---

# ⚠️ **5. If SSH is using the wrong GitHub account**

Check which account SSH is logging in as:

```sh
ssh -T git@github.com
```

If output says:

```
Hi wronguser! You've successfully authenticated...
```

Then Git is using a **different SSH key**.

### 👉 Fix: Create SSH config

Edit `~/.ssh/config`:

```
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa
```

Replace `id_rsa` with your correct key.

---

# ⚠️ **6. If HTTPS stores wrong username in Credential Manager (Windows)**

Open:

**Control Panel → Credential Manager → Windows Credentials**

Find anything like:

```
git:https://github.com
```

Delete it.

Then push again → Git will ask for correct username/token.

---

# 💬 If you want, run these and paste the output:

```
git config --global user.name
git config --global user.email
git config user.name
git config user.email
ssh -T git@github.com
```

I’ll tell you exactly where the wrong name is coming from and how to fix it.
