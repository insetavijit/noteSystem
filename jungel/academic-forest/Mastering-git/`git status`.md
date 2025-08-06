#6AUG25

---

## 🔧 `git status` – Developer Cheat Sheet

### 🔍 Purpose:

Shows the **current state** of your Git working directory and staging area.

---

### 📋 What It Shows:

|Section|Meaning|
|---|---|
|**Branch info**|Which branch you’re on|
|**Staged changes**|Files added with `git add`, ready for commit|
|**Unstaged changes**|Modified but _not_ yet staged|
|**Untracked files**|New files not tracked by Git|

---

### ⚙️ Typical Workflow:

```bash
# After making changes
git status

# After staging files
git add file.js
git status

# Before committing
git status
git commit -m "Meaningful message"
```

---

### 🧑‍💻 Professional Use Case – Real-World Scenario

#### 🧠 Context:

You're working on `feature/login-page`. You modified `login.html`, added `auth.js`, and accidentally changed `README.md`.

```bash
git status
```

**Output:**

```
On branch feature/login-page

Changes to be committed:
  modified:   login.html

Changes not staged for commit:
  modified:   README.md

Untracked files:
  auth.js
```

#### 🛠️ Actions:

- ✅ `login.html` is staged
    
- ❌ `README.md` needs review
    
- ⚠️ `auth.js` is missing from staging
    

```bash
git add auth.js
git restore README.md   # discard accidental change
git status              # confirm everything is clean
```

---

### 📊 Advanced Use Table

|Command|Description|
|---|---|
|`git status -s`|Short (compact) format|
|`git status --ignored`|Show ignored files|
|`git status --porcelain`|Machine-readable output (for scripts)|
|`git status -uno`|Hide untracked files|
|`watch git status`|Auto-refresh status (Linux/macOS)|

---

**Tip:** Use `git status` _constantly_ to avoid mistakes and ensure clean commits.