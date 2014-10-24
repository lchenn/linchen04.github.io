---
layout: post
title: "Git Cheat Sheet"
categories:
tags: "Linux"
---

### Check differences


### Basic operations

# Unstage a file
```bash
$ git reset HEAD file_path
```


#### Checkout a remote branch
```bash
$ git fetch
$ git checkout test
```

#### Checkout a remote tag to a branch
```bash
$ git fetch
$ git checkout -b branch_name tags/tagname
```


### Working with remote
```bash
# Show remote repositories
$ git remote -v
# Add a new remote
$ git remote add origin git@....
# Update the url of an existing remote
$ git remote set-url origin git@...
```


### Tag and Branch
```bash
# Removing a git tag:
$ git tag -d <tag>
# Removing a git branch
$ git branch -d <branch>
# Deleting a tag or branch from a remote:
git push origin :<tag or branch>
# Deleting a tag (with the same name as a branch) from a remote
$ git push origin :refs/tags/<tag>
# Deleting a branch (with the same name as a tag) from a remote
$ git push origin :refs/heads/<branch>
```

### Use a branch to replace master
```bash
$ git checkout seotweaks
$ git merge -s ours master
$ git checkout master
$ git merge seotweaks
```