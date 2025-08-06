Absolutely! Here's the enhanced version of the **`git restore` cheat sheet**, now with real-world scenarios for every advanced use case.

---

## ♻️ `git restore` – Developer Cheat Sheet

### 🔍 Purpose:

Safely undo changes in **working directory** or **staging area**.

---

### 📋 What It Can Do:

|Use Case|Command Example|Meaning|
|---|---|---|
|Discard local file changes|`git restore file.js`|Reverts file to last committed version|
|Unstage a file|`git restore --staged file.js`|Removes file from staging area, keeps changes|
|Discard both|`git restore --source=HEAD --staged --worktree file.js`|Full reset (dangerous!)|

---

### ⚙️ Typical Workflow:

```bash
# Edited file by mistake
git restore file.js

# Staged wrong file
git restore --staged config.json

# Undo everything in current dir
git restore . 
```

---

## 🧑‍💻 Professional Use Case – Full Scenario

### 🧠 Context:

You're working on a hotfix branch. You:

- Accidentally edited `main.js`
    
- Staged `env.config.js` too early
    
- Need to pull a file from an older commit
    

---

### 🛠️ Advanced Use Cases + Scenarios

|Command Example|Scenario|
|---|---|
|`git restore .`|🧹 You made many local changes during testing; want to discard them all and reset working directory.|
|`git restore --staged .`|🧼 You ran `git add .` by mistake and want to unstage everything before committing.|
|`git restore --source=<commit> app.js`|🕰️ You need to restore `app.js` to the state it was in **two commits ago** (e.g., bug-free version).|
|`git restore --worktree style.css`|👁️ You staged changes to `style.css` but want to undo local working changes only, leaving staging intact.|
|`git restore --staged --worktree utils.js`|🚫 You edited and staged `utils.js` by mistake — want to **completely undo everything** about that change.|

---

### ✅ Final Tips

- Use `git status` **before and after** to verify.
    
- Great for fixing accidental changes and resets.
    
- Safe alternative to risky `checkout` for undoing.
    

---

Let me know if you want this as a downloadable `.md` or `.pdf`!