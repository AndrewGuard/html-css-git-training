# Git Merge Conflict Training Guide

This guide will help you train colleagues on how to handle merge conflicts using the colorful `index.html` page.

## Prerequisites
- Git installed and configured
- `index.html` file committed to the main branch

---

## Training Flow: Creating a Merge Conflict

### Step 1: Setup and Verify Main Branch
```bash
git checkout main
git status
```
Ensure the working directory is clean and you're on the main branch.

---

### Step 2: Person A (or Feature Branch) - Make First Change

**Create a new feature branch:**
```bash
git checkout -b feature-red-update
```

**Edit `index.html`:**
- Find the Red Section (around line 75)
- Change the paragraph to:
```html
<p>This is RED! Version from Feature Branch A.</p>
```

**Commit the change:**
```bash
git add index.html
git commit -m "Update red section from feature branch"
```

---

### Step 3: Person B (or Main Branch) - Make Conflicting Change

**Switch back to main:**
```bash
git checkout main
```

**Edit the SAME line in `index.html`:**
- Find the Red Section (same location)
- Change the paragraph to:
```html
<p>This is CRIMSON! Version from Main Branch B.</p>
```

**Commit the change:**
```bash
git add index.html
git commit -m "Update red section from main branch"
```

---

### Step 4: Trigger the Merge Conflict! 🔥

**Attempt to merge the feature branch:**
```bash
git merge feature-red-update
```

**Expected output:**
```
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

**Check the status:**
```bash
git status
```

---

### Step 5: Examine the Conflict

**Open `index.html` and look for conflict markers:**

```html
<div class="box red-box">
    <h2>Red Section</h2>
<<<<<<< HEAD
    <p>This is CRIMSON! Version from Main Branch B.</p>
=======
    <p>This is RED! Version from Feature Branch A.</p>
>>>>>>> feature-red-update
</div>
```

**Explanation of markers:**
- `<<<<<<< HEAD` - Start of your current branch's version
- `=======` - Separator between the two versions
- `>>>>>>> feature-red-update` - End of the incoming branch's version

---

### Step 6: Resolve the Conflict

**Choose ONE of these resolution strategies:**

**Option 1: Keep the current branch (main) version**
```html
<p>This is CRIMSON! Version from Main Branch B.</p>
```

**Option 2: Keep the incoming branch version**
```html
<p>This is RED! Version from Feature Branch A.</p>
```

**Option 3: Combine both (most common in real scenarios)**
```html
<p>This is RED and CRIMSON! Combined from both branches.</p>
```

**Option 4: Write something completely new**
```html
<p>Merge conflict resolved - this is the final version!</p>
```

**Important:** Remove ALL conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)

---

### Step 7: Complete the Merge

**Stage the resolved file:**
```bash
git add index.html
```

**Check the status:**
```bash
git status
```
Should show: "All conflicts fixed but you are still merging."

**Complete the merge with a commit:**
```bash
git commit -m "Resolve merge conflict in red section"
```

Or just:
```bash
git commit
```
(Git will auto-generate a merge commit message)

---

### Step 8: Verify and Visualize

**View the merge in the git log:**
```bash
git log --graph --oneline --all
```

**Test the page:**
Open `index.html` in a browser to verify it still works correctly.

---

## Additional Training Scenarios

### Scenario 2: Multiple Conflicts
Create conflicts in multiple colored sections simultaneously:
- Branch A: Modify Red, Yellow, and Green sections
- Main: Modify the same Red, Yellow, and Green sections differently
- Practice resolving multiple conflicts in one merge

### Scenario 3: CSS Conflicts
```css
/* Branch A changes .red-box background-color to: */
background-color: crimson;

/* Main changes .red-box background-color to: */
background-color: darkred;
```

### Scenario 4: Three-Way Merge Conflict
1. Create two feature branches from main
2. Merge one into main
3. Try to merge the second (which also changed the same lines)

---

## Useful Git Commands During Training

```bash
# Abort a merge if you want to start over
git merge --abort

# See what branches exist
git branch -a

# Visualize the branch structure
git log --graph --oneline --all --decorate

# See the difference between branches
git diff main..feature-red-update

# Check which files have conflicts
git status

# See the conflicted content
git diff
```

---

## Common Mistakes to Teach

1. **Forgetting to remove conflict markers** - Page will display them!
2. **Not staging the file after resolving** - Can't complete the merge
3. **Committing before resolving all conflicts** - Git won't allow it
4. **Accidentally deleting too much code** - Use `git merge --abort` to start over

---

## Tips for Trainers

- 🎨 Use different colored sections for different students/teams
- 👥 Have pairs work on separate machines to simulate real collaboration
- 🖥️ Project the terminal output on a screen so everyone can follow
- ✅ After each resolution, open the HTML file to show it still renders
- 📝 Encourage trainees to document their resolution decisions
- 🔄 Repeat the exercise multiple times with different scenarios

---

## Going Further

Once comfortable with merge conflicts, introduce:
- **Rebase conflicts:** `git rebase` instead of `git merge`
- **Cherry-pick conflicts:** `git cherry-pick`
- **Stash conflicts:** `git stash apply`
- **Three-way merge tools:** `git mergetool`
- **Visual tools:** GitKraken, SourceTree, VS Code's merge editor

---

## Quick Reference Card

```bash
# Setup conflict
git checkout -b feature-branch
# Edit file
git commit -am "Feature change"
git checkout main
# Edit same line
git commit -am "Main change"
git merge feature-branch  # CONFLICT!

# Resolve conflict
# 1. Edit file, remove markers
# 2. git add <file>
# 3. git commit

# Emergency escape
git merge --abort
```

---

**Happy Git Training! 🚀**

Remember: Merge conflicts are normal and part of collaborative development. The goal is to make your trainees comfortable resolving them, not afraid of them!
