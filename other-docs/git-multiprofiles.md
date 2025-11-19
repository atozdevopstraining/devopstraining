You can easily configure **multiple GitHub profiles on the same local system**, each with its **own SSH key** (for example: work GitHub and personal GitHub).
Here is the clean and standard method.

---

# ✅ Step-by-Step: Multiple GitHub Profiles with Multiple SSH Keys

---

## **1. Create separate SSH keys**

Example: one for *personal*, one for *work*.

### Personal key:

```bash
ssh-keygen -t ed25519 -C "personal@example.com" -f ~/.ssh/id_ed25519_personal
```

### Work key:

```bash
ssh-keygen -t ed25519 -C "work@example.com" -f ~/.ssh/id_ed25519_work
```

This creates:

* `~/.ssh/id_ed25519_personal`
* `~/.ssh/id_ed25519_personal.pub`
* `~/.ssh/id_ed25519_work`
* `~/.ssh/id_ed25519_work.pub`

---

## **2. Add both keys to the SSH agent**

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519_personal
ssh-add ~/.ssh/id_ed25519_work
```

---

## **3. Add the public keys to GitHub accounts**

Copy each `.pub` key:

```bash
cat ~/.ssh/id_ed25519_personal.pub
cat ~/.ssh/id_ed25519_work.pub
```

Go to:
**GitHub → Settings → SSH and GPG Keys → Add SSH Key**

Add one key per account.

---

## **4. Configure SSH to use different keys based on hostname**

Edit SSH config file:

```bash
nano ~/.ssh/config
```

Add this:

```
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

---

## **5. Use the correct host in repository remotes**

### Personal repo:

```bash
git clone git@github.com-personal:yourpersonaluser/yourrepo.git
```

### Work repo:

```bash
git clone git@github.com-work:yourworkuser/yourrepo.git
```

If you already have a repo, update remote:

### Personal:

```bash
git remote set-url origin git@github.com-personal:yourpersonaluser/yourrepo.git
```

### Work:

```bash
git remote set-url origin git@github.com-work:yourworkuser/yourrepo.git
```

---

# ✔️ Done!

Now your machine will automatically use:

* **Personal SSH key** for personal repos
* **Work SSH key** for company repos

No conflicts, no switching accounts.

---

If you want, I can also help you set:

* Git user.email per repository
* Global + local gitconfig
* Auto-switch identity based on folder path

Just tell me!
