---
title: Git merge to override master
created: '2021-03-21T09:24:52.347Z'
modified: '2021-03-21T09:29:44.913Z'
---

# Git merge to override master

Suppose I have a `master` branch and a second `different` branch, and that I want to replace master with all the conten t of `different` keepingttrack of the process.

To do so, do the following

```
git checkout different
git merge --strategy=ours master
git chekout master
git merge different
```


If you think you want to go back to `master` before the change identify the last meaningful commit and

```git reset --hard <long-commit-id>```
