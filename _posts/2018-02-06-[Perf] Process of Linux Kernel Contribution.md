---
layout: post  
title: "Contributing to the Linux Kernel's perf tool"  
description: "A comprehensive tutorial detailing the process of contributing to the Linux Kernel's perf tool." 
tags: [Perf]  
redirect_from:  
  - /2017/02/06/
---

# Contributing to the Linux Kernel's perf tool

In this article, we delve into the systematic approach to contribute to the Linux Kernel, specifically focusing on the 'perf' tool. This tutorial employs Ubuntu as its primary operating system.

## 1. Configuring Git for Contributions

Begin by setting up your Git environment. Configure both your username and email address as follows:

```sh
$ git config --global user.name "Sangwon Hong"
$ git config --global user.email qpakzk@gmail.com
```

Subsequently, set up your email sending preferences:

```sh
$ git config --global sendemail.smtpencryption tls
$ git config --global sendemail.smtpserver smtp.gmail.com
$ git config --global sendemail.smtpuser qpakzk@gmail.com
$ git config --global sendemail.smtpserverport 587
```

## 2. Committing Changes

Once you've made your modifications, stage the changes and proceed to commit them.

For those who prefer using the command line for committing:

```sh
$ git commit -sm "perf data: Document missing --force option

Add --force option on the man page

Cc: Jiri Olsa <jolsa@kernel.org>
Cc: Namhyung Kim <namhyung@kernel.org>
```

Alternatively, if you're inclined to use an editor such as Vim:

```sh
$ git commit -s
```

Upon doing so, the editor will open. Craft your commit message as exemplified below:

```sh
perf data: Document missing --force option

Add --force option on the man page

Cc: Jiri Olsa <jolsa@kernel.org>
Cc: Namhyung Kim <namhyung@kernel.org>
Signed-off-by: Sangwon Hong <qpakzk@gmail.com>
```

## 3. Generating a Patch

Once your commit is ready, create a patch which encompasses your commit message:

```sh
$ git format-patch -1
```

## 4. Transmitting the Patch

Git does not include an inherent subcommand for email transmission. As a result, one must first install the `send-email` package:

```sh
$ sudo apt-get install git-email
```

To send your patch to the maintainer (and possibly include other developers), utilize the `-cc` option:

```sh
$ git send-email --to "Arnaldo Carvalho de Melo <acme@kernel.org>" \
--cc "linux-kernel@vger.kernel.org" \
--cc "Jiri Olsa <jolsa@kernel.org>" \
--cc "Namhyung Kim <namhyung@kernel.org>" \
0001-perf-data-Document-missing-force-option.patch
```

**Note:** If you're sending emails via the shell, ensure to allow less secure apps to access your account. Instructions for the same can be found on [this support page](https://support.google.com/accounts/answer/6010255?hl=en).
