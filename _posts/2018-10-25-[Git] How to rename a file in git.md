---
layout: post
title: "How to rename a file in git"
description: ""
tags: [Git]
redirect_from:
  - /2018/10/25/
---

# How to rename a file in git

Git으로 파일을 관리할 때 파일 이름을 바꾸고 `git status`를 수행하면 기존 파일은 deleted되었고 새로운 파일이 생성되었고 인식한다. 이전 이름의 파일과 새로운 이름의 파일을 같이 `git add`를 수행하면 rename으로 바뀌긴 한다. 그러나 파일 내용이 조금 수정되면 rename으로 인식하지 못한다. 이름 변경으로 git에 commit하고 싶을 경우 git은 다음과 같은 subcommand를 제공한다.

## Rename a file
```
$ git mv [old_filename] [new_filename]
```

기존 파일명 새로움 파일명을 `git mv`의 argument로 차례로 넘기면 git은 이전 이름의 파일과 새로운 이름의 파일의 내용이 다를지라도 rename으로 인식하게 된다.

## Reference

* https://help.github.com/articles/renaming-a-file-using-the-command-line/
