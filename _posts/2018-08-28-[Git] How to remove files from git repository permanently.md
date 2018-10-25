---
layout: post
title: "[Git] How to remove files from git repository permanently (KR)"
description: ""
tags: [Git]
redirect_from:
  - /2018/08/28/
---

# How to remove files from git repository permanently

Git은 아무리 삭제한 파일(file)/디렉터리(directory)라고 하더라도 git commit을 하면 삭제한 기록들을 모두 저장한다. 그래서 git rebase를 통해 삭제한 파일/디렉터리를 다시 확인할 수 있다.

그러나 git 히스토리(history)에서 파일/디렉터리를 영원히 삭제하고 싶은 경우가 있다. 더이상 버전관리를 할 필요없는 파일/디렉터리인데 git history에 저장되어 있기 때문에 프로젝트가 무거워지는 경우가 대표적이다. 또는 개인정보가 담긴 파일/디렉터리를 commit해 버린 경우가 있을 수도 있다.

git에서는 이러한 경우를 대비하여 git history 상에서 파일/디렉터리를 완전히 제거해주는 명령을 제공해준다.

## Remove a file

```sh
$ git filter-branch --force --index-filter \
'git rm --cached --ignore-unmatch [FILE NAME]' \
--prune-empty --tag-name-filter cat -- --all
```

## Remove a directory

```sh
git filter-branch --force --index-filter \
'git rm -r --cached --ignore-unmatch [DIR NAME]' \
--prune-empty --tag-name-filter cat -- --all
```

## Conclusion

위 명령을 수행한 후에는 당연히 commit id의 해시가 바뀌기 때문에 remote repository에 올릴 경우 `git push origin master --force`와 같은 방식으로 올려야 한다.
