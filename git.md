Here’s a concise guide showing how to use `git stash`, `git reset --hard`, `git reset --soft`, and a few related commands with examples. These commands are powerful tools for managing changes in your Git repository.

---

## 🔹 `git stash`

Temporarily save uncommitted changes (both staged and unstaged).

### Basic Usage:

```bash
git stash
```

### Examples:

**1. Stash changes and clean working directory:**

```bash
git stash
```

**2. Stash with a message:**

```bash
git stash save "WIP: fixing navbar"
```

**3. List stashed entries:**

```bash
git stash list
```

**4. Apply the most recent stash (but keep it in stash list):**

```bash
git stash apply
```

**5. Apply and remove the stash:**

```bash
git stash pop
```

**6. Apply a specific stash:**

```bash
git stash apply stash@{1}
```

**7. Drop (delete) a stash:**

```bash
git stash drop stash@{1}
```

**8. Clear all stashes:**

```bash
git stash clear
```

---

## 🔹 `git reset --hard`

Resets the **index and working directory** to a specified state. All changes are lost!

### Basic Usage:

```bash
git reset --hard <commit>
```

### Examples:

**1. Discard all changes and reset to last commit:**

```bash
git reset --hard HEAD
```

**2. Reset to a specific commit:**

```bash
git reset --hard a1b2c3d
```

**⚠️ Warning:** This will remove uncommitted and committed changes. Use with caution!

---

## 🔹 `git reset --soft`

Resets the **HEAD** to a previous commit, but **keeps changes staged**.

### Basic Usage:

```bash
git reset --soft <commit>
```

### Example:

**1. Move HEAD back but keep files staged:**

```bash
git reset --soft HEAD~1
```

Useful if you want to **amend a commit** or change the commit message.

---

## 🔹 `git reset --mixed` (default)

Resets HEAD and **unstages** files, but keeps changes in the working directory.

### Example:

```bash
git reset HEAD~1
```

Same as:

```bash
git reset --mixed HEAD~1
```

---

## 🔹 Comparing the three reset types:

| Command             | Resets HEAD | Unstages files | Removes file changes |
| ------------------- | ----------- | -------------- | -------------------- |
| `git reset --soft`  | ✅           | ❌              | ❌                    |
| `git reset --mixed` | ✅           | ✅              | ❌                    |
| `git reset --hard`  | ✅           | ✅              | ✅                    |


---

## ✅ Cherry Picking Example

Let's say you're on `main` and you want to apply a specific commit from `feature-branch` to `main`.

---

### 🧱 Setup:

```bash
# Start on main
git checkout main

# View log of feature-branch
git log feature-branch --oneline
```

You see this commit on `feature-branch`:

```
a1b2c3d Add login validation
```

You want to apply just that commit to `main`.

---

### 🍒 Cherry-pick the commit:

```bash
git cherry-pick a1b2c3d
```

This will:

* Apply the **exact changes** from `a1b2c3d` to your current branch (`main`)
* Create a new commit on `main` with the same message and diff

---

### 🧼 Resolve conflicts (if any):

If there are conflicts, Git will pause and let you fix them. After resolving:

```bash
git add .
git cherry-pick --continue
```

Or to abort:

```bash
git cherry-pick --abort
```

---

### 💡 Bonus: Cherry-pick multiple commits

```bash
git cherry-pick a1b2c3d f6g7h8i
```

Or a range:

```bash
git cherry-pick a1b2c3d^..f6g7h8i
```
