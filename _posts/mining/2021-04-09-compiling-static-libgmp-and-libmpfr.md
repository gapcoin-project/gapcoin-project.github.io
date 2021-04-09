---
layout: post
author: Graham Higgins
title: Creating and using locally-compiled static libgmp and libmpfr libraries for linking with GapMiner 
description: Technical HOW-TO compile and use optimised-to-CPU GMP and MPFR libraries
date: 2021-04-09
category: mining
tags: feature technical
---

## Compiling CPU-specific libgmp and libmpfr on Mint/Ubuntu 20 

The standard libgmp and libmpfr libraries as installed by `apt` *may* not be tuned for the specific CPU that you wish to use. This post describes the process of downloading GMP and MPFR sources and compiling them with the appropriate GCC compiler flags so that the compiler can optimise the resulting binary.

*I piloted this procedure on my Dell XPS 15 7590 i9 laptop and saw a performance increase of around 7.5%, I posted [the tabular+charted results](/paramtests/stdvsopt/) in the performance tests section.*

### 1. Download the sources

At the time of writing, the latest release of GMP is 6.2.1 and is downloadable from [https://gmplib.org/download/gmp/gmp-6.2.1.tar.xz](https://gmplib.org/download/gmp/gmp-6.2.1.tar.xz) and the latest release of MPFR is 4.1.0 and is downloadable from [https://www.mpfr.org/mpfr-current/mpfr-4.1.0.tar.bz2](https://www.mpfr.org/mpfr-current/mpfr-4.1.0.tar.bz2)

For the purposes of this article, I’ll create a work folder `foobar` in `/tmp` and, as I *don’t* want to replace my apt-install system versions of libgmp and libmpfr, I’ll dedicate a separate folder in `/opt/acme` (where I habitually keep my stuff, you can decide for yourself where *you’re* going to save the results). And I’ll bind that folder to a shell variable `$MPDIR` just to make it clear.


```bash
# Bind the destination to a shell variable
export MPDIR=/opt/acme
# Navigate to working folder
cd /tmp/foobar
# Download and unpack gmp
curl -O https://gmplib.org/download/gmp/gmp-6.2.1.tar.xz
tar Jxf gmp-6.2.1.tar.xz
# Download and unpack mpfr
curl -O https://www.mpfr.org/mpfr-current/mpfr-4.1.0.tar.bz2
tar jxf mpfr-4.1.0.tar.bz2
```

### 2. Compile the sources

Once downloaded and unpacked, the sources are ready to be compiled up as static libraries and installed into appropriate folders in `$MPDIR`.

But first, set the GCC compiler flags so that it compiles binaries tuned for the CPU that it’s running on:
```bash
# Configure the GCC compiler to produce binaries tuned the CPU 
export CFLAGS="-O3 -march=native -mtune=native"
export CXXFLAGS="-O3 -march=native -mtune=native"
```

Next, navigate to the source folders, configure, make and install the tuned-for-CPU static libraries.

First, compile and install a static `libgmp` so that it’s available for the subsequent compilation and installation of `libmpfr`

```bash
# Navigate to the GMP sources
cd /tmp/foobar/gmp-6.2.1
# Configure for compilation as static library and installation location as defined
./configure --prefix=${MPDIR}/gmp \
    --enable-static=yes --enable-shared=no --enable-cxx --with-pic 
# Make (`$(nproc)` means “use all threads”)
make -j$(nproc)
# install into `opt/acme/gmp`
make install
```

Next, compile and install a static `libmpfr`

```bash
# Navigate to the MPFR sources
cd /tmp/foobar/mpfr-4.1.0
# Configure for compilation as static library and installation location as defined
./configure --prefix=${MPDIR}/mpfr \
    --enable-static=yes --disable-shared --with-pic --with-gmp=${MPDIR}/gmp
# Make (`$(nproc)` means “use all threads”)
make -j$(nproc)
# install into `opt/acme/mpfr`
make install
```

Okay, that's the first stage completed. The working folder can now be deleted with `rm -rf /tmp/foobar`

### Compiling and linking GapMiner

First, check out a fresh copy of the GapMiner sources

```bash
cd /tmp/
git clone https://github.com/gapcoin-project/GapMiner.git
```

Now, navigate to the GapMiner source folder and, because you’ll want to compare the performance of the standard miner against your optimied one, compile as usual:

```bash
cd /tmp/GapMiner
make -j${nproc}
```

At this point, copy your existing `gapminer` to a safe place, else it will get deleted during the build ...

```bash
cd /tmp/GapMiner
cp bin/gapminer ./gapminer-standard
```

Next, create a copy of `Makefile` as `Makefile.opt`


```bash
cd /tmp/GapMiner
cp Makefile Makefile.opt
```

Now edit `Makefile.opt` binding the `MPDIR` variable and changing the FLAGS declarations to:

```makefile
MPDIR     = /opt/acme
GMPLIB    = $(MPDIR)/gmp/lib/libgmp.a
MPFRLIB   = $(MPDIR)/mpfr/lib/libmpfr.a
CXXFLAGS  = -Wall -Wextra -c -Winline -Wformat -Wformat-security \
            -pthread --param max-inline-insns-single=1000 \
            -Wl,-rpath -Wl,/opt/acme/mpfr/lib \
            -I$(MPDIR)/gmp/include -I$(MPDIR)/mpfr/include
LDFLAGS   = -lcrypto -pthread -lcurl -ljansson -lm
OTFLAGS   = -march=native -mtune=native -O3
```
Changing the default target to:

```makefile
# default target
all: link
        $(CC) $(OTFLAGS) $(ALL_OBJ) $(EV_OBJ) $(MPFRLIB) $(GMPLIB) $(LDFLAGS) -o $(BIN)/gapmineropt
```

Commenting out the disable-GPU override that re-sets `LDFLAGS`

```diff
 # disable GPU support
 CXXFLAGS += -DCPU_ONLY 
-LDFLAGS   = -lm -lcrypto -lmpfr -lgmp -pthread -lcurl -ljansson
+#LDFLAGS   = -lm -lcrypto -lmpfr -lgmp -pthread -lcurl -ljansson
```

And finally commenting out the addition of `$(OTFLAGS)` to `LDFLAGS` (because it’s now explicitly specified for teh default target)

```diff
 # optimization
 CXXFLAGS  += $(OTFLAGS)
-LDFLAGS   += $(OTFLAGS)
+#LDFLAGS   += $(OTFLAGS)
```

Now compile using the copied `Makefile.opt`. 

```bash
cd /tmp/GapMiner
make clean
make -j$(nproc) -f Makefile.opt
```

Rename the resulting optimised `gapminer` binary as `gapminer-optimised` and move the previously-saved `gapminer-standard` back into the `bin` folder:

```bash
cd /tmp/GapMiner
mv ./bin/gapminer ./bin/gapminer-optimised
mv ./gapminer-standard ./bin
```

Now you’re ready to compare the performance. Create the following files with the contents as indicated:

`runoptgapminer`

```bash
#!/bin/bash
timeout 1000s ./bin/gapminer-optimised -o localhost -p 31397 \
    -u $(RPCUSER) -x $(RPCPASSWORD) \
    -e -t 4 -f 32  > optminer.log 2>&1
```

`runstdgapminer`

```bash
#!/bin/bash
timeout 1000s ./bin/gapminer-standard -o localhost -p 31397 \
    -u $(RPCUSER) -x $(RPCPASSWORD) \
    -e -t 4 -f 32 > stdminer.log 2>&1
```

`compareminers`
```bash
#!/bin/bash
./runstdgapminer &
./runoptgapminer &
```

Make them executable with:
```bash
chmod +x compareminers run???gapminer
```

When `compareminers` is executed, it will *simultaneously* run the standard gapminer using four threads and the optimised gapminer using four threads - that’s eight (8) threads in total, adjust equally downwards if necessary. Compare the output in `optminer.log` and `stdminer.log` to see any performance differences.

---

EOT