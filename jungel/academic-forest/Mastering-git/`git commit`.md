Here's your **✅ `git commit` – Developer Cheat Sheet**:

---

## ✅ `git commit` – Developer Cheat Sheet

### 🔍 Purpose:

Save staged changes to the repo with a message.

---

### 📋 What It Can Do:

|Use Case|Command Example|Meaning|
|---|---|---|
|Basic commit|`git commit -m "msg"`|Commits staged changes with message|
|Add & commit in one|`git commit -am "msg"`|Stages **&** commits tracked files only|
|Edit last commit message|`git commit --amend -m "new msg"`|Fix the previous commit|
|Commit empty (marker)|`git commit --allow-empty -m "marker"`|Creates a commit without file changes|
|Commit with GPG signing|`git commit -S -m "secure commit"`|Sign commit (if GPG configured)|
|Bypass hooks|`git commit --no-verify -m "msg"`|Skips pre-commit hooks|

---

### ⚙️ Typical Workflow:

```bash
git add file.js
git commit -m "Add login feature"

# OR (for tracked files)
git commit -am "Quick fix"
```

---

## 🧑‍💻 Professional Use Case – Scenario

### 🧠 Context:

You:

- Fixed a bug in `auth.js`
    
- Forgot to update the commit message
    
- Need to quickly stage + commit tracked changes
    

```bash
git add auth.js
git commit -m "Fix: handle login failure"
# Forgot something?
git commit --amend -m "Fix: login error handler update"
```

---

### 🛠️ Advanced Use Cases + Scenarios

|Command Example|Scenario|
|---|---|
|`git commit -am "Hotfix"`|⚡ Quick patch on tracked files|
|`git commit --amend`|📝 Correct or add to your last commit|
|`git commit --allow-empty`|🔒 Add markers or semantic commits (like "release start")|
|`git commit --no-verify`|🧪 Skip hooks temporarily (not recommended for prod)|
|`git commit -S -m "Signed change"`|✅ Sign commits for audit/security|

---

### ✅ Final Tips:

- Keep messages **clear and conventional** (`feat:`, `fix:`, etc.)
    
- Use `--amend` to fix mistakes instead of adding a new commit
    
- Use tools like **commitizen** or **conventional commits** for standardization
    

---

Want a version with visual examples or PDF?