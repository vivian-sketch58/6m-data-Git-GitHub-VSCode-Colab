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

