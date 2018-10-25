---
layout: post
title: "[Perf] Install Perf from source codes on Ubuntu (EN)"
description: ""
tags: [Perf]
redirect_from:
  - /2017/02/06/
---

# Building Perf

I'll talk about building Perf, which is a profiler tool for Linux 2.6+ based systems that abstracts away CPU hardware differences in Linux performance measurements and presents a simple command line interface.

## Download source codes

```sh
$ git clone --single-branch -b perf/core git://git.kernel.org/pub/scm/linux/kernel/git/acme/linux.git
```

## Set remote repositories

```sh
$ git remote -v
origin	git://git.kernel.org/pub/scm/linux/kernel/git/acme/linux.git (fetch)
origin	git://git.kernel.org/pub/scm/linux/kernel/git/acme/linux.git (push)
```

I'll use `acme` as a remote repository of linux kernel. so rename origin to acme.

```sh
git remote rename origin acme
$ git remote -v
acme	git://git.kernel.org/pub/scm/linux/kernel/git/acme/linux.git (fetch)
acme	git://git.kernel.org/pub/scm/linux/kernel/git/acme/linux.git (push)
```

I'll use origin as my backup remote repository. So I make my remote repository origin.

```sh
$ git remote add origin https://github.com/qpakzk/linux-perf.git
$ git remote -v
acme	git://git.kernel.org/pub/scm/linux/kernel/git/acme/linux.git (fetch)
acme	git://git.kernel.org/pub/scm/linux/kernel/git/acme/linux.git (push)
origin	https://github.com/qpakzk/linux-perf.git (fetch)
origin	https://github.com/qpakzk/linux-perf.git (push)
```

## Install dependencies

```sh
$ sudo apt-get install -y libdw-dev libelf-dev libnewt-dev \
libunwind8-dev elfutils libaudit-dev libperl-dev libnuma-dev \
binutils-dev flex bison libpython2.7-dev asciidoc liblzma-dev \
libiberty-dev libgtk2.0-dev libssl-dev systemtap-sdt-dev python-dev \
libbabeltrace-ctf-dev default-jdk
```

### Set JDIR

```sh
$ echo export JDIR="/usr/lib/jvm/open-jdk" >> ~/.bashrc
$ source ~/.bashrc
```

## Build

I clone perf source code on home directory.

```sh
$ cd ~/linux/tools/perf/
$ make
$ sudo make install
$ sudo cp perf /usr/bin
$ perf

 usage: perf [--version] [--help] [OPTIONS] COMMAND [ARGS]

 The most commonly used perf commands are:
   annotate        Read perf.data (created by perf record) and display annotated code
   archive         Create archive with object files with build-ids found in perf.data file
   bench           General framework for benchmark suites
   buildid-cache   Manage build-id cache.
   buildid-list    List the buildids in a perf.data file
   c2c             Shared Data C2C/HITM Analyzer.
   config          Get and set variables in a configuration file.
   data            Data file related processing
   diff            Read perf.data files and display the differential profile
   evlist          List the event names in a perf.data file
   ftrace          simple wrapper for kernel's ftrace functionality
   inject          Filter to augment the events stream with additional information
   kallsyms        Searches running kernel for symbols
   kmem            Tool to trace/measure kernel memory properties
   kvm             Tool to trace/measure kvm guest os
   list            List all symbolic event types
   lock            Analyze lock events
   mem             Profile memory accesses
   record          Run a command and record its profile into perf.data
   report          Read perf.data (created by perf record) and display the profile
   sched           Tool to trace/measure scheduler properties (latencies)
   script          Read perf.data (created by perf record) and display trace output
   stat            Run a command and gather performance counter statistics
   test            Runs sanity tests.
   timechart       Tool to visualize total system behavior during a workload
   top             System profiling tool.
   version         display the version of perf binary
   probe           Define new dynamic tracepoints
   trace           strace inspired tool

 See 'perf help COMMAND' for more information on a specific command.
```
