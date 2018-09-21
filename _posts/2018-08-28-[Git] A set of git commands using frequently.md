---
layout: post
title: "[Git] A set of git commands using frequently"
description: ""
tags: [Git]
redirect_from:
  - /2018/08/28/
---

# A set of git commands using frequently

## Remove files from git repository permanently

### remove a file

```sh
$ git filter-branch --force --index-filter \
'git rm --cached --ignore-unmatch [FILE NAME]' \
--prune-empty --tag-name-filter cat -- --all
```

### remove a directory

```sh
git filter-branch --force --index-filter \
'git rm -r --cached --ignore-unmatch [DIR NAME]' \
--prune-empty --tag-name-filter cat -- --all
```
