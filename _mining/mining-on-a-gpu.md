---
layout: post
author: Graham Higgins
title: Mining on a GPU
description: Basics of using GapMiner on a GPU
date: 2021-03-22
category: reference
tags:
---

## Mining on a GPU

The Gapcoin GPU miner only functions on AMD cards.


> [pdazzl](https://bitcointalk.org/index.php?topic=822498.msg10704266#msg10704266) @j0nn9 - Any new performance improvements coming or nvidia miner?

> [j0nn9](https://bitcointalk.org/index.php?topic=822498.msg10765912#msg10765912) Since i don't have any Nvidia cards, I'm not capable of porting the miner to Nvidia.



### Announcement of GPU miner

The Miner is still a bit buggy but it produced good results for the last few hours so I decided to release a test version.

About the speed: I managed to get around 1,200,000 pps with a single AMD R9 280. That’s a 6x speed increase over the previous GPU miner implementation.

I could also reduce the memory load. Only the sieve still runs on the CPU. Also, the 10 and 15 gaps per hour statistics have been replaced with “tests per second”, the number of primality tests calculated per second.

The algorithm:

The sieve is split into parts of the required gap size then, simultaneously, the prime candidates from each part are tested, starting from the end of the part and skipping those parts which have a prime in it.

When using the `-e` switch the miner will output info about the current average number of prime candidates of those parts (candidates which are not tested yet). Also the minimum number of prime candidates to test is listed.

Several candidates from each part are tested in one GPU run, this number can be controlled with `-n`

---


### GPU parameter settings

The current parameters should be pretty optimal. To illustrate the range:

    -s   from 100,000 to 100,000,000 default 15,000,000
    -w   from  32 to 32000 default 2048
    -a   from  1,000,000 to  100,000,000 default 30,000,000
    -z   from 2 to 30 default 10

Currently only the primality testing runs on the GPU, the sieving still runs on the CPU.

Although it is possible to port the sieve to the GPU, it will probably take more time.

(eXtremal’s Fermat test could be re-used almost without any changes but, since Primecoin and Gapcoin’s sieving differs, a GPU solution for sieving will need a more deeper look into the OpenCL code.)

---

### Relatively poor GPU performance and/or oveheating

The sieve in Gapcoin only runs about 2-3% of the time.

The sieving is calculated on the CPU and the Fermat tests are run on the GPU. Currently it is very (host) memory-hungry (about 1GB) and it is necessary to use one instance per GPU device.

The memory consumption is so high because a very large sieve is used with many primes and also a queue is used to keep the CPU busy while the GPU is processing the Fermat tests.

Altering a few parameters can reduce the memory load:

    -s  --sieve-size        the prime sieve size
    -w  --work-items        gpu work items (default 2048)
    -a  --max-primes        maximum sieve primes (for use with gpu)
    -z  --queue-size        the gpu waiting queue size (memory intensive)

The sieve dynamically adjusts the sieve primes so that it optimally generaets a new set of prime candidates while the GPU is testing a previous set. The queue must have a minimum size of 2.

If the GPU is overheating, maybe there is too much work at once for the GPU.

Try changing some of the parameters, start with reducing the work group to 256: `-w 256`

---

### [j0nn9’s response](https://bitcointalk.org/index.php?topic=822498.msg9606645#msg9606645) to a question about improvements to the GPU miner

    @j0nn9, is it possible to realize improvement of dcct for the GPU-miner?

I’m not sure whether it is possible. I’ve been trying for the last few days to get something running but since dcct’s improvements are for the sieve - which currently runs on the CPU - I didn’t got a solution which was really faster than the current GPU miner.

The problem is that Gapcoin’s sieve probably can’t be ported to the GPU without a huge speed reduction. I already tried only scanning the sieve on the GPU, splitting it in several pieces for each GPU thread but that reduced the overall speed about 1000x that‘s because memory is such a bottleneck on the GPU.

My current idea is to divide the sieve into parts of the required gap size then apply dcct’s strategy to each of those parts by starting to test prime candidates from the end of the part and skipping those parts which have a prime in it.

One problem is that you have to store the first found prime (if there is one) from the previous part in the current part in order to efficiently scan the whole sieve. This (and some other related problems) lead into very difficult code.

Currently it produces invalid results most of the time but I still think that it will give a reasonable speed increase to be worth the effort.”


---

