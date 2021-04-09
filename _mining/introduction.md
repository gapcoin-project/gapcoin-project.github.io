---
layout: post
author: Graham Higgins
title: An introduction to Gapcoin mining
description: Concise introduction to Gapminer and explanation of the <code>--shift</code>, <code>--sieve-primes</code> and <code>--sieve-size</code> settings common to both GapMiner and the in-wallet miner
date: 2021-03-18
category: referene
tags:
---

Concise introduction to Gapminer and explanation of the `--shift`, `--sieve-primes` and `--sieve-size` settings common to both GapMiner and the in-wallet miner

## Introduction to GapMiner

Gapcoin uses prime gap search as a Proof-of-Work function so mining Gapcoin is a little bit _different_ from the usual case, as illustrated by this exchange on the Gapcoin bitcointalk thread ...

> *[Q:](https://bitcointalk.org/index.php?topic=822498.msg9300240#msg9300240) Is there any indication how long it should take to get some coins? After mining <math>x</math> hours at 20,000 primespersec you should find a block? Or is it just totally random?*
> 
> *[A:](https://bitcointalk.org/index.php?topic=822498.msg9306635#msg9306635) Theoretically you will find a gap with merit <math>m</math> within <math>e^m</math> prime gaps.*
> 
> *For Gapcoin, “merit” is pretty much interchangeable with “difficulty”.* 
> 
> *Assuming <math>20.45</math> is the current difficulty, <math>e^20.45 = 760890487</math> so the miner will need to calculate about <math>760890487</math> primes to find a new block.*
> 
> *If the miner reports a primes per second value of 25,000 then it will need <math>760890487/25000 = 30435</math> seconds which is about 8:30 hours. So it will find approx. 2.8 blocks per day.*

---

## CPU Miner settings

One of the consequences of using prime gap search as a Proof-of-Work function is that the miner settings are both more extensive and more complex than the usual situation (in which the amount of CPU work is solely determined by the number of threads used).

### Settings common to GapMiner and in-wallet miner:

    -f  --shift             the adder shift (default 25)
    -i  --sieve-primes      number of primes for sieving (default 900000)
    -s  --sieve-size        the prime sieve size (default 33554432)

*256 + shift* is the [bit size of the prime](/mining/shifts-and-primedigits/)¹ you are searching for, this has to be greater than 16.

*sieve-primes* is the number of primes in the sieve. The more primes sieved, the fewer prime tests that have to be calculated. But too many primes in the sieve will slow down mining.

*sieve-size* is the size of the sieve used for prime search, this should be not greater than *2^shift* (with a limit of *2^64*)

> ¹*For convenience, [a lookup table of all shifts and corresponding primedigit length](/mining/shift-to-primedigits-mapping/) has been made available.*

### Basic mining settings

#### 1. Shift setting (`--shift`)

The shift setting is the most important of the settings in terms of its impact on the chances of mining a block because it determines the number of digits (the size) of the prime numbers to be searched. The larger the primes, the fewer the “hashes” performed by the miner and the less likely you are to mine a block.

At the lowest shift setting of 15, the primes are 82 digits in length. For basic mining, the highest practical shift setting is 64, with prime digits of length 97.

First, decide whether you just want to mine blocks at the default shift setting of 25, along with the majority of other Gapcoin users and thoroughly explore the gaps between prime numbers of 87 digits (and where [many first occurence gaps of record merit](/gapgraphs/meritbyshift/#meritbynblocks) have been discovered) or whether you want to search for prime gaps in a [relatively unexplored area of prime digit length](/gapgraphs/meritbyshift/#meritbyshift) at some other shift setting less than 64.

*(If you want to mine at higher shift settings/primedigit lengths, you will want to mine [using the Chinese Remainder Theorem](/mining/chinese-remainder-mining/))*

To get some sense of which shifts are the most popular (in terms of Gapcoin blocks mined using that shift setting), have a look at the [shift/blocks table](/gapgraphs/shiftfrequency/#shifts) on the “Shift usage histogram” page.

To get some sense of when first occurrence gaps of record merit were discovered during Gapcoin’s history, see the chart of [Gapcoin-held prime gap records and when discovered](/gapgraphs/thegapcoinnetwork/#records) on the “Record gaps and merits discovered by the Gapcoin network” page.

#### 2. Sieve size (`--sieve-size`)

This setting has relatively little impact on miner performance. It is safe to leave it at the default of 33554432.

#### 3. Sieve primes (`--sieve-primes`)

For basic mining, this setting also has relatively little impact on miner performance but it has more impact than sieve size, so you might want to try some ranging settings around your chosen shift to see if changing the value has any observable impact on miner performance. The default value is 900000.

### Examples of systematically varying the settings

Early in Gapcoin’s history, back on 2015-03-07, [a Q&A interchange between pdazzl and j0nn9 on the bitcointalk thread](https://bitcointalk.org/index.php?topic=822498.msg10687403#msg10687403) included the following speculative variants:

```nohighlight
--sieve-size 2097152   --shift 21 --sieve-primes 56474
--sieve-size 4194304   --shift 22 --sieve-primes 106974
--sieve-size 8388608   --shift 23 --sieve-primes 203094
--sieve-size 16777216  --shift 24 --sieve-primes 386702
--sieve-size 67108864  --shift 26 --sieve-primes 1410973
--sieve-size 134217728 --shift 27 --sieve-primes 2703387
```

These suggested variants have been checked and the resulting performance is available to view [as charted results](/paramtests/pdazzlvariant/).

---
