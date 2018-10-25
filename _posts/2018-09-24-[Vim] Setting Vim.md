---
layout: post
title: "[Vim] Setting Vim (KR)"
description: ""
tags: [Vim]
redirect_from:
  - /2018/09/24/
---

# Setting Vim

`.vimrc` 파일에 Vim editor를 설정해보도록 하겠다.

```sh
$ vi ~/.vimrc
```

```sh
set title
set hlsearch
set number
set autoindent
set cindent
set laststatus=2
set paste
set shiftwidth=8
set showmatch
set smartcase
set smarttab
set smartindent
set softtabstop=8
set tabstop=8
set ruler
set incsearch
set showmatch
set statusline=\ %<%l:%v\ [%P]%=%a\ %h%m%r\ %F\
au BufReadPost *
\ if line("'\"") > 0 && line("'\"") <= line("$") |
\ exe "norm g`\"" |
\ endif
syntax on
```

## Reference

* https://medium.com/sunhyoups-story/vim-%EC%97%90%EB%94%94%ED%84%B0-%EC%9D%B4%EC%81%98%EA%B2%8C-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-5b6b8d546017
