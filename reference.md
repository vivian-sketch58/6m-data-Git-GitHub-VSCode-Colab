# Git/GitHub Command Cheat Sheet
## OS-Specific Quick Reference for Learners

---

## TERMINAL BASICS (Know Your Shell First)

### Mac Users
```bash
# Check your shell
echo $SHELL
# You'll see: /bin/bash or /bin/zsh (both work fine)

# Open Terminal: Cmd + Space → type "Terminal" → Enter
```

### Windows Users (PowerShell)
```powershell
# PowerShell is built-in (recommended, modern syntax)
# Open: Press Windows Key → type "PowerShell" → Enter

# OR use Git Bash (installed with Git)
# More similar to Mac syntax; optional
```

### Windows ARM Users
```powershell
# Same as Windows PowerShell
# Note: Git operations may be ~5-10% slower on ARM
# This is normal; don't worry
```

---

## GIT SETUP (Do This ONCE, First Time)

### All OS
```bash
# Check if Git is installed
git --version
# Should show: git version 2.x.x

# Configure your identity (required before first commit)
git config --global user.name "Your Name"
git config --global user.email "your.email@gmail.com"

# Verify configuration
git config --global --list
# Look for: user.name=Your Name, user.email=your.email@gmail.com
```

---

## SECTION 1: GIT ESSENTIALS (Local Repository)

### Create Your First Repo
```bash
# Create folder
mkdir ~/bootcamp_practice
cd ~/bootcamp_practice

# Initialize Git (creates hidden .git folder)
git init
# Output: Initialized empty Git repository in /Users/yourname/bootcamp_practice/.git/

# Check status (shows current state)
git status
# Output: On branch master, No commits yet
```

### Create & Commit Your First File

#### Mac/Linux
```bash
# Create a simple Python file
cat > data_analysis.py << 'EOF'
def load_data(file_path):
    """Load data from CSV"""
    import pandas as pd
    return pd.read_csv(file_path)
EOF

# OR open your editor:
code data_analysis.py  # Opens VS Code
# Type the Python code above, save
```

#### Windows PowerShell
```powershell
# Create file using PowerShell
@'
def load_data(file_path):
    """Load data from CSV"""
    import pandas as pd
    return pd.read_csv(file_path)
'@ | Out-File -Encoding UTF8 data_analysis.py

# OR open VS Code
code data_analysis.py
# Type code, save
```

### Stage & Commit
```bash
# Check status (see your new file)
git status
# Output: Untracked files: data_analysis.py

# Stage the file (prepare for commit)
git add data_analysis.py

# Check status again (file is now staged)
git status
# Output: Changes to be committed: data_analysis.py

# Commit (save to history)
git commit -m "Initial data loading function"
# Output: 1 file changed, 4 insertions(+), create mode 100644 data_analysis.py

# View commit history
git log
# Shows: commit hash, author, date, message

# Shorter view
git log --oneline
# Shows one line per commit (easier to read)
```

### Make Changes (2nd & 3rd Commit)

#### Mac/Linux
```bash
# Edit the file
echo "" >> data_analysis.py
echo "# Second version: added error handling" >> data_analysis.py

# OR open in editor:
code data_analysis.py
# Add a comment, save
```

#### Windows PowerShell
```powershell
# Edit the file
Add-Content -Path data_analysis.py -Value "`n# Second version: added error handling"

# OR open in editor:
code data_analysis.py
# Add a comment, save
```

### Commit Again
```bash
# Check status (file is "modified")
git status

# Stage & commit
git add data_analysis.py
git commit -m "Add error handling comments"

# Repeat ONE more time to have 3 commits
# Edit file again → git add → git commit -m "Your message"

# View all 3 commits
git log --oneline
# Output:
# abc1234 Add error handling comments
# def5678 Initial data loading function
# (earlier commits if any)
```

---

## SECTION 2: GITHUB & GITHUB INTEGRATION

### Create Remote Repository on GitHub

1. **Go to github.com** (must be logged in)
2. **Click "+" icon** (top right) → "New repository"
3. **Fill in:**
   - Repository name: `bootcamp-practice` (use hyphens, not spaces)
   - Description: "Learning Git for data science bootcamp"
   - Visibility: **Public** (easier for learning)
   - **Do NOT** initialize with README (we'll push our existing code)
4. **Click "Create repository"**
5. **Copy the HTTPS URL** (visible on next screen)
   - Looks like: `https://github.com/yourname/bootcamp-practice.git`

### Connect Local to Remote & Push

```bash
# Add remote connection (origin = your GitHub repo)
git remote add origin https://github.com/yourname/bootcamp-practice.git
# (Replace 'yourname' with your GitHub username)

# Rename default branch to 'main' (modern standard)
git branch -M main

# Push your commits to GitHub (first time with -u flag)
git push -u origin main
# Output: Counting objects, Compressing objects, Writing objects...
# After ~5 seconds: [new branch main → main]

# Verify: Go to github.com, refresh your repo page
# You should see your data_analysis.py file & commit history!
```

### Verify Push Worked
- Navigate to: `https://github.com/yourname/bootcamp-practice`
- You should see:
  - Your `data_analysis.py` file in the repo
  - Commit history on the left (3 commits)
  - Green checkmark next to filenames ✓

---

## VS CODE GIT INTEGRATION (GUI Instead of Terminal)

### Open Project in VS Code
```bash
# Navigate to your project folder
cd ~/bootcamp_practice

# Open in VS Code
code .
# (The dot means "open current folder")

# OR open VS Code → File → Open Folder → select bootcamp_practice
```

### Use Source Control Panel

**Location:** Left sidebar → icon with 3 circles (Source Control)

**Workflow:**

1. **Edit a file** (e.g., README.md)
   - Create new file: README.md
   - Add text: "# My Data Science Project"
   - Save (Cmd/Ctrl + S)

2. **Stage in VS Code**
   - Source Control panel shows your changed files
   - Hover over filename → click **+** button to stage
   - (Equivalent to `git add`)

3. **Commit in VS Code**
   - Type message in **Message** box at top of Source Control
   - Message: "Add project README"
   - Click **checkmark** button (or Ctrl + Enter)
   - (Equivalent to `git commit -m "..."`

4. **Push in VS Code**
   - Click "Sync Changes" button (bottom left)
   - OR click "..." (three dots) in Source Control → "Push"
   - (Equivalent to `git push`)

5. **Verify on GitHub**
   - Refresh github.com/yourname/bootcamp-practice
   - Your README.md now appears in the repo
   - Commit history shows your new commit

---

## SECTION 3: BRANCHING & PULL REQUESTS

### Create a Feature Branch

#### Terminal Method
```bash
# Create and switch to new branch
git checkout -b feature/add-preprocessing
# Output: Switched to a new branch 'feature/add-preprocessing'

# Verify you're on new branch
git branch
# Output:
#   feature/add-preprocessing  ← current (marked with *)
#   main
```

#### VS Code Method
- Source Control panel → click branch name (bottom left)
- Type new branch name: `feature/add-preprocessing`
- Select "Create new branch from main"
- Automatically switches to new branch

### Make Changes on Feature Branch
```bash
# Add new function to data_analysis.py
code data_analysis.py

# Add this function:
"""
def preprocess_data(df):
    '''Remove nulls, normalize columns'''
    return df.dropna().fillna(0)
"""

# Save file
# Stage & commit in VS Code (or terminal)
git add data_analysis.py
git commit -m "Add preprocessing function"
```

### Push Branch to GitHub
```bash
# Push this branch to GitHub
git push -u origin feature/add-preprocessing
# Output: [new branch feature/add-preprocessing → feature/add-preprocessing]

# Verify on GitHub: Refresh page
# You should see dropdown: "main" vs "feature/add-preprocessing"
```

### Create Pull Request (PR) on GitHub

1. **Go to github.com/yourname/bootcamp-practice**
2. **You'll see a banner:** "Compare & pull request" (yellow button)
3. **Click it** → fills in PR form
4. **Add description:** "Adds preprocessing function to handle null values"
5. **Click "Create pull request"**
6. **On PR page, click "Merge pull request"** → "Confirm merge"

### Merge Conflict Demo (Intentional)

**Setup (2 people needed):**

```bash
# Partner A: Edit main_analysis.py line 5
git checkout -b feature/threshold-low
# Edit: threshold = 0.5
git add main_analysis.py
git commit -m "Set low threshold"
git push -u origin feature/threshold-low
# Create PR on GitHub → Merge

# Partner B: Edit same file, same line (before A's merge)
git checkout -b feature/threshold-high
# Edit: threshold = 0.75
git add main_analysis.py
git commit -m "Set high threshold"
git push -u origin feature/threshold-high
# Try to create PR → CONFLICT!

# Resolve conflict in VS Code:
git checkout main
git pull origin main
git checkout feature/threshold-high
git merge main
# Conflict markers appear in file
# <<<<<< HEAD
# threshold = 0.75  ← Partner B's version
# =======
# threshold = 0.5   ← Partner A's version (merged)
# >>>>>> main

# Choose which version to keep (delete conflict markers)
# threshold = 0.75  # Keep Partner B's version (or negotiate)

# Save, stage, commit
git add main_analysis.py
git commit -m "Resolve merge conflict: chose high threshold"
git push origin feature/threshold-high
# Now PR merges successfully!
```

---

## COLAB + GITHUB INTEGRATION

### Clone Repo in Colab

1. **Open Google Colab:** colab.research.google.com
2. **Create new notebook**
3. **First cell:**
```python
# Clone your GitHub repo
!git clone https://github.com/yourname/bootcamp-practice.git

# List files
!ls bootcamp-practice/
# Output: data_analysis.py, README.md, etc.
```

4. **Import & use your code:**
```python
# Add repo to path
import sys
sys.path.insert(0, '/content/bootcamp-practice')

# Import your function
from data_analysis import load_data

# Use it
# data = load_data('your_file.csv')
```

### Push Changes Back from Colab (Optional)

```python
# In Colab cell:
!cd /content/bootcamp-practice && git config user.email "your@email.com"
!cd /content/bootcamp-practice && git config user.name "Your Name"

# Make changes (create new file)
with open('/content/bootcamp-practice/new_analysis.py', 'w') as f:
    f.write("# Analysis from Colab\nprint('Hello from Colab')")

# Commit & push
!cd /content/bootcamp-practice && git add new_analysis.py
!cd /content/bootcamp-practice && git commit -m "Add Colab analysis"
!cd /content/bootcamp-practice && git push https://yourname:YOUR_GITHUB_TOKEN@github.com/yourname/bootcamp-practice.git main
```

**Note:** For push to work, you need GitHub Personal Access Token (PAT) instead of password.

---

## TROUBLESHOOTING QUICK FIXES

### ❌ "fatal: not a git repository"
```bash
# You're not in a Git project folder
# Solution: cd to your project folder first
cd ~/bootcamp_practice
git status  # Should work now
```

### ❌ "git config not set"
```bash
# You haven't configured name/email
# Solution:
git config --global user.name "Your Name"
git config --global user.email "your.email@gmail.com"
git commit -m "Try again"
```

### ❌ "Permission denied" during push
```bash
# GitHub authentication failed (SSH or HTTPS)
# Solution: Use HTTPS instead, GitHub will prompt for password
git remote remove origin
git remote add origin https://github.com/yourname/repo.git
git push -u origin main
```

### ❌ "Branch already exists"
```bash
# You tried to create a branch that's already there
# Solution: Switch to existing branch
git checkout feature/add-preprocessing
# (Instead of git checkout -b feature/add-preprocessing)
```

### ❌ "Merge conflict" (see scary markers)
```bash
# This is NORMAL; it means Git couldn't auto-merge
# Solution:
# 1. Open file in VS Code
# 2. Choose which version you want (delete conflict markers)
# 3. git add file.py
# 4. git commit -m "Resolve conflict"
# 5. git push
```

### ❌ "Changes would be overwritten by merge"
```bash
# You have uncommitted changes
# Solution: Save your work first
git add .
git commit -m "Save work before pulling"
git pull
```

---

## QUICK COMMAND REFERENCE (Clipboard-Ready)

```bash
# Initial setup (once)
git config --global user.name "Your Name"
git config --global user.email "your.email@gmail.com"

# Create repo
git init
git add .
git commit -m "Initial commit"

# Connect to GitHub
git remote add origin https://github.com/yourname/repo.git
git branch -M main
git push -u origin main

# Everyday workflow
git status                          # What changed?
git add filename.py                 # Stage specific file
git add .                          # Stage all files
git commit -m "Your message"        # Save to history
git push                            # Send to GitHub
git pull                            # Get latest from GitHub

# Branching
git branch                          # List all branches
git checkout -b feature/name        # Create & switch to new branch
git checkout main                   # Switch to main
git merge feature/name              # Merge branch into main

# View history
git log                             # Full commit history
git log --oneline                   # Short version
git log --graph --all --oneline     # Visual branch history

# Undo (be careful!)
git restore filename.py             # Undo changes to a file
git reset HEAD filename.py          # Unstage a file
git revert commit-hash              # Undo a commit (safe)
```

---

## FREQUENTLY ASKED QUESTIONS (FAQ)

**Q: What's the difference between `git add` and `git commit`?**
A: `git add` = "Mark these files for saving" (staging). `git commit` = "Actually save to history." Think: add = shopping cart, commit = checkout.

**Q: Do I have to use the terminal? Can I use VS Code GUI?**
A: Yes! VS Code Source Control panel does everything. Terminal is optional. Use whichever feels comfortable.

**Q: What if I mess up and make a bad commit?**
A: Don't panic. You can use `git revert` to undo it safely, or `git reset` to go back. Ask a TA; it's recoverable.

**Q: Can I switch branches with uncommitted changes?**
A: No (usually). Solution: `git add .` and `git commit` first, OR `git stash` to temporarily hide changes.

**Q: How do I delete a branch I don't need?**
A: `git branch -d branch-name` (local) or GitHub UI "Delete branch" button (remote).

**Q: What if my merge conflict looks scary?**
A: It's normal! Just choose which version you want, delete the conflict markers, save, and commit. TAs are here to help.

**Q: Can I use GitHub without the terminal?**
A: Yes. GitHub Desktop app (github.com/desktop) is a full GUI. Or use VS Code Source Control. Terminal is optional.

---

## KEYBOARD SHORTCUTS (VS Code)

| Action | Mac | Windows/Linux |
|--------|-----|---------------|
| Open Source Control | Cmd + Shift + G | Ctrl + Shift + G |
| Save file | Cmd + S | Ctrl + S |
| Open Terminal in VS Code | Cmd + ` | Ctrl + ` |
| Stage/Unstage in Source Control | Click + or - button | Click + or - button |
| Commit | Cmd + Enter (in message box) | Ctrl + Enter (in message box) |

---

## RESOURCES

- **Git Official Docs:** git-scm.com (comprehensive, technical)
- **GitHub Guides:** guides.github.com (beginner-friendly)
- **VS Code Git Docs:** code.visualstudio.com/docs/editor/versioncontrol
- **Troubleshooting:** Stack Overflow (search "[git error message]")

---

# GIT TROUBLESHOOTING DECISION TREE
## Visual Flowchart for Learners (Print & Post in Classroom)

---

## SECTION 1: GIT SETUP & FIRST COMMITS

```
START: You're in terminal/PowerShell
    ↓
❌ Error: "command not found: git"?
├─ YES → Git is NOT installed
│        Solution: Run `git --version` to confirm
│        Ask instructor or TA for install link
├─ NO ✓ → Git is installed, continue
    ↓
❌ Trying to run `git init` but error says "not in a git repo"?
├─ YES → You're probably in WRONG FOLDER
│        Solution: Type `pwd` (Mac/Linux) or `cd` (Windows)
│                 Make sure you're in ~/bootcamp_practice
│                 Then run `git init` again
├─ NO ✓ → You successfully ran `git init`, continue
    ↓
❌ Error: "Author identity unknown"?
├─ YES → You skipped the config step
│        Solution: Run:
│                 git config --global user.name "Your Name"
│                 git config --global user.email "your@email.com"
│                 Then try `git commit` again
├─ NO ✓ → Config is set, continue
    ↓
✓ SUCCESS: Your file is committed!
   Next: Run `git log --oneline` to see your history
   Then: Go to SECTION 2 flowchart

```

---

## SECTION 2: PUSH TO GITHUB & VS CODE

```
START: You created a GitHub repo and have its URL
    ↓
❌ When you paste URL, do you see "SSH" or "HTTPS"?
├─ SSH (looks like: git@github.com:username/repo.git)
│  ├─ YES → Continue to SSH flowchart (below)
│  └─ NO → Stick with HTTPS, continue
│
├─ HTTPS (looks like: https://github.com/username/repo.git)
│  ├─ YES → Continue below ✓
│  └─ NO → Ask TA to help you identify URL type

    ↓ [Using HTTPS, continuing...]

❌ Error: "fatal: remote origin already exists"?
├─ YES → You already added this remote
│        Solution: Run `git remote remove origin`
│                 Then run `git remote add origin [URL]` again
├─ NO ✓ → Remote connection made, continue

    ↓

❌ Error: "Permission denied" or "401 Unauthorized"?
├─ YES → GitHub won't let you access (auth problem)
│        Solution: 
│        1. Try again (GitHub might be slow)
│        2. Use HTTPS instead of SSH
│        3. Ask TA if still failing
├─ NO ✓ → Authentication worked, continue

    ↓

✓ SUCCESS: `git push -u origin main` finished
   Next: Refresh github.com/yourname/repo
          Your code should now be visible online!
   Then: Continue to "VS Code Integration" section

---

## VS CODE INTEGRATION

START: You opened your project folder in VS Code
    ↓
❌ Do you see "Source Control" icon in left sidebar?
├─ NO → Not visible
│       Solution: 
│       1. Click left sidebar (4th icon from top, looks like 3 circles)
│       2. OR press Cmd+Shift+G (Mac) / Ctrl+Shift+G (Windows)
│       3. If still nothing: open your project folder first
│          File → Open Folder → select bootcamp_practice
├─ YES ✓ → Source Control panel is visible, continue

    ↓

❌ When you edit a file, does it appear in Source Control panel?
├─ NO → Your changes aren't being tracked
│       Solution:
│       1. Make sure you saved the file (Cmd/Ctrl+S)
│       2. Check: are you in a Git repo?
│          Terminal: `git status`
│          If error, you forgot `git init`
├─ YES ✓ → File changes are tracked, continue

    ↓

COMMITTING VIA VS CODE:
  1. Click file → hover → click "+" button (Stage)
  2. Type commit message in box at top
  3. Click checkmark (Commit)
  4. Click "Sync Changes" (Push to GitHub)

❌ After "Sync Changes," do you see success message?
├─ NO → Something went wrong
│       Solution: Scroll down in VS Code source control
│                 Read error message
│                 If unclear: screenshot to Slack
├─ YES ✓ → Push succeeded!

    ↓

✓ SUCCESS: Your VS Code commit is on GitHub
   Next: Go to SECTION 3 flowchart

```

---

## SECTION 3: BRANCHING & MERGE CONFLICTS

```
START: You're creating a feature branch
    ↓
❌ In VS Code, click branch name (bottom left)
   Are you seeing option to "Create Branch"?
├─ NO → Look for text showing current branch (prob "main")
│       Try again: Look for it in bottom left corner
├─ YES ✓ → Create branch dialog opened, continue

    ↓

CREATING BRANCH:
  Type name: `feature/add-preprocessing`
  Click "Create branch from main"
  
❌ Did it successfully switch to new branch?
├─ NO → Look at bottom left; still says "main"?
│       Click the text → select branch from dropdown
│       Choose your new feature branch
├─ YES ✓ → You're on feature branch, continue

    ↓

MAKE CHANGES ON BRANCH:
  1. Edit your code (add a function)
  2. Save (Cmd/Ctrl+S)
  3. Stage + Commit in VS Code (like before)
  4. Click "Sync Changes" to push branch

❌ Error: "branch doesn't exist yet"?
├─ YES → This is NORMAL
│        Solution: Check the checkbox "Publish branch"
│                 Or run: git push -u origin [branch-name]
├─ NO ✓ → Branch pushed successfully, continue

    ↓

CREATE PULL REQUEST (On GitHub):
  1. Go to github.com/yourname/repo
  2. Click "Compare & pull request" button (yellow)
  3. Add description (2 sentences is fine)
  4. Click "Create pull request"

    ↓

MERGING PULL REQUEST (On GitHub):
  1. On PR page, click "Merge pull request"
  2. Click "Confirm merge"
  3. Optional: "Delete branch" (cleans up)

    ↓

---

## MERGE CONFLICT RESOLUTION

START: You tried to merge two branches that edited same file
    ↓
YOU'LL SEE SCARY SYMBOLS:
  <<<<<<< HEAD
  your version of the code
  =======
  their version of the code
  >>>>>>> branch-name

STAY CALM! This is normal.

    ↓

RESOLVE:
  1. Open the file in VS Code
  2. Look at the two versions (above and below =====)
  3. Choose which one you want to keep
  4. DELETE the conflict markers: <<<<<<, =====, >>>>>>>
  5. Save (Cmd/Ctrl+S)
  6. Stage + Commit: "Resolve merge conflict"
  7. Push

    ↓

❌ VS Code shows conflict, but you don't see the conflict markers?
├─ YES → VS Code might be showing conflict UI
│        Click "Accept Current Change" or "Accept Incoming Change"
│        Let VS Code resolve it for you
├─ NO → You're looking at the raw conflict markers
│       Delete them manually (see step 4 above)

    ↓

✓ SUCCESS: Merge conflict resolved!
   Congratulations: You've completed Git workflow mastery!

```

---

## QUICK ERROR LOOKUP TABLE

| Error Message | Cause | Fix |
|---------------|-------|-----|
| `fatal: not a git repository` | Not in a Git folder | `cd ~/bootcamp_practice` then try again |
| `fatal: remote already exists` | Already added GitHub connection | `git remote remove origin` then re-add |
| `Permission denied (publickey)` | SSH authentication failed | Use HTTPS instead: `git remote set-url origin https://...` |
| `Author identity unknown` | Skipped `git config` step | Run `git config --global user.name "Name"` & `user.email` |
| `Could not open a connection` | Wi-Fi issues | Check internet. Try again in 30 sec. |
| `Merge conflict in [file]` | Two people edited same line | See MERGE CONFLICT section above |
| `no changes added to commit` | Forgot `git add` | Run `git add filename` then `git commit` |
| `branch doesn't exist on remote` | Branch not pushed yet | Run `git push -u origin [branch-name]` |
| `Your branch is ahead of 'origin/main'` | Local changes not pushed | Run `git push` |
| `Your branch is behind 'origin/main'` | Remote has newer code | Run `git pull` |

---

## DECISION TREE: "I Don't Know What's Wrong"

```
START: Something broke
    ↓
Step 1: Read the ERROR MESSAGE carefully
        └─ What's the KEY WORD? (denied, not found, conflict, etc.)
           Look it up in the table above

    ↓
Step 2: If not in table, try ONE of:
        ├─ `git status` (what's the current state?)
        ├─ `git log --oneline` (do your commits exist?)
        ├─ `git branch` (which branch are you on?)
        └─ `git remote -v` (is GitHub connection set up?)

    ↓
Step 3: Still stuck?
        ├─ Screenshot the error
        ├─ Paste in Slack
        ├─ Tag @TA
        └─ They'll help in <5 min

```

---

## COMMON QUESTIONS (Not Errors, Just Confusion)

**Q: What does `git add` do?**
A: Marks files you want to include in the next commit (like adding items to a shopping cart).

**Q: What's the difference between local and remote?**
A: Local = your laptop. Remote = GitHub server in the cloud.

**Q: Do I HAVE to use branches?**
A: Not for solo projects. But for team projects: YES (keeps people out of each other's hair).

**Q: What if I made a mistake and committed the wrong thing?**
A: No problem. Use `git revert [commit-hash]` to undo it safely. Ask TA for details.

**Q: Can I switch branches if I have uncommitted changes?**
A: Usually no. First: `git add .` and `git commit`, then switch.

**Q: How do I delete a branch I don't need?**
A: `git branch -d [branch-name]` (local) or GitHub UI "Delete branch" (remote).

---

## BEFORE YOU PANIC

Remember:
- Git is designed to PREVENT data loss (not cause it)
- Every error you see has been seen by millions of developers
- There is NO "unfixable" Git problem
- Worst case: delete folder and clone again (you'll have all commits from GitHub)

**Take a breath. Ask for help. You've got this.** 💪

---


