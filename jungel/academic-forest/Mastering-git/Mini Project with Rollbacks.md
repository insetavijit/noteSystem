# 🚧 Week 3 Mini Project: Git Rollback Simulation (Industry-Level)

## 🧩 Scenario

You're a developer on a collaborative **To-Do App** project in a team of engineers. The app is a CLI-based task manager using text files for simplicity. During development, you introduce bugs, merge flawed features, and accidentally delete critical files. Your goal is to fix these issues using **advanced Git undo techniques** (`reset`, `revert`, `checkout`, `restore`, `stash`, `reflog`, `rebase`, and `cherry-pick`) while maintaining a professional workflow suitable for a production environment.
gpt -=>Grock : #6AUG25

---

## 📁 Project Setup: `buggy-todo-app`

### ⚙️ Initial Setup Script

Run this script to initialize the repository consistently:

```bash
#!/bin/bash
mkdir buggy-todo-app && cd buggy-todo-app
git init
echo "# To-Do App CLI\nA simple CLI-based task manager." > README.md
git add README.md
git commit -m "Initial commit: project setup"
```

---

## 📋 Tasks & Git Challenges

Each task simulates a real-world scenario with advanced Git practices. Follow the steps and use the provided solutions to undo mistakes.

### 1. ✅ Initialize Repository & Base Commit

**Task:**

- Create the `buggy-todo-app` repository.
- Add `README.md` with a project description.
- Commit with message: `"Initial commit: project setup"`.

**Solution:**

```bash
mkdir buggy-todo-app && cd buggy-todo-app
git init
echo "# To-Do App CLI\nA simple CLI-based task manager.\n\n## Features\n- Add tasks\n- Mark tasks as complete\n- List tasks" > README.md
git add README.md
git commit -m "Initial commit: project setup"
```

**Explanation:** Initializes a Git repository and commits the `README.md` with a professional project description, setting the stage for further development.

---

### 2. 🧪 Add a Buggy Feature

**Task:**

- Create `todo.txt` with three tasks in an incorrect format (e.g., missing priority).
- Commit with message: `"feat: add basic todo list"`.
- **Mistake**: Realize the task format is wrong (e.g., tasks should have `[priority]` prefix).

**Solution:**

```bash
echo "Task 1: Buy groceries\nTask 2: Write code\nTask 3: Call team" > todo.txt
git add todo.txt
git commit -m "feat: add basic todo list"
# Mistake detected: tasks need [priority]
git reset --soft HEAD~1
echo "[High] Buy groceries\n[Medium] Write code\n[Low] Call team" > todo.txt
git add todo.txt
git commit -m "feat: add todo list with priorities"
```

**Explanation:** `git reset --soft HEAD~1` undoes the commit while keeping changes staged, allowing you to fix the task format and recommit. This is a common practice when catching errors before pushing to a shared repository.

---

### 3. 🔄 Fix a Logic Flaw with Interactive Rebase

**Task:**

- Create `todo_logic.md` describing a flawed task sorting algorithm (e.g., sorting by name instead of priority).
- Commit with message: `"docs: add sorting logic"`.
- **Mistake**: The logic is incorrect. Use `git rebase -i` to edit the commit.

**Solution:**

```bash
echo "## Task Sorting Logic\nSort tasks alphabetically by name." > todo_logic.md
git add todo_logic.md
git commit -m "docs: add sorting logic"
# Mistake: should sort by priority
git rebase -i HEAD~1
# Change 'pick' to 'edit' for the commit, save and exit
echo "## Task Sorting Logic\nSort tasks by priority (High > Medium > Low)." > todo_logic.md
git add todo_logic.md
git commit --amend --no-edit
git rebase --continue
```

**Explanation:** `git rebase -i HEAD~1` allows editing the last commit. By changing to `edit`, you can modify `todo_logic.md` and amend the commit, maintaining a clean history. This is an advanced practice for refining commits before sharing.

---

### 4. 📂 Recover a Deleted Critical File

**Task:**

- Accidentally delete `README.md`.
- Commit the deletion with message: `"chore: remove outdated README"`.
- **Mistake**: Realize `README.md` is critical. Recover it using `git restore`.

**Solution:**

```bash
rm README.md
git add README.md
git commit -m "chore: remove outdated README"
# Mistake: README is needed
git log --oneline  # Find hash of commit before deletion (e.g., Initial commit)
git restore --source=<initial-commit-hash> -- README.md
git add README.md
git commit -m "fix: restore critical README"
```

**Explanation:** `git restore --source=<initial-commit-hash> -- README.md` recovers the file from the commit before deletion. This is a robust way to restore files in a production environment without disrupting history.

---

### 5. 💼 Stash a Work-in-Progress Feature with Named Stashes

**Task:**

- Create `future_plan.txt` with plans for a new feature (e.g., task categories).
- Stash the changes with a descriptive name.
- Simulate switching to an urgent bugfix branch.

**Solution:**

```bash
echo "Future: Add task categories (Work, Personal, Urgent)" > future_plan.txt
git add future_plan.txt
git stash push -m "WIP: task categories feature"
git checkout -b hotfix-branch
# Simulate bugfix
echo "Fix: Handle empty task list" >> todo_logic.md
git add todo_logic.md
git commit -m "fix: handle empty task list"
git checkout main
git stash pop
git add future_plan.txt
git commit -m "feat: add task categories plan"
```

**Explanation:** `git stash push -m "WIP: task categories feature"` saves changes with a descriptive name, making it easier to manage multiple stashes in a team setting. `git stash pop` reapplies the stashed changes, a common practice for context-switching in fast-paced environments.

---

### 6. 🔁 Revert a Public Commit with Conflict Handling

**Task:**

- Create a commit with a broken feature: `"feat: broken sorting algorithm"`.
- Simulate pushing to a shared repository.
- **Mistake**: The feature breaks the app. Use `git revert` to undo it safely, handling potential merge conflicts.

**Solution:**

```bash
echo "Broken: Sort tasks by length of description" >> todo_logic.md
git add todo_logic.md
git commit -m "feat: broken sorting algorithm"
# Simulate push (in practice, you'd run `git push`)
# Mistake: feature is broken
git revert HEAD
# If conflicts arise, resolve manually in todo_logic.md
# Example resolution: keep priority-based sorting
git add todo_logic.md
git revert --continue
```

**Explanation:** `git revert HEAD` creates a new commit to undo the broken feature, preserving history for shared repositories. If conflicts occur, resolve them manually and use `git revert --continue`. This is critical for public repositories where history cannot be rewritten.

---

### 7. 🔍 Recover a Lost Commit with Reflog and Cherry-Pick

**Task:**

- Create a commit: `"feat: add task deletion"`.
- Simulate an accidental hard reset: `git reset --hard HEAD~1`.
- Recover the lost commit using `git reflog` and `cherry-pick` to reapply it selectively.

**Solution:**

```bash
echo "Feature: Delete tasks with 'rm' command" >> todo_logic.md
git add todo_logic.md
git commit -m "feat: add task deletion"
git reset --hard HEAD~1
# Recover the lost commit
git reflog  # Find hash of "feat: add task deletion"
git cherry-pick <task-deletion-hash>
```

**Explanation:** `git reflog` lists all HEAD movements, allowing recovery of the lost commit’s hash. `git cherry-pick <hash>` reapplies the commit, a powerful technique for selective recovery in complex histories.

---

### 8. 🌟 Advanced: Fix a Merge Conflict During Rebase

**Task:**

- Create a feature branch with conflicting changes.
- Merge it into `main`, introducing a conflict.
- Use `git rebase` to clean up history, resolving conflicts.

**Solution:**

```bash
git checkout -b feature-branch
echo "Sort tasks by due date" >> todo_logic.md
git add todo_logic.md
git commit -m "feat: sort by due date"
git checkout main
echo "Sort tasks by priority" >> todo_logic.md
git add todo_logic.md
git commit -m "feat: sort by priority"
git merge feature-branch  # Conflict occurs
# Resolve conflict: combine both sorting methods
echo "Sort tasks by priority, then due date" > todo_logic.md
git add todo_logic.md
git commit
# Clean up history with rebase
git checkout feature-branch
git rebase main
# Resolve conflict again in todo_logic.md
git add todo_logic.md
git rebase --continue
git checkout main
git merge feature-branch
```

**Explanation:** Merging introduces a conflict, which is resolved by combining changes. `git rebase main` rewrites the feature branch’s history to apply it cleanly on `main`, a common practice for maintaining linear histories in professional projects.

---

## 📦 Deliverables

1. **Repository**: A `buggy-todo-app` with at least 8 commits, including branches, merges, and undo operations.
2. **undo_summary.md**: A detailed summary of mistakes, Git commands used, and outputs.

**undo_summary.md Content:**

```markdown
# Undo Summary

## Mistakes & Fixes

1. **Buggy Feature (Task 2)**:
   - **Mistake**: Added `todo.txt` with incorrect task format.
   - **Fix**: Used `git reset --soft HEAD~1` to undo commit, fixed format, and recommitted.
   - **Outcome**: Clean commit with correct task format.

2. **Logic Flaw (Task 3)**:
   - **Mistake**: Committed flawed sorting logic in `todo_logic.md`.
   - **Fix**: Used `git rebase -i HEAD~1` to edit the commit and fix the logic.
   - **Outcome**: Updated commit with correct sorting logic.

3. **Deleted File (Task 4)**:
   - **Mistake**: Deleted `README.md` accidentally.
   - **Fix**: Used `git restore --source=<initial-commit-hash> -- README.md` to recover.
   - **Outcome**: Restored critical file without history loss.

4. **WIP Feature (Task 5)**:
   - **Mistake**: Uncommitted changes in `future_plan.txt` interrupted by urgent bugfix.
   - **Fix**: Used `git stash push -m "WIP: task categories feature"` and `git stash pop`.
   - **Outcome**: Preserved and reapplied WIP changes.

5. **Public Commit (Task 6)**:
   - **Mistake**: Pushed a broken sorting algorithm.
   - **Fix**: Used `git revert HEAD` to create an undo commit, resolving conflicts.
   - **Outcome**: Safely undid changes in shared repository.

6. **Lost Commit (Task 7)**:
   - **Mistake**: Hard reset removed a task deletion feature.
   - **Fix**: Used `git reflog` to find the commit and `git cherry-pick` to reapply it.
   - **Outcome**: Recovered lost feature.

7. **Merge Conflict (Task 8)**:
   - **Mistake**: Merge introduced conflicting sorting logic.
   - **Fix**: Resolved conflict during merge and used `git rebase` for clean history.
   - **Outcome**: Linear history with combined features.

## Git Outputs

### git log --oneline
```

(HEAD -> main) Merge branch 'feature-branch'  
feat: sort by priority  
feat: sort by due date  
feat: add task deletion  
Revert "feat: broken sorting algorithm"  
fix: handle empty task list  
fix: restore critical README  
feat: add todo list with priorities  
Initial commit: project setup

```

### git reflog
```

HEAD@{0}: merge feature-branch: Merge made by the 'recursive' strategy.  
HEAD@{1}: cherry-pick: feat: add task deletion  
HEAD@{2}: reset: moving to HEAD~1  
HEAD@{3}: commit: feat: add task deletion  
...

```

### git stash list
```

# Empty if all stashes popped

```

## Lessons Learned
- Use `git reset --soft` for local commit fixes, but prefer `git revert` for shared repositories.
- Named stashes (`git stash push -m`) improve traceability in collaborative projects.
- `git reflog` and `cherry-pick` are critical for recovering from destructive operations.
- Rebasing ensures clean, linear histories for easier code reviews.
```

---

## ⏱️ Estimated Time: 4–5 Hours

This project is designed to take longer due to its complexity and real-world relevance, suitable for a mid-level developer preparing for industry roles.

---

## 📡 Advanced Practices Incorporated

- **Named Stashes**: Used descriptive stash names for traceability, a best practice in teams.
- **Interactive Rebase**: Edited commits to maintain a clean history, common in professional workflows.
- **Cherry-Pick**: Selectively reapplied lost commits, useful for recovering specific changes.
- **Conflict Resolution**: Handled merge and rebase conflicts, mimicking real-world collaboration.
- **Structured Documentation**: `undo_summary.md` follows industry standards for auditability and clarity.
- **Setup Script**: Ensures consistent starting conditions, a practice used in CI/CD pipelines.

---

## 🛠️ Optional Enhancements

- **Starter Files**: I can generate a `.zip` with the initial repository state, including `README.md` and setup script.
- **Automated Testing**: Add a script to verify the repository state (e.g., check commit count, file contents).
- **CI/CD Integration**: Simulate a GitHub Actions workflow to validate undo operations.
- **Score Sheet**: Provide a self-assessment table for tracking task completion and correctness.

Let me know if you want any of these enhancements or additional tasks (e.g., simulating a squash merge or handling a detached HEAD state)!