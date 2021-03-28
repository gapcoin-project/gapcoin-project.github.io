---
layout: post
author: Graham Higgins
title: Technical documentation, Gapminer parameter list and description of approach
description: Gapminer parameters and a description of the way it works
date: 2021-03-18
category: mining
tags: gapminer
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

