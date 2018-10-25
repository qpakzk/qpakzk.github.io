---
layout: post
title: "[Python] Install python version management tools (KR)"
description: ""
tags: [Python]
redirect_from:
  - /2018/09/05/
---

# Install python version management tools

python은 버전 관리가 중요하다. pyenv, pyenv-virtualenv, autoenv를 이용하여 python을 설치하고 버전을 관리하면 유용하다. 본 포스트에서는 macOS 환경에서 pyenv, pyenv-virtualenv, autoenv 설치해보도록 하겠다.

## pyenv

pyenv는 다양한 python 버전 설치 및 관리를 도와주는 프로그램이다.

### 설치

Homebrew를 이용하여 pyenv를 설치해보도록 하겠다.

```sh
$ brew install pyenv
```

pyenv의 최신 버전으로 업그레이드를 원하면 다음과 같이 하면 된다.

```sh
$ brew upgrade pyenv
```

### 환경변수 설정

bash를 사용한다고 가정하고 환경변수 설정을 진행하도록 하겠다.

```sh
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
$ echo 'eval "$(pyenv init -)"' >> ~/.bash_profile
$ source ~/.bash_profile
```

## pyenv-virtualenv

```sh
$ brew install pyenv-virtualenv
```

```sh
$ echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc
```


## autoenv

```sh
$ brew install autoenv
$ echo "source $(brew --prefix autoenv)/activate.sh" >> ~/.bashrc
$ source ~/.bashrc
```
