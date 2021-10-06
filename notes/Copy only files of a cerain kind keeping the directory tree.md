---
title: Copy only files of a cerain kind keeping the directory tree
created: '2021-10-06T12:25:20.491Z'
modified: '2021-10-06T12:25:51.858Z'
---

# Copy only files of a cerain kind keeping the directory tree

```
rsync -rav -e ssh --include '*/' --include='*.pdf' --exclude='*' server:path localpathpath
```
