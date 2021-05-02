---
layout: post
author: Jonny Frey, edited by Graham Higgins
title: Technical documentation, GPU Gapminer parameter list and description of approach
description: The GPU Gapminer parameters and a description of the way it works
date: 2021-03-18
category: reference
tags: gapminer
---

The GPU Gapminer parameters and a description of the way it works


## GPU Gapminer parameters


    GapMiner  Copyright (C)  2014  The Gapcoin developers  <info@gapcoin.org>

Required Options:   

    -o  --host              host ip address

    -p  --port              port to connect to

    -u  --user              user for gapcoin rpc authentification

    -x  --pwd               password for gapcoin rpc authentification

Additional Options:

    -q  --quiet             be quiet (only prints shares)

    -e  --extra-verbose     additional verbose output

    -j  --stats-interval    interval (sec) to print mining informations

    -t  --threads           number of mining threads

    -l  --pull-interval     seconds to wait between getwork request

    -m  --timeout           seconds to wait for server to respond

    -c  --stratum           use stratum protocol for connection

    -s  --sieve-size        the prime sieve size

    -i  --sieve-primes      number of primes for sieving

    -f  --shift             the adder shift

    -b  --benchmark         run a gpu benchmark

    -g  --use-gpu           use the gpu for Fermat testing

    -d  --gpu-dev           the gpu device id

    -w  --work-items        gpu work items (default 2048)

    -z  --queue-size        the gpu waiting queue size (memory intensive, default 10)

    -a  --platform          opencl platform (amd or nvidia)

    -n  --num-gpu-tests     the number of test per gap per gpu run (default 8)

    -h  --help              print this information

    -v  --license           show license of this program


---

## [The approach](https://github.com/gapcoin-project/Gapcoin-PoWCore#gapcoin-powcore---gapcoins-proof-of-work-functionality)

#### Prime gap

The average length of a prime gap with the starting prime <math>p</math>, is <math>log(p)</math> which means that the average prime gap size increases with larger primes.

#### Merit

Instead of the pure length, Gapcoin uses the “merit” of a prime gap which is the ratio of the gap’s size to the average gap size. If <math>p</math> is the prime starting a prime gap then <math>m = gapsize/log(p)</math> will be the *merit* of this prime gap.


#### Difficulty

A pseudo-random number is calculated from <math>p</math> to provide finer difficulty adjustment. Let <math>rand(p)</math> be a pseudo-random function with <math>0 < rand(p) < 1</math>.

Then, for a prime gap starting at prime <math>p</math> with size <math>s</math>, the difficulty will be <math>s/log(p) + 2/log(p) ∗ rand(p)</math> where <math>2/log(p)</math> is the average distance between a gap of size <math>s</math> and <math>s + 2</math> (the next greater gap) in the proximity of <math>p</math>.

#### Shift and adder

When it actually comes to mining, there are two additional fields added to the block header, named “shift” and “adder”.

We will calculate the prime <math>p</math> as `sha256(block header) ∗ 2^shift + adder`.

As an additional criterion, the adder has to be smaller than <math>2^shift</math> to avoid a situation in which the PoW could be reused.

#### Sieving steps

Calculate the first <math>n</math> primes. In the actual sieve we skip all even numbers because we want to only sieve the odd multiplies of each prime.

So, we create an additional set of primes and multiply each with two. Make sure the `start_index` of the sieve is divisible by two.

Now calculate for each prime the first odd number in the sieve which is divisible by that prime (called `pindex`).

For each prime <math>p</math>: mark `pindex` as composite, add <math>2 ∗ p</math> to `pindex` and mark it as composite, redo till we reach the end of the sieve.

For each remaining prime candidate, check primality with the Fermat-pseudo-prime-test as it is faster than the Miller-Rabin-test
(Fermat is not as accurate as the Miller-Rabin and maybe some valid sieve results will not be accepted but this should be very rare)

Now scan the remaining (pseudo) primes for a big prime gap.

##### dcct's improvements

We do not check every remaining prime candidate with the Fermat test. Instead we look how large the gap has to be to fit the required difficulty (`max_length`).

Then we determine the first prime in the sieve (called `pstart`). Now we scan the prime candidates in the range `(pstart, pstart + max_length)`. We start at the position `(pstart + max_length)` and scan every prime candidate in reverse order till we reach `pstart`.

If we find a prime within the range `(pstart, pstart + max_length)` we can skip all other prime candidates within that range and set `pstart` to that prime.

We redo the above process till we reach the end of the sieve.

---

#### 2014-11-04 [I started working on a GPU miner](https://bitcointalk.org/index.php?topic=822498.msg9439230#msg9439230)

Hi there,

Just wanted to inform you, that I started working on a GPU miner. At the moment I can't say how long it will take.

Just playing around with eXtremal's (madMAx's) code. Till now, the results are pretty promising: On a R9 280 the Fermat test gives a 30x - 40x speed increase in comparison to a single CPU core and gmp.

The sieve in Gapcoin only runs about 2-3% of the time, so at the moment I will only port the primality testing to the GPU.

And of course I will open source it, once it's finished.

Thanks for all your great support so far, I will keep you informed about the process.

j0nn9

---

#### 2014-11-07 [experimental GPU miner](https://bitcointalk.org/index.php?topic=822498.msg9464035#msg9464035)

Hi there,

I've managed to build a experimental GPU miner.

It got me about 200,000 pps with one R9 280x without any overclocking or powertune.

Currently the miner is very experimental and needs to be tested, therefore I published the source code on github.

The miner is a hybrid version of eXtremals fermat test and GapMiners sieve.

The sieving is calculated on the cpu and the fermat tests are running on the GPU.

Currently it is very (host) memory hungry about 1GB and you have to use one instance per gpu device.

You can get it with:


```bash
git clone https://github.com/gapcoin/GapMiner.git -b gpu-miner
cd GapMiner
git submodule init
git submodule update
```


It was built against AMD app SDK v2.9 but maybe works with other versions too. You can edit the Makefile to change the SDK destination directory.

I will merge nonce-pools stratum changes, and probably fix some bugs at the weekend, and then create some binaries within the next week.

---

####  2014-11-07 [why involves only one GPU](https://bitcointalk.org/index.php?topic=822498.msg9472165#msg9472165)

> Quote from: qwep on 2014-11-07, 21:59:51
> why involves only one GPU

You have to use one instance per gpu.

Use `--gpu-dev <id>`, to select the right one.

---

#### 2014-11-08 [after some time the speed starts decreasing](https://bitcointalk.org/index.php?topic=822498.msg9476809#msg9476809)

> Quote from: qqqq on 2014-11-08, 08:36:06
> I got 3x290 and it seems work fine but than after some time the speed starts decreasing in 400 times. It's solo mining.


The Miner currently uses the cpu for sieving, and is very memory hungry, maybe you run out of memory and parts of the program where moved onto the disk (pagefile).

The memory consumption is so high, because a very lage sieve is used, with many primes, and also a queue is used to keep the CPU busy while the GPU is processing the Fermat tests.

You can alter a few parameters to reduce the memory load:

    -s  --sieve-size        the prime sieve size

    -w  --work-items        gpu work items (default 2048)

    -a  --max-primes        maximum sieve primes (for use with gpu)

    -z  --queue-size        the gpu waiting queue size (memory intensive)


The Sieve dynamically adjusts the sieve primes, so that it opimaly generaets a new set of prime candidates while the gpu is testing a previous set. The queue must have a minimum size of 2.

---

#### 2014-11-09 [What are the optimal parameters](https://bitcointalk.org/index.php?topic=822498.msg9488207#msg9488207)

> Quote from: qwep on 2014-11-08, 12:40:18
> What are the optimal parameters
 
    -s  --sieve-size        the prime sieve size

    -w  --work-items        gpu work items (default 2048)

    -a  --max-primes        maximum sieve primes (for use with gpu)

    -z  --queue-size        the gpu waiting queue size (memory intensive)


The current parameters should be pretty optimal.

To give you a range:

    -s   from 100,000 to 100,000,000 default 15,000,000
    -w   from  32 to 32000 default 2048
    -a   from  1,000,000 to  100,000,000 default 30,000,000
    -z   from 2 to 30 default 10

---

#### 2014-11-09 [Dev Is it possible to reduce the load on the processor](https://bitcointalk.org/index.php?topic=822498.msg9488438#msg9488438)

> Quote from: qwep on 2014-11-08, 00:06:41
> Dev Is it possible to reduce the load on the processor

Currently only the primality testing runs on the GPU, the sieving still runs on the CPU.
Although it is possible to port the sieve to the GPU, it will probably take more time.

I could reuse eXtremal's fermat test almost without any changes, but since Primecoin and Gapcoin's sieving differs it will need a more deeper look into the opencl code.

---

#### 2014-11-09, [Was anyone able to run this on nvidia-cards?](https://bitcointalk.org/index.php?topic=822498.msg9489479#msg9489479)

> Quote from: fydel on 2014-11-09, 17:10:41
> > Quote from: dcct on 2014-11-09, 17:02:21
> > Was anyone able to run this on nvidia-cards?
> 
> Nope. Sadly I am getting the same error that q327K091 reported. I was using GFX 750 Ti.

> > Quote from: q327K091 on 2014-11-07, 13:07:35
> > ok got passed OpenCL compiler error, now this

( replaced

    // uint4 q[2] = {0, 0};
        uint4 q[2] = {0, 0, 0, 0};

)

    [2014-11-07 07:05:28] Server supports longpoll
    [2014-11-07 07:05:28] Got new target: 13.0000000 @ 22.4320864
    [2014-11-07 07:05:33] Found platform[0] name = NVIDIA CUDA
    [2014-11-07 07:05:33] Found 3 device(s)
    [2014-11-07 07:05:33] Compiling ...
    [2014-11-07 07:05:33] Source: 205100 bytes
    [2014-11-07 07:05:36] pps: -2147483648 / -2147483648  10g/h -2147483648 / -2147483648  15g/h -2147483648 / -2147483648
    [2014-11-07 07:05:42] Compiled kernel binary size = 969615 bytes
    [2014-11-07 07:05:42] Loaded kernel binary size = 969615 bytes
    [2014-11-07 07:05:42] Using GPU 0 [GeForce GTX 750 Ti]: which has 5 CUs
    [2014-11-07 07:05:42] clWaitForEvents error -9999!
    [2014-11-07 07:05:42] OpenCL error: -5 at ./src/GPUFermat.cpp:406
    [2014-11-07 07:05:42] OpenCL error: -5 at ./src/GPUFermat.cpp:397
    [2014-11-07 07:05:42] OpenCL error: -5 at ./src/GPUFermat.cpp:397

`-5` is an “out of resources” error.

You could try to use

    -w 32

to reduce the memoy load for the gpu.

---

#### 2014-11-11 [What could be wrong? I'm mining it with CPU and it's all right](https://bitcointalk.org/index.php?topic=822498.msg9502722#msg9502722)

Maybe too much work at once for the gpu.

You could try to change some of these parameters,
I would start to try `-w 256`

    -s   form 100,000 to 100,000,000 default 15,000,000
    -w   from  32 to 32000 default 2048
    -a   from  1,000,000 to  100,000,000 default 30,000,000
    -z   from 2 to 30 default 10

---


#### 2014-11-20 [@j0nn9, is it possible to realize improvement of dcct for the GPU-miner?](https://bitcointalk.org/index.php?topic=822498.msg9606645#msg9606645)

I'm not sure whether it is possible.

I've been trying the last few days to get something running, but since dcct's improvements are for the sieve, which currently runs on the CPU, I didn't got a solution which was really faster than the current GPU miner.

The problem is, that Gapcoin's sieve probably can't be ported to the gpu without a huge speed reduction I already tried only scanning the sieve on the gpu, splitting it in several pieces for each gpu thread, but that reduced the overall speed about 1000x - it's just so that Memory is a bottleneck on the gpu.

But I'm not yet out of ideas  Wink

---

#### 2014-12-03 [GPU-Miner status](https://bitcointalk.org/index.php?topic=822498.msg9722936#msg9722936)

Hi there,

just wanted to give a little status update on the GPU-Miner.

My current idea is to divide the sieve into parts of the required gap size, then apply dcct's strategy to each of those parts, by start testing prime candidates from the end of the part and skipping those parts which have a prime in it.

One problem is, that you have to store the first found prime (if there is one) from the previous part in the current part, to efficiently scan the whole sieve. This and some other related problems lead into very difficult code.

Currently it's produce invalid results most of the time, but I still think that it will give a reasonable speed increase to be worth the effort.

---

#### 2014-12-05 [Improved GPU-Miner (experimental)](https://bitcointalk.org/index.php?topic=822498.msg9744615#msg9744615)

Windows: [https://github.com/gapcoin/GapMiner/releases/download/gpu-miner-rev3/windows.zip](https://github.com/gapcoin/GapMiner/releases/download/gpu-miner-rev3/windows.zip)

md5: 6e0fa4a4331c3758bec1fc74334aa753

Linux: [https://github.com/gapcoin/GapMiner/releases/download/gpu-miner-rev3/linux.zip](https://github.com/gapcoin/GapMiner/releases/download/gpu-miner-rev3/linux.zip)

md5: 85bb6f69b22de5e51388155e7b532195

Source Code: [https://github.com/gapcoin/GapMiner](https://github.com/gapcoin/GapMiner) (branch gpu-miner)

The Miner is still a bit buggy, but it produced good results for the last few hours, so I decided to release a test version.

About the speed: I managed to get around 1,200,000 pps with a single AMD R9 280, that's a 6x speed increase to the previous GPU-Miner.

I could also reduce the memory load. Only the Sieve still runs on the CPU.

Also the 10 and 15 gaps per hour are replaced with tests per second, which are the number of primality tests calculated per second.


The algorithm:

The sieve is splitted into parts of the required gap size, then simultaneously, the prime candidates from each part are tested,
starting from the end of the part and skipping those parts which have a prime in it.

When using the `-e` switch you'll get an info about the current average number of prime candidates of those parts (candidates which are not tested yet). Also the minimum number of prime candidates to test are listed.

In one GPU run, several candidates from each part are tested, you can control these number with `-n`

Debugging:

For debugging there are two options added to the Makefile, one for debugging while mining, these are some tests, which shouldn't have a great impact on the pps and one for debugging only. Activating the second option will run several time intensive tests while mining, which has a huge impact on the pps.

#### 2014-05-09 eXtremal [Open Source XPM Pool + GPU Miner (aka. madPrimeMiner)](https://bitcointalk.org/index.php?topic=602292.msg6648209#msg6648209)

Mining algorithm consists of two parts - sieve and Fermat test. madPrimeMiner have very fast sieve and slow non-optimized Fermat test, xpmclminer have too poor sieve but fast Fermat test. I will merge two miners code for create fastest XPM miner.”

“Built with system libwt version 3.3.1, or 3.3.2 is minimal required?”

    [GPU 0] T=-1C A=-1% E=0 primes=0.103835 fermat=482404/sec cpd=6.07/day
    (ST/INV/DUP): 1x 8ch(0/0/0) 1x 9ch(0/0/0)

With replaced Fermat:

    (ST/INV/DUP): 1x 8ch(0/0/0)
    [GPU 0] T=-1C A=-1% E=0 primes=0.104250 fermat=496779/sec cpd=6.51/day

My code uses 384-bit operands, need to create 352-bit version and tune sieve parameters.


> This is on a 290X correct?

Yes. I changed weave depth and got this results:

    [GPU 0] T=-1C A=-1% E=0 primes=0.102074 fermat=589708/sec cpd=6.26/day
    (ST/INV/DUP): 9x 8ch(0/0/0) 1x 10ch(0/0/0)

Fermat tests number increased, CPD - no.. need more time to find right configuration. I will release something after 7CPD reaching on R9 290X.

Claymore already take code of sieve algorithm and release new version with 7.0CPD on Radeon R9 290X. This miner with patch from xpmclminer shows only 6.6CPD now.

---

Peeps, if you want to make use of existing madmax's client with the improved fermat.cl, you can do the following:

1) mkdir ../gpu (while in the madmax dir where xpmclient is located)
2) copy the new fermat.cl, together with the sha256.cl and sieve.cl into the gpu dir (sha256 and sieve .cl inside xpmclient gpu src)
3) if you are using Catalyst 13.12, you need Catalyst 14's libamdocl64.so. replace or load it using LD_LIBRARY_PATH

---

Btw, once .cl is compiled into .bin, you do not need to stick with the above steps, including the need to install new Catalyst drivers

I have kernel.bin for 280x and 7950, if anyone is interested.

---

I'm wrong about 400% (miner shows 500-600k Fermat tests per second, but miner do some other work, not only Fermat tests Smiley ), really 100-120%.

---

    [GPU 0] T=-1C A=-1% E=0 primes=0.098627 fermat=500023/sec cpd=3.76/day
    (ST/INV/DUP): 156x 7ch(0/0/0) 17x 8ch(0/0/0) 1x 9ch(0/0/0)

Conclusion: The sieve code is very fast but the modular exponentiation code needs some improvement. Should be able to achieve an estimated 5 CPD with a faster modular exponentiation implementation on an R9 280X (GTX 580 - 4.2 CPD)

---

My Fermat test implementation is not based on your work, it is faster a bit. But your miner is really good.

My miner shows about 0.3 cpd currently for diff 11 on 290x. However, my calculations show that miner for dif11 will be faster only at 10.99.

What's wrong with cpd calculation? It looks very nice and can be used for target 11 without changes with good approximation. But if you use target 10 for BT sieves you will get invalid cpd values like 0,47. For target 11 for BT you should use 6 layers C1 and 5 layers C2.

-- I know about 6 layers from C1 & 5 from C2.. after full disabling BT shares, miner shows prime probability 0,145 and 4ch/d with target 11 Smiley (on 10ch version prime probability and ch/d decrease).


---

>> Anyone tested on old GPU like HD-5970?

> try it out works on 6970/50

While it may work, pre GCN cards are bad at primecoin mining, there's no way around it.

---

R7 240 is just as quick as a HD5870/6970. VLIW isn't optimize to do primecoin mining.

---

270X settings for DTC:

    #define SIZE 4096           // Size of local sieve array (must be multiple of 1024)
    #define LSIZE 256           // Local worksize for sieve (don't change this)
    #define STRIPES 400         // Number of sieve segments (you may tune this)
    #define WIDTH 20            // Sieve width (includes extensions, you may tune this)
    #define PCOUNT 38400        // Number of sieve primes (must be multiple of 256, you should tune this, 40960 is for 280X)
    #define SCOUNT PCOUNT       // Don't change it
    #define TARGET 9            // Target for s_sieve


>> If you change target to 9 you need to use the latest `*.cl` files from git, 6 days ago. Otherwise you have bugs...

>> Also you may have to reduce STRIPES to maybe 150, otherwise the miner crashes because the sieve now returns 3 times more candidates.

