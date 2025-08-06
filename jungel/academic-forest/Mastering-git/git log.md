Here's the **📜 `git log` – Developer Cheat Sheet**, displayed right here:

---

## 📜 `git log` – Developer Cheat Sheet

### 🔍 Purpose:

View the project history (**commits**) in various formats.

---

### 📋 What It Can Do:

|Use Case|Command Example|Meaning|
|---|---|---|
|Show full log|`git log`|Default detailed commit history|
|Compact log|`git log --oneline`|One-line summary per commit|
|Log with graph|`git log --graph --oneline --all`|Shows commit tree structure|
|Log with file changes|`git log -p file.txt`|Shows diffs for file changes|
|Log for specific author|`git log --author='Alice'`|Filter commits by author|
|Log for a specific file|`git log -- file.js`|Show commits that changed a specific file|

---

### ⚙️ Typical Workflow:

```bash
# View history
git log

# View short summary
git log --oneline

# View changes made in each commit
git log -p

# View history of a file
git log -- file.txt
```

---

## 🧑‍💻 Professional Use Case – Full Scenario

### 🧠 Context:

You're investigating a production bug. You need to:

- Find the last commit that changed `server.js`
    
- Understand what changed (diff)
    
- See who made the change
    

```bash
git log -p server.js
```

---

### 🛠️ Advanced Use Cases + Scenarios

|Command Example|Scenario|
|---|---|
|`git log --oneline`|📄 Quickly scan commit history|
|`git log --graph --all`|🌳 View complete commit tree (all branches)|
|`git log --author='Bob'`|👤 Track commits by a specific team member|
|`git log --since='2 weeks ago'`|📅 Find recent changes only|
|`git log -S'configValue'`|🔍 Find commits that added/removed a specific string|
|`git log -- file.js`|📁 Check history of a specific file|

---

### ✅ Final Tips:

- Use `--oneline` + `--graph` to **visualize branch history**
    
- Use `-S<string>` to **trace code changes**
    
- Great for **debugging**, **tracking regressions**, and **auditing code**
    

---

Let me know if you want it summarized even further for a sticky note version.