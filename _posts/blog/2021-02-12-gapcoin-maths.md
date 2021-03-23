---
layout: post
author: Graham Higgins
title: Gapcoin maths, from YomKi‘s posts to bitcointalk
description: A technical discussion of the maths behind Gapcoin
date: 2021-03-23
category: maths
tags: feature explainer
---


*(Edited together from 2015/2016 posts to the Gapcoin bitcoin forum by [YomKi](https://bitcointalk.org/index.php?topic=822498.msg14421320#msg14421320))*

The algorithm description on [github](https://github.com/Gapcoin/Gapcoin-PoWCore) is a partial sieve, Fermat test for each remainder, then scan for large gaps. Jonny’s CTR work in [GapMiner](https://github.com/Gapcoin/GapMiner) is doing a lot of startup work but looks like it eventually comes down to sieve the range, Fermat test candidates then scan for large gaps. 

To the best of my knowledge, Gapcoin’s PoW’s are doing effective work and finding large prime gaps. These are computationally difficult to find but relatively easy to verify (very much so in the range Gapcoin is looking at) and Gapcoin is producing results that some people care about. Looking at the distribution *might* tell someone something and particularly large merits might also provide more information (useful for bounds on <math>c</math> in the Cramér-Granville conjecture for instance).

### The significance of finding first occurrence prime gaps

Record large prime gaps provide supporting data to hypotheses about prime gap upper bounds and averages.

Finding *first occurrence* or record (first *known* occurrence) prime gaps tells us something about the structure of the primes. How much is debatable. The recreational/computational task of finding them may lead to new ideas. It demonstrably leads to more efficient software, parts of which can be re-used for other tasks.

Finding new first occurrence gaps would be, in my opinion, more useful in terms of final results, as the results are concrete: “no prime under this point starts a longer gap” vs. “we did lots of work and this is the best we found”. The process involves doing an exhaustive search and one problem would be verification that people actually *did* the work. The final results are flawed if anyone cheats or if a block gets skipped. How to do a quick verification isn’t immediately obvious¹. Lastly, the network could compute for years and find no actual result but just move the “no results below x” forward. Useful but not exciting.

¹ *See foot of page for a reference to Seth Troisi’s contemporary online service providing automated checking and submission of first known occurrence prime gaps*

Finding “the next gap” is a much easier problem and takes as long to verify as it does to find (very slightly less but within a few percent). Given the task of finding record prime gaps, improving the performance of finding the next gap (or primes in a range) is important.

Large prime gaps, like twin primes, are pointing out “hey, something interesting is happening here.” That is why it is more interesting than just listing billions of primes, or finding the next prime. From a project point of view it has the nice features of “hard to find, easy to verify”, relatively linear effort/reward (unlike factoring) and a bonus reward (we broke ## first known occurrence records) to keep up interest.

There are lots of computational problems like this, many with distributed projects. I think record prime gaps is interesting and well-structured for what Gapcoin wants. I think it’s easier to see the possible mathematical benefits than, say, record Mersenne primes, large arithmetic progressions, or Riesel prime searches.

### Approaches to finding first occurrence prime gaps

There are a few different methods being used for current gap finding efforts:

#### 1. Exhaustive search.

This is looking for true record gaps, which means it started at 2 and went up from there.  It’s intensely computationally expensive.  Tomás Oliveira e Silva ran [a distributed project](http://sweet.ua.pt/tos/gaps.html) from 2005 to 2012 that got to <math>4e18</math> using years of work on hundreds of cores.  Interestingly, the computational result was used in Helfgott’s 2013 proof of the Odd Goldbach Conjecture.  Recently the [PGS team at mersenneforum](https://www.mersenneforum.org/forumdisplay.php?f=131) have used a different method to extend this and after about 9 months have brought this to <math>10e18</math>.  The number of records per computational effort is very small, however these are true Minimal Gaps -- once found the record is permanent, as no earlier gaps of that size exist.

#### 2. Gapcoin.
For relatively small P1 values (84-347 digits), choose a random small range, sieve out small multiples, then run Fermat tests to find gaps.  While each step is efficient and fast, it’s rather inefficient at finding record gaps.  It’s basically rapidly throwing darts while blindfolded and being spun around -- the only way to get more darts in the target is to throw faster.

Although in terms of efficiency, Gapcoin is rapidly throwing darts with a blindfold on, the CRT work at least points one in the right direction. Other search methods are aiming the darts at high-probability areas which is why they generate more records. There is arguably a benefit to searching in areas that wouldn’t be covered by the traditional methods. If Gapcoin had more computational resources, it would generate more results of course, as would other methods.

#### 3. Primorial methods.
Gaps are far more common at multiples of primorials without some small divisors, e.g. numbers of the form <math>N * p# / k</math> with k a small square free number.  So if one looks at increasing values of <math>N * 191#/30</math>, for instance, using efficient methods for finding the previous and next primes around that point, one can find record gaps many times times faster than the Gapcoin method.  That is the method used by most other searchers and is what holds all but 3 of the highest merits (thoHow shift setting determines the number of digits in the primes to be searchedse three being from the exhaustive search).  There are some minor variations -- Hans Rosenthal in 2017 did searches with a fixed large N and instead varied k.  Using the dart analogy from before, this is throwing darts while aiming at the target.  The darts are thrown a lot slower but since they’re all thrown in the direction of the target rather than randomly around the room, more of them result in high results.

There may be yet other methods.  I don’t know how Helmut Spielauer finds results (he holds most of the records from 1400-3000) and while searchers like [Michiel Jansen](https://www.mersenneforum.org/search.php?searchid=3887432) use the <math>N * p#/k</math> form, it’s not known what software or algorithm is used.

##### On shift sizes and the size of primes to be examined

Ignoring the coin part of Gapcoin and just looking at the gap records, the shift determines the size of the primes examined. Shift 25 is finding gaps in the 5k-6k range, which Gapcoin has done a lot of work in. Shift 512 in the 12k-17k range. Shift 896 18k-24k. Shift 1024 20k-28k. Ranges very approximate.¹

¹ *For a more detailed explanation, see [“How shift setting determines the number of digits in the primes to be searched”](/mining/shifts-and-primedigits/)*

The higher gap lengths have lower merits, making records easier to find but take longer to calculate and find. Other shift amounts, especially larger than 25, are more likely to find new records since the threshold is lower. Presumably one doesn’t want to do this at the expense of coin return however (there are tools that are much better than Gapcoin at finding records but they don’t have coins).

Using different shift values helps search different ranges, improving the number of results. *(At the time of writing in 2015)* Gapcoin has fallen below 1000 records, now holding about 1.1% from its peak of 1614 records and 2.1%. It’s debatable whether this is a good measure. Right now there are big spikes around length 85, 347 and 232. These are for the shift values of 25 (the original setting), 896 and 512 respectively. [pdazzl](https://bitcointalk.org/index.php?action=profile;u=470347) had quite a few posts about different shift amounts in 2015.²

² *pdazzl’s contributions have been collated in the [Mining how-to](/mining/mining-how-to/) page.*

On the `gapcoin.org` web site, the [length page](http://gapcoin.org/primegaps-length.php) no longer shows data and the files from the [downloads page](http://gapcoin.org/downloads.php) are gone also. So no more Gapcoin records recorded unless someone digs them out of the blockchain.³

³ *the prime gap data that originally appeared on gapcoin.org has been collated and updated in the [Prime Gaps](/primegaps/) section.*

#### Larger gap lengths / higher merits

One might ask whether higher gap lengths have higher merits and wonder if there is some feature of gaps which are more isolated that makes them of lower merit. In short: are more isolated gaps more predictable to find?

If they were maximal gaps, yes. But if one looks at current records, they drop in average merit as the gap size increases.

This is almost certainly an artifact of the time taken per test. It takes much longer to find gaps at the larger sizes, hence we can run many more tests at small sizes given the same processing time, so it’s more likely we find a large merit at the smaller sizes.

Gapcoin ran for a long time with shift 25 and increased the average merit quite a bit in the 5k-7k range. So it finds fewer records in that area now because the threshold is higher¹. On the other hand, that would still seem to be a good choice if looking for very large merits (34+). It depends what your goal is. My point is mostly that spreading out the shift values would result in more even coverage leading to more records.

¹ *(see the [Shift usage histogram](/gapgraphs/shiftfrequency/) for detailed information on the Gapcoin network’s shift use and coverage)*

#### More efficient gap-finding algorithms

One might wonder if there are tools much better than the current algorithm then what would be the reason for not converting Gapcoin to use the more efficient algorithm.

Probably because very few people actually do the coding and most have no incentive. There are some arguable distribution benefits of the random selections rather than traditional ones and it does simplify things for the project. It wouldn’t surprise me if the developers had other reasons.

The non-CRT algorithm is like throwing darts at a target while blindfolded and being spun around. It’s nice that you throw quickly but most of your darts are hitting everything in the room but the wall with the target.

The CRT algorithm does a better job of throwing only when we think we’re pointing toward the target wall.

The traditional method is not using a blindfold and aiming at the target. Measured in speed of throws (primes per second) it is much slower but each prime is far more likely to find a gap. I’m basing this on seeing a single computer in the shift 512 range generating 10x more records/day than Gapcoin’s overall results. There are lots of programming differences as well but I think the largest difference is the search process itself.

In theory, with Gapcoin’s `p = sha256(Blockheader) * 2^shift + adder (adder < 2^shift)`, one would select shift and adder such that they come out to the prime found using sieving around something like <math>1234567 * 193#/210</math>. I don’t have any idea if that would be possible for a miner. It might be possible but result in fewer reported blocks (even if the average merits are higher) so be worth less over time.

#### Validating Gapcoin‘s discovered first occurrence prime gaps

The probable prime test on the endpoints is a quite small portion of time. It’s also mostly playing with semantics as the endpoints are those that failed the test we applied to the interior post-sieve candidates. Most importantly, it also doesn’t match the way the records have been stated over the last 20 years and would lead to very different record results. Specifically, the records are stored by gap size (with prime endpoints).

The test Dr. Nicely’s cglp4 does is strong [BPSW](https://en.wikipedia.org/wiki/Baillie%E2%80%93PSW_primality_test) and it’s possible to add additional non-overlapping probable primality tests for little cost.

Proofs are possible¹. On the 257 Gapcoin record gaps, doing the verification including a primality proof of the endpoints took under 8 minutes on a single core of a home computer. But the time grows rapidly as the size increases and isn’t feasible past 30k digits with today’s software/hardware. If you look at Nicely’s results, gaps under 1000 digits typically have proven endpoints, which is quite a bit larger than Gapcoin’s results.

¹ *Seth Troisi, of the Mersenne Forum’s Prime Gap Search Group currently provides an online resource for [the automated checking and submission](https://primegaps.cloudygo.com/) of record (first known occurrence) prime gaps*

