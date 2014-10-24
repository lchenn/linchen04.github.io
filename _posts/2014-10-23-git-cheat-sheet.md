---
layout: post
title: "Git Cheat Sheet"
categories:
tags: "Linux"
---

### Git basics

Basic concepts

```bash
master # default development branch
origin # default upstream repository
HEAD  # Current branch
HEAD^ # Parent of HEAD
HEAD~4 # The great-great grandparent of HEAD
<commit>~1 # The previous commit of <commit>
<commit>~2 # The grandparent of <commit>
<commit>  # The first 7 chars can be used to identify a commit
```

Basic operations

```bash
# Shows files changed in working directory
$ git status
# Shows who changed what at when in a file
$ git blame <file>
# Checkouts a file from a commit
$ git checkout <commit> <file>
# Checks in a file
$ git commit -a -m "<commit message>"

# Checkout a remote branch
$ git fetch
$ git checkout <branch>
# Checkout a branch and switch it immediately
$ git checkout -b <branch>
# Checkout a remote tag to a branch
$ git fetch
$ git checkout -b <branch> tags/<tag>

# Adopts a commit from other branch
$ git cherry-pick <commit>
```

### Config the Git
```bash
# Sets the name you want attached to your commit transactions
$ git config --global user.name "<name>"
# Sets the email you want attached to your commit transactions
$ git config --global user.email "<email address>"
# Enables helpful colorization of command line output
$ git config --global color.ui auto
# Sets the core editor for commit
$ git config --system core.editor <editor>
# Open the global configuration file in a text editor for manual editing.
$ git config --global --edit
```

### Git file operation
```bash
# Deletes the file from the working directory and stages the deletion
$ git rm <file>
# Removes the file from version control but preserves the file locally
$ git rm --cached <file>
```

### Save fragment
```bash
# Temporarily stores all modified tracked files
$ git stash
# Restores the most recently stashed files
$ git stash pop
# Lists all stashed changesets
$ git stash list
# Discards the most recently stashed changeset
$ git stash drop
# Create a branch from a Stash
$ git stash branch <branch>
```

### Check the difference
```bash
# Shows difference between working directory and last commit
$ git diff [HEAD]
# Shows difference between staged changes and last commit.
$ git diff --cached
# Shows difference between two commits
$ git diff <old_commit> <new_commit>
# Shows the commits on branchA that are not on branchB
$ git diff <branchB>...<branchA>
# Outputs metadata and content changes of the specified commit
$ git show <commit>
```

### Push changes to remote
```bash
# Forces the git push even if it results in a non-fast-forward merge.
$ git push <remote> --force
# Pushes the tags
$ git push --tags
# Pushes the branch
$ git push <remote> <branch>
# Pushes all the local branches to remote
$ git push <remote> --all
```

### Rebase
```bash
# Interactively rebase from a commit
$ git rebase -i <commit>

# Deletes a commit:
# Start from the <commit>~1, and delete the line of that commit
$ git rebase -i <commit>~1
```

### Tag and Branch
```bash
# Makes a tag
$ git tag <bag>
# Removes a git tag
$ git tag -d <tag>

# Creates a branch
$ git branch <branch>
# Removes a git branch
$ git branch -d <branch>

# Deletes a tag or branch from a remote:
$ git push <remote> :<tag or branch>

# Deletes a tag (with the same name as a branch) from a remote
$ git push <remote> :refs/tags/<tag>
# Deletes a branch (with the same name as a tag) from a remote
$ git push <remote> :refs/heads/<branch>

# Merges a branch to the current branch
$ git merge <branch>
```

### Show the log
```bash
# Condenses each commit to a single line
$ git log --oneline
# Only displays commits that have the specific file.
$ git log -- <file>
# Shows full diff of each commit
$ git log -p
# Searches for commits by a particular author.
$ git log --author="<pattern>"
# Shows commits that occur between <since> and <until>
$ git log <since>..<until>
# Draws text based graph of commits
$ git log --graph --decorate
# Lists the versions of a file
$ git log --follow <file>
```

### Git reset
```bash
# Unstage a file, put a file from staging area to working directory
$ git reset HEAD <file>

# Resets staging area to match most recent commit, but leave the working directory unchanged.
$ git reset
# Resets staging area and working directory to match most recent commit
#  and overwrites all changes in the working directory.
$ git reset --hard
# Moves the current branch tip backward to <commit>,
# reset the staging area to match, but leave the working directory alone.
$ git reset --hard <commit>
# Same as previous, but resets both the staging area & working directory to match.
# Deletes uncommitted changes, and all commits after <commit>.
$ git reset --hard <commit>
```

### Resolve merge conflicts
```bash
# To view the merge conflicts
$ git diff (complete conflict diff)
$ git diff --base file (against base file)
$ git diff --ours file (against your changes)
$ git diff --theirs file (against other changes)

# To discard conflicting patches
$ git reset --hard
$ git rebase --skip

# After resolve conflicts, merge with
$ git add $conflicting_file
$ git rebase --continue
```

### Working with remote
```bash
# Shows remote repositories
$ git remote -v
# Shows information about a remote
$ git remote show <remote>
# Adds a new remote
$ git remote add origin git@....
# Updates the url of an existing remote
$ git remote set-url origin git@...

# Shows remote branches
$ git branch -r
```

### Uses a branch to replace master
```bash
$ git checkout seotweaks
$ git merge -s ours master
$ git checkout master
$ git merge seotweaks
```

### Patches with git
```bash
# Generates a patch
$ git diff <old_commit>  <new_commit> > my.patch
# Apply the patch
$ git apply my.patch

# Prepares a patch for other developers
$ git format-patch origin
# Apply a patch that some sent you
$ git am -3 patch.mbox
# (in case of a conflict, resolve and use
$ git am --resolved )
```

### Repository operations
```bash
# Checks for errors and cleanup repository
$ git fsck
$ git gc --prune
```