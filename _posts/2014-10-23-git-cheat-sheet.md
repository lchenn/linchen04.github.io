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
# File changed in working directory
$ git status
# Who changed what at when in a file
$ git blame <file>
# Checkout a file from a commit
$ git checkout <commit> <file>
# Checking in a file
$ git commit -a -m "<commit message>"

# Checkout a remote branch
$ git fetch
$ git checkout <branch>
# Checkout a branch and switch it immediately
$ git checkout -b [branch]
# Checkout a remote tag to a branch
$ git fetch
$ git checkout -b <branch> tags/<tag>

# Adopt a commit from other branch
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
# Show difference between working directory and last commit
$ git diff [HEAD]
# Show difference between staged changes and last commit.
$ git diff --cached
# Show difference between two commits
$ git diff <old_commit> <new_commit>
# Show the commits on branchA that are not on branchB
$ git diff <branchB>...<branchA>
# Outputs metadata and content changes of the specified commit
$ git show <commit>
```

### Push changes to remote
```bash
# Forces the git push even if it results in a non-fast-forward merge.
$ git push <remote> --force
# Publish the tags
$ git push --tags
# Publish the branch
$ git push <remote> <branch>
# Push all the local branches to remote
$ git push <remote> --all
```

### Rebase
```bash
# Interactively rebase from a commit
$ git rebase -i <commit>

# Delete a commit:
# Start from the <commit>~1, and delete the line of that commit
$ git rebase -i <commit>~1
```

### Tag and Branch
```bash
# Make a tag
$ git tag <bag>
# Remove a git tag
$ git tag -d <tag>

# Create a branch
$ git branch <branch>
# Remove a git branch
$ git branch -d <branch>

# Delete a tag or branch from a remote:
$ git push <remote> :<tag or branch>

# Delete a tag (with the same name as a branch) from a remote
$ git push <remote> :refs/tags/<tag>
# Delete a branch (with the same name as a tag) from a remote
$ git push <remote> :refs/heads/<branch>

# Merge a branch to current
$ git merge <branch>
```

### Show the log
```bash
# Condense each commit to a single line
$ git log --oneline
# Only display commits that have the specific file.
$ git log -- <file>
# Show full diff of each commit
$ git log -p
# Search for commits by a particular author.
$ git log --author="<pattern>"
# Show commits that occur between <since> and <until>
$ git log <since>..<until>
# Draw text based graph of commits
$ git log --graph --decorate
# List the versions of a file
$ git log --follow <file>
```

### Git reset
```bash
# Unstage a file, put a file from staging area to working directory
$ git reset HEAD <file>

# Reset staging area to match most recent commit, but leave the working directory unchanged.
$ git reset
# Reset staging area and working directory to match most recent commit
#  and overwrites all changes in the working directory.
$ git reset --hard
# Move the current branch tip backward to <commit>,
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
# Show remote repositories
$ git remote -v
# Show information about a remote
$ git remote show <remote>
# Add a new remote
$ git remote add origin git@....
# Update the url of an existing remote
$ git remote set-url origin git@...

# Show remote branches
$ git branch -r
```

### Use a branch to replace master
```bash
$ git checkout seotweaks
$ git merge -s ours master
$ git checkout master
$ git merge seotweaks
```

### Patch with git
```bash
# Generate a patch
$ git diff <old_commit>  <new_commit> > my.patch
# Apply the patch
$ git apply my.patch

# Prepare a patch for other developers
$ git format-patch origin
# Apply a patch that some sent you
$ git am -3 patch.mbox
# (in case of a conflict, resolve and use
$ git am --resolved )
```

### Repository operations
```bash
# Check for errors and cleanup repository
$ git fsck
$ git gc --prune
```