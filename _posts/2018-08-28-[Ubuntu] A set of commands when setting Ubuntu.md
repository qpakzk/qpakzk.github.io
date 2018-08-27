---
layout: post
title: "[Ubuntu] A set of commands when setting Ubuntu"
description: ""
tags: [ubuntu]
redirect_from:
  - /2018/08/28/
---

# A set of commands when setting Ubuntu

## Vim 설치

```sh
$ sudo apt-get remove -y vim-tiny
$ sudo apt-get update
$ sudo apt-get install -y vim
```

## VMWare Tools 설치

```sh
$ sudo apt-get install open-vm-tools open-vm-tools-desktop
```

## 터미널 기본 편집기 변경

```sh
$ sudo update-alternatives --config editor
```
