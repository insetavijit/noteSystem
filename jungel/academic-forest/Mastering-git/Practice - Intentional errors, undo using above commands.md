# 🎯 Git Undo Practice Guide - Complete Solutions

_A beginner-friendly guide to mastering Git's undo commands with clear explanations and practical examples._

---

## 🚀 Getting Started

Before diving into the exercises, let's set up our practice environment:

```bash
mkdir git-undo-practice && cd git-undo-practice
git init
echo "line 1" > notes.txt
git add .
git commit -m "Initial commit"
```

**What this does:** Creates a new directory, initializes a Git repository, creates a simple text file, and makes our first commit to work with.

---

## 📚 Understanding Git's Undo Commands

Before we start practicing, here's what each command does:

- **`git reset`** - Moves your current branch to a different commit (like time travel)
- **`git revert`** - Creates a new commit that undoes previous changes (safe for shared code)
- **`git checkout`** - Switches branches or restores files from different commits
- **`git restore`** - Modern way to discard changes or unstage files
- **`git reflog`** - Shows a history of where your HEAD has been (your safety net!)

---

## 1️⃣ Git Reset - Time Travel for Your Commits

_Think of `git reset` as a time machine that can take your project back to any previous state._

### 🔧 Exercise 1: "Oops, I committed too early!"

**The Scenario:**

```bash
echo "draft" >> notes.txt
git add .
git commit -m "Wrong commit"
# Oh no! I wasn't ready to commit this yet!
```

**The Solution:**

```bash
git reset --soft HEAD~1
```

**What happens:**

- Your commit disappears from history
- BUT your changes stay exactly where they were (still staged and ready to commit)
- It's like you pressed "undo" on just the commit action

**When to use this:** When you committed too early but the changes are fine.

---

### 🔧 Exercise 2: "I staged the wrong file!"

**The Scenario:**

```bash
echo "update" >> notes.txt
git add notes.txt
# Wait, I don't want to stage this file yet!
```

**The Solution:**

```bash
git reset notes.txt
```

**What happens:**

- The file is removed from the staging area
- Your changes remain in the file, just not staged for commit
- Like taking something out of your shopping cart before checkout

**When to use this:** When you accidentally staged files you're not ready to commit.

---

### 🔧 Exercise 3: "Delete these commits completely!"

**The Scenario:**

```bash
touch file{1..3}.txt
git add . && git commit -m "Add files"
git commit --allow-empty -m "Another commit"
# These commits are completely wrong - I want them GONE!
```

**The Solution:**

```bash
git reset --hard HEAD~2
```

**What happens:**

- Moves back 2 commits in history
- **Permanently deletes** both the commits AND all changes
- Your working directory looks exactly like it did 2 commits ago

**⚠️ Warning:** This permanently destroys work! Only use when you're absolutely sure.

**When to use this:** When you want to completely remove commits and don't care about losing the changes.

---

## 2️⃣ Git Revert - The Safe Undo

_`git revert` is like adding a correction to a document instead of using whiteout. Everyone can see what you fixed._

### 🔧 Exercise 1: "This commit introduced a bug!"

**The Scenario:**

```bash
echo "bug" > bug.txt
git add . && git commit -m "Introduce bug"
# This commit caused problems - but others are already using this code!
```

**The Solution:**

```bash
git revert HEAD
```

**What happens:**

- Creates a brand new commit that undoes the bug commit
- Original history stays intact (important for shared repositories)
- It's like saying "Remember that bug I added? Here's a commit that removes it."

**When to use this:** When you need to undo changes in code that others might already have.

---

### 🔧 Exercise 2: "I need to undo a commit from the middle of history"

**The Scenario:**

```bash
git commit --allow-empty -m "Commit A"
git commit --allow-empty -m "Commit B (bad)"
git commit --allow-empty -m "Commit C"
# Only commit B is bad, but I want to keep A and C!
```

**The Solution:**

```bash
git log --oneline  # Find commit B's hash (looks like: abc1234)
git revert abc1234  # Replace with actual hash
```

**What happens:**

- Creates a new commit that only undoes commit B's changes
- Commits A and C remain untouched
- Like surgically removing just the bad parts

**When to use this:** When only one specific commit in your history is problematic.

---

### 🔧 Exercise 3: "Multiple bad commits in a row"

**The Scenario:**

```bash
git commit --allow-empty -m "Bad 1"
git commit --allow-empty -m "Bad 2"
# Both of these commits are problems!
```

**The Solution:**

```bash
git revert HEAD HEAD~1
```

**What happens:**

- Creates two new commits that undo "Bad 2" then "Bad 1"
- Done in reverse order to avoid conflicts
- Original history preserved

**When to use this:** When several recent commits all need to be undone safely.

---

## 3️⃣ Git Checkout - File and Branch Switching

_`git checkout` is like having access to any version of your files from your project's history._

### 🔧 Exercise 1: "Restore a file from a previous version"

**The Scenario:**

```bash
echo "bad line" >> notes.txt
git commit -am "Corrupted file"
# The file is messed up, but it was perfect in the previous commit!
```

**The Solution:**

```bash
git checkout HEAD~1 -- notes.txt
```

**What happens:**

- Grabs `notes.txt` from one commit ago
- Replaces your current version with the old, good version
- Like copying from a backup

**When to use this:** When you need to restore a specific file to a previous state.

---

### 🔧 Exercise 2: "Browse your project's history"

**The Scenario:**

```bash
git log --oneline  # Pick any old commit hash
git checkout abc1234  # Replace with actual hash
# What does my project look like at this point in time?
```

**The Solution:**

```bash
git checkout abc1234  # Time travel to that commit
# Look around, check files, etc.
git checkout main     # Return to present
```

**What happens:**

- First command: You're now viewing your project exactly as it was at that commit
- Second command: Returns you to your current branch
- Like looking through old photo albums, then closing the album

**When to use this:** To investigate how your project looked at different points in history.

---

## 4️⃣ Git Restore - The Modern File Manager

_`git restore` is Git's newer, cleaner way to manage file changes._

### 🔧 Exercise 1: "I messed up this file - start over!"

**The Scenario:**

```bash
echo "mistake" >> notes.txt
# I made changes to this file that I don't want to keep
```

**The Solution:**

```bash
git restore notes.txt
```

**What happens:**

- Throws away all your unstaged changes to the file
- Restores it to exactly how it was in your last commit
- Like hitting "undo" until you're back to the last save

**When to use this:** When you want to discard changes you've made to a file.

---

### 🔧 Exercise 2: "Take this file out of staging"

**The Scenario:**

```bash
echo "stage me" >> file.txt
git add file.txt
# Actually, I don't want to include this in my next commit
```

**The Solution:**

```bash
git restore --staged file.txt
```

**What happens:**

- Removes the file from staging area
- Keeps your changes in the file, just unstaged
- Like taking something out of your shopping cart but keeping it in your hands

**When to use this:** When you staged files you're not ready to commit yet.

---

### 🔧 Exercise 3: "Get this file from a specific old commit"

**The Scenario:**

```bash
git log --oneline  # Find an old commit hash
# I want notes.txt from that specific old version
```

**The Solution:**

```bash
git restore --source=abc1234 notes.txt  # Replace with actual hash
```

**What happens:**

- Gets `notes.txt` from that specific commit
- Replaces your current version
- Like asking for a specific version from your project's archive

**When to use this:** When you need a file from a particular point in your project's history.

---

## 5️⃣ Git Reflog - Your Emergency Recovery Tool

_`git reflog` is like having a complete history of every action you've taken in Git. It's your ultimate safety net!_

### 🔧 Exercise 1: "I reset to the wrong commit!"

**The Scenario:**

```bash
git commit --allow-empty -m "Safe point"
git commit --allow-empty -m "Oops point" 
git reset --hard HEAD~1
# Wait! I wanted to keep "Oops point"!
```

**The Solution:**

```bash
git reflog                    # Shows: abc1234 Oops point
git reset --hard abc1234      # Replace with actual hash
```

**What happens:**

- `git reflog` shows you everywhere your HEAD has been
- You can see the "Oops point" commit is still there!
- Reset back to it like nothing happened

**When to use this:** When you've made a mistake with reset and need to recover.

---

### 🔧 Exercise 2: "I accidentally deleted a branch!"

**The Scenario:**

```bash
git checkout -b temp-branch
git commit --allow-empty -m "Important work"
git checkout main
git branch -D temp-branch
# Oh no! I deleted my branch with important work!
```

**The Solution:**

```bash
git reflog                                    # Find the "Important work" hash
git checkout -b temp-branch abc1234           # Recreate branch at that commit
```

**What happens:**

- Reflog shows you the commit from your deleted branch
- You recreate the branch pointing to that exact commit
- Your work is completely recovered!

**When to use this:** When you've accidentally deleted branches with important work.

---

### 🔧 Exercise 3: "Hard reset destroyed my work!"

**The Scenario:**

```bash
echo "important data" > important.txt
git add . && git commit -m "Add important file"
git reset --hard HEAD~1
# My important file is gone! 😱
```

**The Solution:**

```bash
git reflog                              # Find "Add important file" hash  
git reset --hard abc1234                # Restore everything
```

**What happens:**

- Reflog shows the commit with your important file
- Hard reset back to that commit restores everything
- Your file is back like magic!

**When to use this:** When hard reset has destroyed work you need to recover.

---

## 🎯 Quick Reference Cheat Sheet

|**Situation**|**Command**|**What it does**|
|---|---|---|
|Undo last commit, keep changes|`git reset --soft HEAD~1`|Removes commit, keeps files staged|
|Unstage files|`git reset filename` or `git restore --staged filename`|Moves files from staging to working directory|
|Completely delete commits|`git reset --hard HEAD~n`|⚠️ Permanently removes n commits and changes|
|Safely undo a commit|`git revert HEAD`|Creates new commit that undoes the changes|
|Discard file changes|`git restore filename`|Throws away unstaged changes to file|
|Restore file from old commit|`git checkout OLD_COMMIT -- filename`|Gets file from specific commit|
|Emergency recovery|`git reflog` then `git reset --hard HASH`|Recovers from almost any mistake|

---

## 🛟 Emergency Recovery Steps

If you think you've lost important work:

1. **Don't panic!** Git rarely loses data permanently
2. **Check reflog:** `git reflog` shows everywhere you've been
3. **Look for your work:** Find the commit hash with your important changes
4. **Recover:** `git reset --hard HASH` or `git checkout -b new-branch HASH`
5. **Remember:** Reflog entries expire after ~90 days, so don't wait too long!

---

## 💡 Pro Tips for Git Beginners

- **Always commit your work** before experimenting with these commands
- **Use `git status`** frequently to understand what's happening
- **Test these commands** in practice repositories first
- **`git reflog` is your friend** - it can recover almost anything
- **When in doubt, create a branch** before trying destructive operations
- **Soft reset (`--soft`)** is usually safer than hard reset (`--hard`)

Remember: Git is designed to help you, not hurt you. These tools are powerful, but with practice, they'll become natural parts of your workflow!