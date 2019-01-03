---
layout: post
title: "[CMD] Compress and extract files using tar command"
description: ""
tags: [CMD]
redirect_from:
  - /2018/09/13/
---

# Compress and extract files using tar command

In this post, I'll take a look at how to compress and extract a tar.gz file using tar command in the terminal.

## Compress files

```sh
$ tar -czvf [ARCHIVE].tar.gz [FILE/DIRECTORY]
```

* options
  * -c : Create an archive.
  * -z : Compress the archive of gzip.
  * -v : Verbosely list files processed. (verbose mode)
  * -f : Allow to specify archive's filename.

## Extract files

```sh
$ tar -xzvf archive.tar.gz
```

* options
  * -x : Extract an archive.


## Reference

* https://www.howtogeek.com/248780/how-to-compress-and-extract-files-using-the-tar-command-on-linux/
