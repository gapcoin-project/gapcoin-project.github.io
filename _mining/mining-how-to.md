---
layout: post
author: Graham Higgins
title: The hows and whys of miner settings
description: A technical discussion of Gapcoin mining
date: 2021-03-18
category: mining
tags:
---

## Gapminer parameters


    GapMiner  Copyright (C)  2014  The Gapcoin developers  <info@gapcoin.org>

    Required Options:   

      -o  --host              host ip address

      -p  --port              port to connect to

      -u  --user              user for gapcoin rpc authentification

      -x  --pwd               password for gapcoin rpc authentification

    Additional Options:

      -q  --quiet             be quiet (only prints shares)

      -e  --extra-verbose     additional verbose output

      -j  --stats-interval    interval (sec) to print mining informations (default 10)

      -t  --threads           number of mining threads

      -l  --pull-interval     seconds to wait between getwork request

      -m  --timeout           seconds to wait for server to respond

      -c  --stratum           use stratum protocol for connection

      -s  --sieve-size        the prime sieve size (default 33554432)

      -i  --sieve-primes      number of primes for sieving (default 900000)

      -f  --shift             the adder shift (default 25)

      -r  --crt               use the given Chinese Remainder Theorem file

      -d  --fermat-threads    number of fermat threads wen using the crt

          --calc-ctr          calculate a chinese remainder theorem file

          --ctr-strength      more = longer time and mybe better result

          --ctr-primes        the number of to use primes in the ctr file

          --ctr-evolution     whether to use evolutional algorithm

          --ctr-fixed         the number of fixed starting prime offsets

          --ctr-ivs           the number of individuals used in the evolution

          --ctr-range         percent deviation from the number of primes

          --ctr-bits          additional bits added to the primorial

          --ctr-merit         the target merit

          --ctr-file          the target ctr file

      -h  --help              print this information

      -v  --license           show license of this program

---

## What to expect

[Q:](https://bitcointalk.org/index.php?topic=822498.msg9300240#msg9300240) Is there any indication how long it should take to get soime coins? After mining x hours at 20,000 primespersec you should find a block? Or is it just totally random?

[A:](https://bitcointalk.org/index.php?topic=822498.msg9306635#msg9306635) Theoretically you will find a gap with merit *m* within *e^m* prime gaps.

For Gapcoin, “merit” is pretty much interchangeable with “difficulty”. 

Assuming *20.45* is the current difficulty, *e^20.45* = 760890487 so the miner will need to calculate about 760890487 primes to find a new block.

If the miner reports a primes per second value of 25,000 then it will need 760890487/25000 = 30435 seconds which is about 8:30 hours. So it will find approx. 2.8 blocks per day.

---

## The approach

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

#### Sieveing steps

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


#### Settings

`start_index` can be `hash ∗ 2^shift + [0, 2^shift]`

The maximum sieve size depends on `start_index` and is limited by `(hash + 2^shift) - start_index`.

The shift can theoretically be in the range `[14, 2^16]` but nodes can choose to only accept shifts up to a given amount (e.g. 1024 for the main nodes)


---

## CPU Miner settings common to GapMiner and in-wallet miner:

    -f  --shift             the adder shift (default 25)
    -i  --sieve-primes      number of primes for sieving (default 900000)
    -s  --sieve-size        the prime sieve size (default 33554432)

*256 + shift* is the [bit size of the prime](/mining/shifts-and-primedigits/) you are searching for, has to be greater than 13.¹

*sieve-primes* is the number of primes in the sieve. The more primes sieved, the fewer prime tests that have to be calculated. But too many primes in the sieve will slow down mining.

*sieve-size* is the size of the sieve used for prime search, this should be not greater than *2^shift*.²


¹ Lower shift limited later changed to 16

² Applying this maximum limit is only practicable up to a shift of 64

---

## Pushing the limits

By [swissknife1000](https://github.com/gapcoin/gapcoin/issues/5) but results not as described.

Observes that:

- shift = CPU hash rate controller¹
- sieve-size = secondary memory usage controller
- sieve-primes = primary memory usage controller

Higher shifts will slow CPU hash rate but the hash rate is not a guaranteed factor in winning blocks.

¹ *shift sets the number of digits in the primes to be searched and the hash rate will **obviously** vary with the number of digits in the prime*

Recommends changing mining parameters to:

    -f --shift 64
    -i --sieve-primes 40900000
    -s --sieve-size 1553554432

Makes the following (edited) observations:

Memory does not allow a 2 billion `--sieve-size` (currently) but `--sieve-primes` needs to equal or be greater than 40-50 million. You can freely mine at shift 64 without any lost blocks. There is a large loss of hash rate at shift 69 and other various places along the line. Test smaller numbers first and sieve sizes and work your way up.

Every hardware and memory setup will produce different results but every shift can attain 40-50 million `--sieve-primes` with 16GB memory and 6-8 cores or less.

- 16GB across 6 cores, use 50 million `--sieve-primes`
- 16GB across 8 cores, use 40 million `--sieve-primes`

- 32GB across 12 cores use 50 million `--sieve-primes`
- 32GB across 16 cores use 40 Million `--sieve-primes`

with 1.5 billion `--sieve-size` staying the same.

Intel and AMD are always changing but the 1.5 billion `--sieve-size` and 40-50 million `--sieve-primes` is solid, no matter what else changes.

Disable HyperThreading (anything pre-Ryzen 3000) in BIOS and try to lower voltages to stabilize for Yitang Zhang algo to free up memory as multi-threading is useless.

Normally you will need to double your memory when Hyperthreading is enabled but AMD Ryzen 3000 allows you to multi-task WITHOUT disabling multi-threading. However NO temp sensors for Linux Ryzen 3000 yet.

---

## Mining with the Chinese Remainder Theorem at higher shifts


    -r  --crt               use the given Chinese Remainder Theorem file
    -d  --fermat-threads    number of fermat threads wen using the crt

Experimentation suggests that maximum effective `--fermat-threads` is `--threads -1`.

If you want more `--fermat-threads` then the value of `--sieve-primes` needs to be reduced and vice versa. 

Parameter defaults for example shift of 512 (default sieve-size value, reduced value for sieve-primes) :

    -t 8 -f 512 -i 10000 -s 33554432 -d 7 -r crt/crt-22m-512s.txt

#### Example of shifts [contributed by pdazzl](https://bitcointalk.org/index.php?topic=822498.msg40898123#msg40898123)

Here are my thoughts from initially testing out the new crt miner.

What I think is my ideal performance setup is setting roughly half the total threads to Fermat threads. My sieve-primes # is what I then fine-tune on a particular shift size (near the end of fine-tuning only adjusting 1000 on sieve-primes at a time then re-running for a minute to observe). The ideal behavior is the gaplist size generally (most of the time) stays above 100. It'll creep up to a 2000-3000 then oscillate back down to 100 and then continues in this see-saw fashion. The Fermat test speeds seem to kick in faster when the list grows and tamps down the list.

Those are my findings after only 24 hours.  Two shift 512’s so far. I parked my beefier server on shift 1024 for most of the day but gave up after the probability reached 170% with no solved block.

Got my first big CRT block, a record too. Shift 512, length 13306.  On these really big shifts, a much higher overall Fermat thread ratio appears to yield better results.


##### Shift 479

    -t 8 -f 479 -i 13000 -d 6 -r crt/crt-22m-480s-dif22084c.txt

*Content of `crt-22m-480s-dif22084c.txt`*

    |== ChineseSet ==|
    n_primes:     70
    size:         11058
    n_candidates: 769
    offset:       1476535438052344808249114914435996661778930746178207307948586337728699041748900
    69973599252984037935841114047624491809544987485395054755413948

##### Shift 512

    -t 8 -f 511 -i 13000 -d 6 -r crt/crt-22m-512s-dif21588k.txt

*Content of `crt-22m-512s-dif21588k.txt`*

    |== ChineseSet ==|
    n_primes:     74
    size:         11319
    n_candidates: 766
    offset:       1336758545212663910491770481671492155581631117386004561640004944472923534481900
    192446905129909515783553630929900340855652983761167499030099751977773980

##### Shift 1024

If anyone wants to go after the 1020-1024 range here is my best customized sieve file. Strange thing is Gapcoin seems to not record about 15-20% of found blocks for these much higher shifts for some reason, not sure if it's a bug or something else.  Anyways if you’re more interested in setting a bunch of new records than getting more coins and have the cpus available then this should do you well.

    -t 8 -f 1021 -i 23000 -d 6 -r crt/crt-22m-1024s-dif21514b.txt

*Content of `crt-22m-1024s-dif21514b.txt`*

    |== ChineseSet ==|
    n_primes:     130
    size:         18863
    n_candidates: 1039
    offset:       4626081985258152152387146716381104236401743138963348264823465389447497680671113
    1850105279036924603869257530367004081634142637510553687550996988149393864286408
    0741632575037157518785072850028569785866506191383414969297175673797072420119844
    8403639569393650350154418384633294148378069691014056008325991106608

#### Shift 512 performance tests

Doing some more performance testing, here's another one that appears to yield good results if someone wants to try it out.

It's a very low number of primes to sieve with but results in generating a LOT of candidate gaps in the gaplist. The gaplist grows by 50000 every 10 seconds. But the block percentage goes up very quickly. The reason I think it does is because of j0nn9’s algo picking the best candidate gaps from a bigger applicant pool in the heap and thus yielding block solving gaps more quickly.

You’ll want to monitor your memory usage for a couple rounds at first, the high watermark for the above arguments on my machine is about 2.6Gb of RAM so you’ll want to make sure you're not too close to maxing out your memory.


    -t 8 -f 508 -i 10000 -d 7 -r crt/crt-22m-512s.txt

<pre style="font-size:75%">
[2021-03-20 14:37:26] pps: 19216520 / 14220794  tests/s 166659 / 73165  gaps/s 1412 / 1046  gaplist 16212  block [0.061 %]
[2021-03-20 14:37:31] pps: 16369213 / 14245215  tests/s 375725 / 186920  gaps/s 1139 / 1067  gaplist 40465  block [0.158 %]
[2021-03-20 14:37:36] pps: 13382822 / 14210920  tests/s 558188 / 299342  gaps/s 1039 / 1072  gaplist 63953  block [0.252 %]
[2021-03-20 14:37:41] pps: 13943502 / 14137060  tests/s 774781 / 404501  gaps/s 1040 / 1059  gaplist 87180  block [0.347 %]
[2021-03-20 14:37:46] pps: 15246023 / 14032320  tests/s 939739 / 502872  gaps/s 1010 / 1052  gaplist 110259  block [0.438 %]
[2021-03-20 14:37:51] pps: 13739140 / 13874775  tests/s 1169134 / 604929  gaps/s 1034 / 1047  gaplist 132790  block [0.528 %]
[2021-03-20 14:37:56] pps: 14116799 / 13781034  tests/s 1355944 / 706248  gaps/s 1021 / 1043  gaplist 154553  block [0.617 %]
[2021-03-20 14:38:01] pps: 12009346 / 13715721  tests/s 1463812 / 805227  gaps/s 962 / 1040  gaplist 175620  block [0.707 %]
[2021-03-20 14:38:06] pps: 12237896 / 13639221  tests/s 1743849 / 895389  gaps/s 1024 / 1034  gaplist 198285  block [0.794 %]
[2021-03-20 14:38:11] pps: 12447803 / 13537097  tests/s 1630149 / 980470  gaps/s 861 / 1026  gaplist 220651  block [0.877 %]
[2021-03-20 14:38:16] pps: 13876281 / 13453590  tests/s 1950484 / 1062918  gaps/s 943 / 1016  gaplist 241560  block [0.965 %]
[2021-03-20 14:38:21] pps: 12388443 / 13386715  tests/s 2366953 / 1163215  gaps/s 1044 / 1015  gaplist 264398  block [1.051 %]
[2021-03-20 14:38:26] pps: 13090006 / 13330451  tests/s 2303653 / 1249402  gaps/s 942 / 1011  gaplist 284557  block [1.134 %]
[2021-03-20 14:38:31] pps: 13188928 / 13218887  tests/s 2498232 / 1333810  gaps/s 951 / 1006  gaplist 306511  block [1.213 %]
[2021-03-20 14:38:36] pps: 12709365 / 13174729  tests/s 2949285 / 1416248  gaps/s 1052 / 1001  gaplist 327661  block [1.298 %]
[2021-03-20 14:38:41] pps: 10242349 / 13041904  tests/s 2730413 / 1496945  gaps/s 914 / 995  gaplist 347620  block [1.374 %]
[2021-03-20 14:38:46] pps: 15282921 / 13101004  tests/s 3189761 / 1595605  gaps/s 1004 / 996  gaplist 369749  block [1.467 %]
[2021-03-20 14:38:51] pps: 11712828 / 13044960  tests/s 3318869 / 1687937  gaps/s 987 / 996  gaplist 389984  block [1.550 %]
[2021-03-20 14:38:54] Got new target: 21.9356425 @ 21.9356425
[2021-03-20 14:38:56] pps: 14767503 / 13050820  tests/s 3772335 / 1775830  gaps/s 1067 / 995  gaplist 12354  block [1.635 %]
[2021-03-20 14:39:01] pps: 15902633 / 13032501  tests/s 3742388 / 1864600  gaps/s 1004 / 992  gaplist 33266  block [1.718 %]
[2021-03-20 14:39:06] pps: 14521706 / 13000936  tests/s 4300354 / 1950667  gaps/s 1101 / 991  gaplist 53680  block [1.804 %]
[2021-03-20 14:39:11] pps: 11139913 / 12995733  tests/s 3405200 / 2035718  gaps/s 833 / 988  gaplist 74717  block [1.891 %]
[2021-03-20 14:39:16] pps: 14814830 / 13054730  tests/s 4555992 / 2142250  gaps/s 1063 / 991  gaplist 96601  block [1.986 %]
[2021-03-20 14:39:21] pps: 12802957 / 13048281  tests/s 3966409 / 2229109  gaps/s 887 / 990  gaplist 118227  block [2.074 %]
[2021-03-20 14:39:26] pps: 12904250 / 13022517  tests/s 4523940 / 2314318  gaps/s 974 / 988  gaplist 139285  block [2.157 %]
[2021-03-20 14:39:31] pps: 11279758 / 12958809  tests/s 4082008 / 2388005  gaps/s 847 / 984  gaplist 160674  block [2.233 %]
[2021-03-20 14:39:36] pps: 17102741 / 12974224  tests/s 5143318 / 2471163  gaps/s 1030 / 982  gaplist 181847  block [2.321 %]
[2021-03-20 14:39:41] pps: 11441225 / 12947906  tests/s 4368781 / 2550862  gaps/s 845 / 980  gaplist 201954  block [2.405 %]
[2021-03-20 14:39:46] pps: 13735623 / 12962938  tests/s 5450888 / 2643775  gaps/s 1018 / 981  gaplist 223706  block [2.495 %]
[2021-03-20 14:39:51] pps: 13188317 / 12972131  tests/s 5476983 / 2731947  gaps/s 987 / 980  gaplist 245309  block [2.586 %]
[2021-03-20 14:39:56] pps: 13260139 / 12954803  tests/s 6135686 / 2824376  gaps/s 1070 / 980  gaplist 267770  block [2.669 %]
</pre>

#### Recently-checked

    -t 8 -f 512 -i 10000 -r -d 7 crt/crt-22m-512s.txt

<pre style="font-size:75%">
[2021-03-20 12:37:47] pps: 18495710 / 14116054  tests/s 148644 / 74445  gaps/s 1235 / 1015  gaplist 17753  block [0.059 %]
[2021-03-20 12:37:52] pps: 13802828 / 14079900  tests/s 403682 / 193838  gaps/s 1187 / 1063  gaplist 42592  block [0.151 %]
[2021-03-20 12:37:57] pps: 12671518 / 13525757  tests/s 531797 / 300320  gaps/s 983 / 1060  gaplist 66771  block [0.231 %]
[2021-03-20 12:37:59] Got new target: 21.9941027 @ 21.9941027
[2021-03-20 12:38:02] pps: 14859072 / 13777797  tests/s 851063 / 423676  gaps/s 1125 / 1080  gaplist 15239  block [0.321 %]
[2021-03-20 12:38:07] pps: 15255561 / 13458765  tests/s 1125842 / 531174  gaps/s 1169 / 1074  gaplist 38661  block [0.399 %]
[2021-03-20 12:38:12] pps: 11268274 / 13286300  tests/s 1126086 / 629201  gaps/s 973 / 1067  gaplist 63099  block [0.478 %]
[2021-03-20 12:38:17] pps: 10256765 / 13030863  tests/s 1374862 / 733961  gaps/s 1008 / 1060  gaplist 87190  block [0.554 %]
[2021-03-20 12:38:19] Got new target: 21.9976819 @ 21.9976819
[2021-03-20 12:38:22] pps: 10878878 / 12909645  tests/s 1385496 / 824326  gaps/s 901 / 1049  gaplist 13161  block [0.624 %]
[2021-03-20 12:38:27] pps: 13545491 / 12804779  tests/s 1739698 / 917524  gaps/s 1006 / 1043  gaplist 35699  block [0.700 %]
[2021-03-20 12:38:32] pps: 12189545 / 12743278  tests/s 1957140 / 1007954  gaps/s 1019 / 1036  gaplist 58460  block [0.777 %]
[2021-03-20 12:38:37] pps: 11330048 / 12677931  tests/s 2032090 / 1102107  gaps/s 962 / 1031  gaplist 82968  block [0.856 %]
[2021-03-20 12:38:42] pps: 13317033 / 12704077  tests/s 2202445 / 1184361  gaps/s 964 / 1025  gaplist 104051  block [0.934 %]
[2021-03-20 12:38:47] pps:  9779510 / 12540270  tests/s 2133375 / 1262437  gaps/s 865 / 1014  gaplist 126091  block [1.004 %]
[2021-03-20 12:38:52] pps: 12145440 / 12464679  tests/s 2695852 / 1357193  gaps/s 1014 / 1013  gaplist 147873  block [1.076 %]
[2021-03-20 12:38:57] pps: 10770346 / 12302662  tests/s 2712057 / 1446475  gaps/s 951 / 1009  gaplist 168944  block [1.143 %]
[2021-03-20 12:39:02] pps: 15267641 / 12382540  tests/s 3178297 / 1547001  gaps/s 1043 / 1010  gaplist 192246  block [1.227 %]
[2021-03-20 12:39:07] pps: 10085647 / 12296102  tests/s 2887639 / 1630676  gaps/s 893 / 1005  gaplist 214795  block [1.297 %]
[2021-03-20 12:39:12] pps: 16094646 / 12253024  tests/s 3561779 / 1722980  gaps/s 1041 / 1003  gaplist 238035  block [1.368 %]
[2021-03-20 12:39:17] pps:  9867777 / 12196255  tests/s 3302622 / 1811490  gaps/s 915 / 1001  gaplist 260289  block [1.442 %]
[2021-03-20 12:39:22] pps: 10742836 / 12100984  tests/s 3638679 / 1898021  gaps/s 959 / 998  gaplist 282001  block [1.507 %]
[2021-03-20 12:39:27] pps: 11224182 / 12060660  tests/s 3833170 / 1987370  gaps/s 964 / 996  gaplist 303736  block [1.579 %]
[2021-03-20 12:39:30] Got new target: 22.0051803 @ 22.0051803
[2021-03-20 12:39:32] pps: 13545298 / 12070507  tests/s 4492366 / 2095322  gaps/s 1077 / 999  gaplist 12522  block [1.640 %]
[2021-03-20 12:39:37] pps: 11028683 / 12039127  tests/s 4015533 / 2180550  gaps/s 924 / 997  gaplist 35850  block [1.711 %]
[2021-03-20 12:39:42] pps: 13396770 / 12023991  tests/s 4701849 / 2264422  gaps/s 1038 / 994  gaplist 56824  block [1.785 %]
[2021-03-20 12:39:47] pps: 12374667 / 12032576  tests/s 4683985 / 2357883  gaps/s 992 / 994  gaplist 80135  block [1.862 %]
[2021-03-20 12:39:52] pps: 10571585 / 11991386  tests/s 4486635 / 2439966  gaps/s 916 / 991  gaplist 101579  block [1.931 %]
</pre>


#### Larger gaps

Also for anyone interested in hunting for larger overall length gaps, here are some settings that have worked for me (your mileage may vary).  As time goes on I‘m starting to think in some ways larger shifts can be tuned for larger performance (notice I set the fermat thread to total thread ratio very high on these).

Shift 702 on an i7 (8 cores)

    -t 7 -f 702 -i 450000 -d 5 -r crt/crt-22m-704s.txt

Shift 920 on a 4 xeon server (16 cores)

    -t 18 -f 920 -i 300000 -d 15 -r crt/crt-22m-928s.txt


##### Super-ambitious but unfortunately impractical on standard kit

    -t 4 -d 3 -f 512 -i 1553554432 -s 40900000 --crt crt/crt-22m-512s.txt


##### Shifts, sieve-primes, sieve-size

I calculated some surrounding shifts and will diversify my workers over them to test them out:

    -f 21 -s 2097152 -i 56474
    -f 22 -s 4194304 -i 106974
    -f 23 -s 8388608 -i 203094
    -f 24 -s 16777216 -i 386702
    -f 26 -s 67108864 -i 1410973
    -f 27 -s 134217728 -i 2703387

---

## Optimal GPU parameter settings

The current parameters should be pretty optimal. To illustrate the range:

    -s   from 100,000 to 100,000,000 default 15,000,000
    -w   from  32 to 32000 default 2048
    -a   from  1,000,000 to  100,000,000 default 30,000,000
    -z   from 2 to 30 default 10

Currently only the primality testing runs on the GPU, the sieving still runs on the CPU.

Although it is possible to port the sieve to the GPU, it will probably take more time.

(eXtremal’s Fermat test could be re-used almost without any changes but, since Primecoin and Gapcoin’s sieving differs, a GPU solution for sieving will need a more deeper look into the OpenCL code.)

---

## Relatively poor GPU performance and/or oveheating

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

## Improvements to the GPU miner

    @j0nn9, is it possible to realize improvement of dcct for the GPU-miner?

I’m not sure whether it is possible. I’ve been trying for the last few days to get something running but since dcct’s improvements are for the sieve - which currently runs on the CPU - I didn’t got a solution which was really faster than the current GPU miner.

The problem is that Gapcoin’s sieve probably can’t be ported to the GPU without a huge speed reduction. I already tried only scanning the sieve on the GPU, splitting it in several pieces for each GPU thread but that reduced the overall speed about 1000x that‘s because memory is such a bottleneck on the GPU.

My current idea is to divide the sieve into parts of the required gap size then apply dcct’s strategy to each of those parts by starting to test prime candidates from the end of the part and skipping those parts which have a prime in it.

One problem is that you have to store the first found prime (if there is one) from the previous part in the current part in order to efficiently scan the whole sieve. This (and some other related problems) lead into very difficult code.

Currently it produces invalid results most of the time but I still think that it will give a reasonable speed increase to be worth the effort.”


---

## Announcement of GPU miner

The Miner is still a bit buggy but it produced good results for the last few hours so I decided to release a test version.

About the speed: I managed to get around 1,200,000 pps with a single AMD R9 280. That’s a 6x speed increase over the previous GPU miner implementation.

I could also reduce the memory load. Only the sieve still runs on the CPU. Also, the 10 and 15 gaps per hour statistics have been replaced with “tests per second”, the number of primality tests calculated per second.

The algorithm:

The sieve is split into parts of the required gap size then, simultaneously, the prime candidates from each part are tested, starting from the end of the part and skipping those parts which have a prime in it.

When using the `-e` switch the miner will output info about the current average number of prime candidates of those parts (candidates which are not tested yet). Also the minimum number of prime candidates to test is listed.

Several candidates from each part are tested in one GPU run, this number can be controlled with `-n`

---

## GPU miner and the Chinese Reminder Theorem approach

I tried a lot to improve the CPU miner by [using the Chinese Reminder Theorem](/mining/chinese-remainder-mining/) but it seems that Gapcoin’s restriction on the prime numbers makes it impossible to use the full potential of this method so the current method is still faster.

From my point of view, the miner is probably at the upper limits of its performance but maybe someone else might have some smart ideas.
