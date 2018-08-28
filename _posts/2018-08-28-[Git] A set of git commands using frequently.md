---
layout: post
title: "[Git] A set of git commands using frequently"
description: ""
tags: [git]
redirect_from:
  - /2018/08/28/
---

# A set of git commands using frequently

## Remove files from git repository permanently

```sh
$ git filter-branch --force --index-filter \
'git rm --cached --ignore-unmatch [FILE NAME]' \
--prune-empty --tag-name-filter cat -- --all
```
