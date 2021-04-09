---
layout: post
author: Graham Higgins
title: Building headless Gapcoin and Gapcoin-qt for Windows
description: HOW-TO cross-compile Windows binaries using a “depends” build
date: 2021-04-09
category: gapcoin
tags:
---


## Soup-to-nuts cross-compilation on Ubuntu 18/20 host, contributed by [Wizz](https://bitcointalk.org/index.php?topic=822498.msg56742732#msg56742732)


<pre><code style="font-size:90%" class="bash">git clone https://github.com/gapcoin-project/gapcoin-core.git
cd gapcoin-core/
git submodule init
git submodule update
sudo apt update
sudo apt upgrade
sudo apt install build-essential libtool autotools-dev automake pkg-config bsdmainutils curl git
sudo apt install g++-mingw-w64-x86-64
sudo update-alternatives --config x86_64-w64-mingw32-g++  #Set manually the default mingw32 g++ compiler option to posix.
PATH=$(echo "$PATH" | sed -e 's/:\/mnt.*//g')
sudo bash -c "echo 0 > /proc/sys/fs/binfmt_misc/status"
cd depends
make HOST=x86_64-w64-mingw32
cd ..
./autogen.sh
CONFIG_SITE=$PWD/depends/x86_64-w64-mingw32/share/config.site ./configure --prefix=/
make
</code></pre>

---

EOT