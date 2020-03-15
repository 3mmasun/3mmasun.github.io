---
layout: post
title: "Create or Delete Git Remote Branch"
date: 2020-02-04 16:00:00 +0800
tags: [git]
---

### create a remote branch feature-1

```bash
# syntax
git checkout -b <branch_name>
git push <remote_name> <branch_name>

# example
git checkout -b feature-1
git push origin feature-1
```

### delete a remote branch feature-2

```bash
# syntax
git push <remote_name> --delete <branch_name>

# example
git push origin --delete feature-2
```
