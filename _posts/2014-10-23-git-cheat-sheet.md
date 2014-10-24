---
layout: post
title: "Git Cheat Sheet"
categories:
tags: "Linux"
---

### Check differences


### Basic operations

```bash
# Unstage a file
$ git reset HEAD file_path

# Checkout a remote branch
$ git fetch
$ git checkout test

# Checkout a remote tag to a branch
$ git fetch
$ git checkout -b branch_name tags/tagname
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

### Tag and Branch
```bash
# Make a tag
$ git tag <bag>
# Publish the tag
$ git push --tags
# Remove a git tag
$ git tag -d <tag>

# Create a branch
$ git branch <branch>
# Publish the branch
$ git push <remote> <branch>
# Push all the local branches to remote
$ git push <remote> --all

# Remove a git branch
$ git branch -d <branch>
#
# Deleting a tag or branch from a remote:
$ git push origin :<tag or branch>
# Deleting a tag (with the same name as a branch) from a remote
$ git push origin :refs/tags/<tag>
# Deleting a branch (with the same name as a tag) from a remote
$ git push origin :refs/heads/<branch>
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
```

### Git reset
```bash
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