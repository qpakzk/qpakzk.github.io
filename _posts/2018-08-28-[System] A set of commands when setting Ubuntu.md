---
layout: post
title: "[System] A set of commands when setting Ubuntu"
description: ""
tags: [System]
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

## 터미널 기본 편집기 변경

```sh
$ sudo update-alternatives --config editor
```

## VMWare Tools 설치

```sh
$ sudo apt-get install open-vm-tools open-vm-tools-desktop -y
```

## git 설치 및 설정

```sh
$ sudo apt-get install -y git
$ git config --global user.name "Sangwon Hong"
$ git config --global user.email "qpakzk@gmail.com"
```
