---
layout: post
title: "[VMWare] Setting shared folders on VMWare Fusion (KR)"
description: ""
tags: [VMWare]
redirect_from:
  - /2018/10/07/
---

# Setting shared folders on VMWare Fusion

본 포스트 내용은 아래 환경에서 진행되었다.

> * VMWare Fusion 10
> * Host OS : macOS Mojave
> * Guest OS : Ubuntu 16.04 또는 18.04

VMWare Fusion에서 Host OS인 macOS와 Guest OS인 Ubuntu 간에 공유 폴더를 설정할 때 문제가 발생하는 경우가 있다. [영상](https://www.youtube.com/watch?v=hK3-XMpCyQ0)과 같이 VMWare tool을 설치했고 공유 폴더로 설정하고자 하는 가상 머신에 Enable Shared Folders를 지정했으나 `/mnt/hgfs/[SHARED FOLDER]`가 생성되지 않았다.

```sh
$ ls /mnt/
$
```

[구글링 결과](https://github.com/vmware/open-vm-tools/issues/199) 다음 명령을 수행하여 해결하였다.

```sh
$ sudo mkdir /mnt/hgfs
$ sudo /usr/bin/vmhgfs-fuse .host:/ /mnt/hgfs -o subtype=vmhgfs-fuse,allow_other
$ ls /mnt/hgfs
shared_folder
```
