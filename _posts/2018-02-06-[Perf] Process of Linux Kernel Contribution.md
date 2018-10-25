---
layout: post
title: "[Perf] Process of Linux Kernel perf contribution"
description: ""
tags: [Perf]
redirect_from:
  - /2017/02/06/
---

# Process of Linux Kernel perf contribution

In this post, I'll talk about how to contribute to Linux Kernel. I'll exercise on Ubuntu.

## 1. Configuration

First of all, configure an username and an email address in Git.

```sh
$ git config --global user.name "Sangwon Hong"
$ git config --global user.email qpakzk@gmail.com
```

And configure the email sending options.

```sh
$ git config --global sendemail.smtpencryption tls
$ git config --global sendemail.smtpserver smtp.gmail.com
$ git config --global sendemail.smtpuser qpakzk@gmail.com
$ git config --global sendemail.smtpserverport 587
```

## 2. Make a commit

After adding modified files, make a commit.

If you want to make a commit on the command line, you can do like this:

```sh
$ git commit -sm "perf data: Document missing --force option

Add --force option on the man page

Cc: Jiri Olsa <jolsa@kernel.org>
Cc: Namhyung Kim <namhyung@kernel.org>
```

Otherwise, if you would like to use the editor like Vim, enter 'git commit -s' in the shell.

```sh
$ git commit -s
```

And then the editor opens. Write messages to make a commit.

```sh
perf data: Document missing --force option

Add --force option on the man page

Cc: Jiri Olsa <jolsa@kernel.org>
Cc: Namhyung Kim <namhyung@kernel.org>
Signed-off-by: Sangwon Hong <qpakzk@gmail.com>
```

## 3. Make a patch

Make a patch to send it to the maintainer. The patch has a commit message.

```sh
$ git format-patch -1
```

## 4. Send a patch

It's not default subcommand sending email in git. So first of all, it needs to install send-email package.

```sh
$ sudo apt-get install git-email
```

Ans send a patch to the maintainer. If you send it including other developers, you can use -cc option.

```sh
$ git send-email --to "Arnaldo Carvalho de Melo <acme@kernel.org>" \
--cc "linux-kernel@vger.kernel.org" \
--cc "Jiri Olsa <jolsa@kernel.org>" \
--cc "Namhyung Kim <namhyung@kernel.org>" \
0001-perf-data-Document-missing-force-option.patch
```

ps. if you send email on the shell, let less secure apps use your account. For doing this, enter [this site](https://support.google.com/accounts/answer/6010255?hl=en).
