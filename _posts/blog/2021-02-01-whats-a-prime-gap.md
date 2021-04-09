---
layout: post
title: Prime gaps and the Gapcoin rationale
description: Explanation of prime gaps, merit and how Gapcoin uses both.
date: 2021-02-01
category: maths
tags: explainer
---

<h3 class="ui teal header">Definition of a “prime gap”</h3>

A prime gap is the difference between successive prime numbers. For example, the numbers 317 and 331 are both prime, but no number in between is prime, so we have a prime gap of 14.

A prime gap constitutes a **first occurrence** when no preceding gap has an equal value. 

A first occurrence prime gap is **maximal** if the gap strictly exceeds all preceding gaps.

No gap exceeding 1550 has been definitively established as a first occurrence; larger gaps included in (these) lists are instead **first known occurrence** prime gaps and should be taken as the normal use of the term.

The smallest gap whose first occurrence remains uncertain is the gap of 1432.

The smallest gap for which no occurrence is yet known is the gap of 112738.

###### (portions of the above taken from the late Dr. Thomas R. Nicely’s list: [“First occurrence prime gaps”](https://faculty.lynchburg.edu/~nicely/gaps/gaplist.html) last updated 12th. August, 2019)

<h3 class="ui teal header">The “merit” of a prime gap</h3>

As a consequence of the [Prime Number Theorem](https://en.wikipedia.org/wiki/Prime_number_theorem), the average difference between consecutive primes near <math>x</math> is approximately <math>ln(x)</math>.

The **merit** of a prime gap is thus defined as the prime gap divided by this average prime gap.

For example, the merit of the prime gap between 317 and 331 is 2.43, which means that this prime gap is more than twice the average prime gap among those between 1 and 317.

Formally, the merit <math>M</math> of a prime gap of measure <math>g</math> following the prime <math>p<sub>1</sub></math> is defined as <math>M=g/ln(p<sub>1</sub>)</math>. It is the ratio of the measure of the gap to the “average” measure of gaps near that point.

###### (portions of the above taken from [“Prime numbers and cryptography - The Times Malta”](https://timesofmalta.com/articles/view/Prime-numbers-and-cryptography.672957))

<h4 class="ui horizontal divider teal header"><i class="cogs icon"></i></h4>

<h3 class="ui teal header">Gapcoin’s method for finding prime gaps</h3>

The prime numbers are not regularly spaced.

For example from 2 to 3 the gap is 1. (2 is a prime number, the one and only even prime number)

From 3 to 5 the gap is 2.

From 7 to 11 it is 4.

Between 2 and 50 we have the following pairs of 2-gap primes: 3-5, 5-7, 11-13, 17-19, 29-31, 41-43

A prime gap of length <math>n</math> is a run of <math>n-1</math> consecutive composite (i.e. divisible) numbers between two successive primes (see: [http://mathworld.wolfram.com/PrimeGaps.html](http://mathworld.wolfram.com/PrimeGaps.html)).

We will write a function *gap* with parameters:

- <math>g</math> (an integer >= 2) which indicates the gap we are looking for
- <math>m</math> (an integer >= 2) which gives the start of the search (<math>m</math> inclusive)
- <math>n</math> (an integer >= <math>m</math>) which gives the end of the search (<math>n</math> inclusive)

As an example: `gap(2, 2, 50)` will return `[3, 5]` which is the first pair of prime numbers between 2 and 50 that has a 2-gap.

The function should return the first pair of prime numbers spaced with a gap of <math>g</math> between the limits <math>m</math>, <math>n</math> if these numbers exist, otherwise `nil` or `null` or `None` or `Nothing` depending on the programming language in which the *gap* function is implemented.

Examples:
  
`gap(2, 5, 7)` yields `[5, 7]`

`gap(2, 5, 5)` yields `nil`

`gap(4, 130, 200)` yields `[163, 167]`

`gap(6, 100, 110)` yields `nil`


Example 4 returns `nil` because the numbers between 100 and 110 include the primes 101, 103, 107 and 109. By the same token, [101-107] is not a 6-gap because the sequence includes 103 and neither is [103-109] a 6-gap because it includes 107.

The *gap* function returns only the **first occurrence** (if any) of the specified size gap. In example 3, `[193, 197]` is also a 4-gap pair of primes between 130 and 200 but it’s not the first occurrence of a 4-gap pair of primes in the sequence.

<h3 class="ui teal header">December 2017, largest prime gap merit discovered to date</h3>

In December 2017 (confirmed in early 2018) the Gapcoin network found a new prime gap (of length 8350 following an 87-digit prime) of maximum known merit (i.e. the largest prime gap merit discovered to date).

The merit <math>M=G/ln(P1)</math> of this gap is <math>M=41.93878373153988</math>, *the largest merit of any known first occurrence prime gap* and the first prime gap to be discovered with a merit exceeding 40. The value of the merit means that the gap of 8350 is almost 42 times as large as the average prime gap at that point. Source : [https://faculty.lynchburg.edu/~nicely/](https://faculty.lynchburg.edu/~nicely/)

Gapcoin's [highest found merits](http://gapcoin.org/primegaps-merits.php) as of 31st March 2020 (Top 30)

<h4 class="ui horizontal divider teal header"><i class="cogs icon"></i></h4>

<h3 class="ui teal header">Gapcoin rationale and description from 2015 by “j0nn9”, original developer¹</h3>

First of all, Gapcoin follows Riecoin’s way and uses enough Miller-Rabin tests with random bases to avoid composite numbers being accepted as Prove of Work, like Primecoin mistakenly could.

But the real improvement is due to its easy “pool-mineable” Hashing algorithm. This means that creating a Gapcoin pool will be as easy as creating a scrypt one!

When you look at Riecoin, there are only two pools. Even Primecoin, the first scientific cryptocurrency, only has three reliable pools. This is due to the difficulty of creating a fair reward system for the custom hashing algorithms of Prime- and Riecoin.

In Primecoin, which is searching for long prime chains, you can easily modify your miner to search for smaller chains. In fact, it is mostly about a simple one-line-editing. As an example, just turn a 10 into a 7 in xolominer and you will get scads of 7-chains, but your chance to find a block has diminished.

To avoid this, pools supply better payment for shares with longer chain-lengths.

In Riecoin, it is even worse. Riecoin searches for prime tuples of length 6. Pools do accept tuples with less primes, but a 6-tuple only can occur in certain places. (Look at this post for a detailed explanation.) 4-tuples, by comparison, are more frequent. There are places, where a 4-tuple can occur, but no 6-tuple, which Riecoin truly needs. So pools have to check every submitted share whether the miner really searches for 6-tuples or not. Those facts are what make it so hard to create a Prime- or Riecoin pool.

With Gapcoin, there won’t be any problems like these. While in Riecoin and Primecoin you can choose whether to search for bigger shares or smaller ones, Gapcoin is searching for prime gaps in general. The distribution of prime gaps is still a mystery for mathematicians, that’s why you can’t modify your miner to look for special results. Consequently, every submitted share can be paid equally.

¹ *(Some statements about Riecoin and Peercoin are no longer the case, having been overtaken by time and subsequent improvements/developments)*


<h3 class="ui teal header">Prime gap searching as a Proof-of-Work function</h3>

A PoW algorithm has to fit two specifications:

- It must be cryptographically secure (a PoW must not be reusable)
- It must be hard to calculate, but easy to verify

Verifying a prime gap is easy, you only have to check every number between the start and the end to be composite.

Calculating is harder, much harder!

Large prime gaps occur a lot lesser than smaller ones. According to [E. Westzynthius](http://primerecords.dk/primegaps/gaps20.htm), in <math>e^n</math> prime gaps there will be one gap that is <math>n</math> times greater than the average prime gap.

The average length of a prime gap with the starting prime <math>p</math>, is <math>log(p)</math>, which means that the average prime gap size increases with larger primes. Then, instead of the pure length, we use the **merit** of the prime gap, which is the ratio of the gap’s size to the average gap size.

Let <math>p</math> be the prime starting a prime gap, then <math>m = gapsize/log(p)</math> will be the merit of this prime gap.

Also a pseudo-random number is calculated from <math>p</math> to provide finer difficulty adjustment.

Let <math>rand(p)</math> be a pseudo-random function with <math>0 > rand(p) > 1</math> Then, for a prime gap starting at prime <math>p</math> with size <math>s</math>, the difficulty will be <math>s/log(p) + 2/log(p) * rand(p)</math>, where <math>2/log(p)</math> is the average distance between a gap of size <math>s</math> and <math>s + 2</math> (the next greater gap) in the proximity of <math>p</math>.

When it actually comes to mining, there are two additional fields added to the block header, named “shift” and “adder”. We will calculate the prime <math>p</math> as <math>sha256(blockheader) * 2^shift + adder</math>. As an additional criterion the adder has to be smaller than <math>2^shift</math> to avoid that the PoW could be reused.

If the difficulty reaches 35.4245, every block will be a new world record: [Top 20 Prime Gaps](http://primerecords.dk/primegaps/gaps20.htm)

Also, if the difficulty reaches (or spikes above) <strong>41.94</strong>, *every* block will be a new world record.

We already broke more than [544 records](http://gapcoin.org/primegaps.php) of first known occurrence prime gaps. *(Note: Content not updated from 2014)*.

<h3 class="ui teal header">Prime numbers</h3>

Prime numbers are interesting for lots of mathematicians around the globe, and they’re also important to every day cryptography (see RSA).

Researches about prime gaps could not only lead to new breakthroughs in the bounded gap, it may also help proving the Twin Prime Conjecture and maybe even the millennium problem, the Riemann hypothesis. Who knows?
