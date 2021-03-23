---
layout: post
author: Graham Higgins
title: Gapcoin maths
description: A technical discussion of the maths behind Gapcoin
date: 2021-03-19
category: maths
tags:
---

#### [YomKi](https://bitcointalk.org/index.php?topic=822498.msg14421320#msg14421320)


The algorithm description on [github](https://github.com/gapcoin/Gapcoin-PoWCore) is a partial sieve, Fermat test for each remainder, then scan for large gaps. Jonny’s CTR work in [GapMiner](https://github.com/gapcoin/GapMiner) is doing a lot of startup work but looks like it eventually comes down to sieve the range, Fermat test candidates then scan for large gaps. 

To the best of my knowledge, Gapcoin’s PoW’s are doing effective work and finding large prime gaps. These are computationally difficult to find but relatively easy to verify (very much so in the range gapcoin is looking at) and Gapcoin is producing results that some people care about. Looking at the distribution *might* tell someone something and particularly large merits might also provide more information (useful for bounds on <math>c</math> in the Cramér-Granville conjecture for instance).

In terms of efficiency, Gapcoin is rapidly throwing darts with a blindfold on. The CRT work at least points one in the right direction. Other search methods are aiming the darts at high-probability areas which is why they generate more records. There is arguably a benefit to searching in areas that wouldn’t be covered by the traditional methods. If Gapcoin had more computational resources, it would generate more results of course, as would other methods.

Record large prime gaps provide supporting data to hypotheses about prime gap upper bounds and averages.

There are a few different methods being used for current gap finding efforts:

#### Exhaustive search.

This is looking for true record gaps, which means it started at 2 and went up from there.  It’s intensely computationally expensive.  Tomás Oliveira e Silva ran a distributed project from 2005 to 2012 that got to <math>4e18</math> using years of work on hundreds of cores.  Interestingly, the computational result was used in Helfgott’s 2013 proof of the Odd Goldbach Conjecture.  Recently the PGS team at mersenneforum have used a different method to extend this and after about 9 months have brought this to <math>10e18</math>.  The number of records per computational effort is very small, however these are true Minimal Gaps -- once found the record is permanent, as no earlier gaps of that size exist.


#### Gapcoin.
For relatively small P1 values (84-347 digits), choose a random small range, sieve out small multiples, then run Fermat tests to find gaps.  While each step is efficient and fast, it’s rather inefficient at finding record gaps.  It’s basically rapidly throwing darts while blindfolded and being spun around -- the only way to get more darts in the target is to throw faster.


#### Primorial methods.
Gaps are far more common at multiples of primorials without some small divisors, e.g. numbers of the form <math>N * p# / k</math> with k a small square free number.  So if one looks at increasing values of <math>N * 191#/30</math>, for instance, using efficient methods for finding the previous and next primes around that point, one can find record gaps many times times faster than the gapcoin method.  That is the method used by most other searchers and is what holds all but 3 of the highest merits (those three being from the exhaustive search).  There are some minor variations -- Hans Rosenthal in 2017 did searches with a fixed large N and instead varied k.  Using the dart analogy from before, this is throwing darts while aiming at the target.  The darts are thrown a lot slower, but since they’re all thrown in the direction of the target rather than randomly around the room, more of them result in high results.


There may be other methods.  I don’t know how Helmut Spielauer finds results (he holds most of the records from 1400-3000), and while searchers like Michiel Jansen use the <math>N * p#/k</math> form, it’s not known what software or algorithm is used.


j0nn9 last posted in mid-2015, about the same time as his last commit, which is a stretch of “recently.”  I hope he’s doing well.

But the point is true that using different shift values helps search different ranges, improving the number of results.  Gapcoin has fallen below 1000 records, now holding about 1.1% from its peak of 1614 records and 2.1%.  It’s debatable whether this is a good measure.  Right now there are big spikes around length 85, 347, and 232.  These are for the shift values of 25 (the original setting), 896, and 512 respectively.  pdazzl had quite a few posts about different shift amounts in 2015.

The length page no longer shows data, and the files from the downloads page are gone also.  So no more gapcoin records recorded unless someone digs them out of the blockchain.

---

### All relevant Yomki


Thanks Graham. My main issue is getting a URL that returns the JSON text for the blocks. Parsing after that is easy with various methods, but I’m not sure what the right URL is.
> Quote from: PeterTheGrape Just to be clear, as long as the blockchain exists somebody with the skill can extract all the gaps?

To the best of my knowledge, yes.

For instance, I can manually use a link like [https://chainz.cryptoid.info/gap/block.dws?694002.htm](https://chainz.cryptoid.info/gap/block.dws?694002.htm), select the raw block, and see that at 25 Dec 2017 20:09:52 GMT, someone generated the gap

    `4794 288611882004167236117992212159960853275034004726383126062751827740529360669038502244433`

that has a merit of 24.08050173. Most of the blocks are not records. The record gap for 4794 has a merit of 29.39 for instance, so this block isn’t interesting.

> And also was wondering that about the other math coins that are similarly neglected primecoin, riecoin and there are others whose names I forget.

No idea.

> Quote The problem with submitting them late is only that the work might get done twice?

Submitting them late just means nobody knows about them. Since the date is encoded in the block, there ought not be any issue with someone reporting them as if they found them. Gapcoin chooses the P1 randomly in a large enough space that it is *extremely* unlikely anyone would select the same P1.

There are a few different methods being used for current gap finding efforts:

- Exhaustive search. This is looking for true record gaps, which means it started at 2 and went up from there. It’s intensely computationally expensive. Tomás Oliveira e Silva ran a distributed project from 2005 to 2012 that got to 4e18 using years of work on hundreds of cores. Interestingly, the computational result was used in Helfgott’s 2013 proof of the Odd Goldbach Conjecture. Recently the PGS team at mersenneforum have used a different method to extend this and after about 9 months have brought this to 10e18. The number of records per computational effort is very small, however these are true Minimal Gaps -- once found the record is permanent, as no earlier gaps of that size exist.
- Gapcoin. For relatively small P1 values (84-347 digits), choose a random small range, sieve out small multiples, then run Fermat tests to find gaps. While each step is efficient and fast, it’s rather inefficient at finding record gaps. It’s basically rapidly throwing darts while blindfolded and being spun around -- the only way to get more darts in the target is to throw faster.
- Primorial methods. Gaps are far more common at multiples of primorials without some small divisors, e.g. numbers of the form N * p# / k with k a small square free number. So if one looks at increasing values of N * 191#/30, for instance, using efficient methods for finding the previous and next primes around that point, one can find record gaps many times times faster than the gapcoin method. That is the method used by most other searchers and is what holds all but 3 of the highest merits (those three being from the exhaustive search). There are some minor variations -- Hans Rosenthal in 2017 did searches with a fixed large N and instead varied k. Using the dart analogy from before, this is throwing darts while aiming at the target. The darts are thrown a lot slower, but since they’re all thrown in the direction of the target rather than randomly around the room, more of them result in high results.

There may be other methods. I don’t know how Helmut Spielauer finds results (he holds most of the records from 1400-3000), and while searchers like Michiel Jansen use the <math>N * p#/k</math> form, it’s not known what software or algorithm is used.

---

> Quote: Interesting item posted to Hacker News, a paper published at October's Fields Medal Symposium in Toronto: [A Schr¨odinger Equation for Solving the Riemann Hypothesis](http://phys.lsu.edu/~fmoxley/fieldsMedalSymposium.pdf)

The author has previously published this on [vixra](http://vixra.org/abs/1704.0108), which doesn’t bode well. He isn’t on the Fields Symposium program nor is he an invited speaker. He was an attendee.

Some interesting discussion of the Bender-Brody-Müller paper the Moxley one assumes:
- [https://math.stackexchange.com/questions/2211278/riemann-hypothesis-is-bender-brody-m%C3%BCller-hamiltonian-a-new-line-of-attack](https://math.stackexchange.com/questions/2211278/riemann-hypothesis-is-bender-brody-m%C3%BCller-hamiltonian-a-new-line-of-attack)
- [https://arxiv.org/pdf/1704.02644.pdf](https://arxiv.org/pdf/1704.02644.pdf) (“Conclusion: As attractive this idea looks, it does not hold when checking the analysis part of the problem.”

There is some fundamental disagreement there, with Bellissard indicating the BBM paper is heavily flawed while Moxley runs with it.

---

I’m looking for some simple code (e.g. Python, Go, C, Perl, Java, etc.) to scrape blocks to JSON / text. I don’t want the transactions, I want the block data. E.g. the “Raw Block” data from [https://chainz.cryptoid.info/gap/block.dws?688423.htm](https://chainz.cryptoid.info/gap/block.dws?688423.htm).

gapcoin.org went down but was still doing the scraping for a while, but that stopped as well after a while and nobody has submitted any records for Gapcoin for almost a year. If I have a good way to scrape the block data I can do regular submissions.

Gapcoin is down to 748 records (from 1102 at the beginning of the year and 1614 at its peak). The best Gapcoin merit is currently the 29th highest known, but it’s possible there is a higher merit sitting in the blockchain.

---

> Quote there were lots of instructions posted by Jonn9 how to create custom  sifts recently 

j0nn9 last posted in mid-2015, about the same time as his last commit, which is a stretch of “recently.” I hope he’s doing well.

But the point is true that using different shift values helps search different ranges, improving the number of results. Gapcoin has fallen below 1000 records, now holding about 1.1% from its peak of 1614 records and 2.1%. It’s debatable whether this is a good measure. Right now there are big spikes around length 85, 347, and 232. These are for the shift values of 25 (the original setting), 896, and 512 respectively. pdazzl had quite a few posts about different shift amounts in 2015.

The [length page](http://gapcoin.org/primegaps-length.php) no longer shows data, and the files from the [downloads page](http://gapcoin.org/downloads.php) are gone also. So no more gapcoin records recorded unless someone digs them out of the blockchain.

---

The web page is working again, thanks to whoever got it going again.

Gapcoin just got a new top 20 record, with a merit of 34.66, for the number 16 spot.

In December 2014, Gapcoin first made it on the top 20 list with two gaps of merit 33.32 and 33.08 (number 13 and 20 respectively). It peaked in May 2015 with positions 11, 14, 18, and 19 with merits 33.49, 33.32, 33.27, and 33.27. The bottom two dropped off the top 20 list in October 2015, and in June 2016 Gapcoin didn’t have any top 20 merit gaps. At the start of 2017 it takes a merit of 34.52 to get on the top-20 list, and Gapcoin’s second highest merit (the 33.49 that was at one time #11) is now number 55.


---

The web page is still dead, but the dump files are being updated. I’m worried about the loss of infrastructure, as if the gap results are lost then there is no difference between Gapcoin and any other busy-work coin.

---

It seems whatever process had been updating the results ([http://gapcoin.org/primegaps-length.php](http://gapcoin.org/primegaps-length.php)) has stopped. Nothing has changed for almost a month.

I’m not sure if the dump file on the downloads page is more recent, but it had more records. 146 new gaps were submitted to Dr. Nicely’s site. The overall number of Gapcoin records has been going down a little in the last two months as others have broken records.

---

There were 551 record gaps in the file sent.

Gapcoin went from 755 total records to 1241, a gain of 486. The difference is because of breaking its own records.

Gapcoin had 1614 records on 27 Dec 2015 right after submitting. It’s been dropping every month as records have been broken by others. Those tend to be the lowest merits however.


---

The Gapcoin results from 27-Dec-2015 to 14-Aug-2016 are published.

> > Quote from: BitcoinFX The 22M diff at [http://gap.coinia.net/gap/blockexplorer.php](http://gap.coinia.net/gap/blockexplorer.php) is the current network difficulty, as in `getdifficulty`

> I’m also not aware of any published ’live’ statistics for the network total `primespersec` - being estimated or otherwise.

I didn’t mean the difficulty, but the primes per second. [http://gap.coinia.net/gap/stat.php](http://gap.coinia.net/gap/stat.php) under “networkprimesps” would seem to be a live statistic for network total primes per second. It was in the hundreds of millions in early 2015, then fell to very little (sub 10M early this year). It’s up to about 22 million (unrelated to the difficulty which happens to be around 22.x).

Greek’s number indicates 200-400 cores worth overall back in the low-result time frame, or (extremely roughly) around 50 full time computers.

On another, previous, topic of getting university support for gapcoin, I thought the answers here were interesting:

[Could Bitcoin’s mining be combined with actually useful work?](https://www.quora.com/Could-Bitcoins-mining-be-combined-with-actually-useful-work)

[Why haven’t bit-miners repurposed their Bitcoin mining operations to solve for “Real” and “Important”, unsolved mathematical mysteries?](https://www.quora.com/Why-havent-bit-miners-repurposed-their-Bitcoin-mining-operations-to-solve-for-%E2%80%9CReal%E2%80%9D-and-%E2%80%9CImportant%E2%80%9D-unsolved-mathematical-mysteries)

Considering most answers are “no”. The questions are not quite the same (at least the answers assume the result must be a proof rather than understanding).

---

Is there a way to see the overall activity?

About 2 weeks ago the rate of record results on the Gapcoin page went up dramatically, and has stayed that way. The overall number of Gapcoin records had been falling by about 100/month since January (that is, the number of gaps found were not enough to keep up with the amount of records broken by others), but since then it has been able to keep up and even gain a little.

I looked at the coinia stats page on the first post, and it doesn’t seem right. BitCoinFX reports one of his machines generates 15M pps. That exceeds coinia’s “networkprimeps” number for most of this year. It’s reporting a current value of about 22M pps, which implies there are only a couple machines running, which doesn’t seem right. It shows 500 new accounts every day, and one would think they might actually run something.

--- 

> Quote from: no-ice-please 1) Wouldn’t higher gap lengths have higher merits? Or is there some feature of gaps that are more isolated that makes them lower merit? Are more isolated gaps more predictable to find?

If they were maximal gaps, yes. But if one looks at current records, they drop in average merit as the gap size increases.

This is almost certainly an artifact of the time taken per test. It takes much longer to find gaps at the larger sizes, hence we can run many more tests at small sizes given the same processing time, so it’s more likely we find a large merit at the smaller sizes.

Gapcoin ran for a long time with shift 25 and increased the average merit quite a bit in the 5k-7k range. So it finds fewer records in that area now because the threshold is higher. On the other hand, that would still seem to be a good choice if looking for very large merits (34+). It depends what your goal is. My point was mostly that spreading out the shift values would result in more even coverage leading to more records.

 > 2) If there are tools much better than the current algorithm, what would be the reason for not converting Gapcoin to use the more efficient algorithm?</div>Probably because very few people actually do the coding, and most have no incentive. There are some arguable distribution benefits of the random selections rather than traditional ones, and it does simplify things for the project. It wouldn’t surprise me if the developers had other reasons.

The non-CRT algorithm is like throwing darts at a target while blindfolded and being spun around. It’s nice that you throw quickly, but most of your darts are hitting everything in the room but the wall with the target.

The CRT algorithm does a better job of throwing only when we think we’re pointing toward the target wall.

The traditional method is not using a blindfold and aiming at the target. Measured in speed of throws (primes per second) it is much slower, but each prime is far more likely to find a gap. I’m basing this on seeing a single computer in the shift 512 range generating 10x more records/day than Gapcoin’s overall results. There are lots of programming differences as well, but I think the largest difference is the search process itself.

In theory, with Gapcoin’s `p = sha256(Blockheader) * 2^shift + adder (adder < 2^shift)`, one would select shift and adder such that they come out to the prime found using sieving around something like <math>1234567 * 193#/210</math>. I don’t have any idea if that would be possible for a miner. It might be possible but result in fewer reported blocks (even if the average merits are higher) so be worth less over time.

---

Ignoring the coin part of Gapcoin and just looking at the gap records, the shift determines the size of the primes examined. Shift 25 is finding gaps in the 5k-6k range, which Gapcoin has done a lot of work in. Shift 512 in the 12k-17k range. Shift 896 18k-24k. Shift 1024 20k-28k. Ranges very approximate.

The higher gap lengths have lower merits, making records easier to find, but take longer to calculate and find. Other shift amounts, especially larger than 25, are more likely to find new records since the threshold is lower. Presumably one doesn’t want to do this at the expense of coin return however (there are tools that are much better than Gapcoin at finding records, but they don’t have coins).

---

The probable prime test on the endpoints is a quite small portion of time. It’s also mostly playing with semantics as the endpoints are those that failed the test we applied to the interior post-sieve candidates. Most importantly, it also doesn’t match the way the records have been stated over the last 20 years, and would lead to very different record results. Specifically, the records are stored by gap size (with prime endpoints).

The test Dr. Nicely’s cglp4 does is strong [BPSW](https://en.wikipedia.org/wiki/Baillie%E2%80%93PSW_primality_test), and it’s possible to add additional non-overlapping probable primality tests for little cost.

Proofs are possible. On the 257 gapcoin record gaps, doing the verification including a primality proof of the endpoints took under 8 minutes on a single core of a home computer. But the time grows rapidly as the size increases, and isn’t feasible past 30k digits with today’s software/hardware. If you look at Nicely’s results, gaps under 1000 digits typically have proven endpoints, which is quite a bit larger than gapcoin’s results.

---

Finding first occurrence or record (first known occurrence) prime gaps tells us something about the structure of the primes. How much is debatable. The recreational/computational task of finding them may lead to new ideas. It demonstrably leads to more efficient software, parts of which can be re-used for other tasks.

Finding new first occurrence gaps would be, in my opinion, more useful in terms of final results, as the results are concrete: “no prime under this point starts a longer gap” vs. “we did lots of work and this is the best we found”. The process involves doing an exhaustive search, and one problem would be verification that people actually *did* the work. The final results are flawed if anyone cheats or if a block gets skipped. How to do a quick verification isn’t immediately obvious. Lastly, the network could compute for years and find no actual result, but just move the “no results below x” forward. Useful, but not exciting.

Finding “the next gap” is a much easier problem, and takes as long to verify as it does to find (very slightly less, but within a few percent). Given the task of finding record prime gaps, improving the performance of finding the next gap (or primes in a range) is important.

Large prime gaps, like twin primes, are pointing out “hey, something interesting is happening here.” That is why it is more interesting than just listing billions of primes, or finding the next prime. From a project point of view it has the nice features of “hard to find, easy to verify”, relatively linear effort/reward (unlike factoring), and a bonus reward (we broke ## first known occurrence records) to keep up interest.

There are lots of computational problems like this, many with distributed projects. I think record prime gaps is interesting and well structured for what gapcoin wants. I think it’s easier to see the possible mathematical benefits than, say, record Mersenne primes, large arithmetic progressions, or Riesel prime searches.

---

>Quote from: no-ice-please 
> > Quote from: YomKi... finding large prime gaps. These are computationally difficult to find, but relatively easy to verify ...
> 
> Does verifying them involve only
>
> 1) Make sure the two numbers are prime
>
> 2) Make sure there are no primes between them

Yes, that should be all that is necessary. To give you an idea, gapcoin has found 257 record gaps in the last 4 months across the whole network. Verification of them all took 36.5 seconds on a single core. There is still a very small chance the end points are pseudoprimes (this verification was with BPSW rather than a simple Fermat test). After results get submitted to Dr. Nicely, proofs are eventually run on the endpoints if they’re small enough, and that threshold is much higher than the sizes Gapcoin is producing.

> And it seems like with large primes both those would be relatively hard

It depends on “large” and “hard”. Gapcoin is finding primes in the 80-400 digit range, which isn’t very large. A verification for the high end is about half a second. It gets more interesting at 4000 digits, taking maybe 10 minutes. At 40,000 digits it’s certainly possible but quite time consuming. Martin Raab’s monster 4.7 million digit prime can have the endpoints verified with good probable prime tests in 1-2 days but the interior looks like it would take months.

---

> Quote from: MadCow Thanks! At least the PoW does something meaningful

To the best of my knowledge, gapcoin’s PoW’s are doing effective work, and finding large prime gaps. These are computationally difficult to find, but relatively easy to verify (very much so in the range gapcoin is looking at), and Gapcoin is producing results that some people care about. Looking at the distribution *might* tell someone something, and particularly large merits might also provide more information (useful for bounds on c in the Cramér-Granville conjecture for instance).

In terms of efficiency, gapcoin is rapidly throwing darts with a blindfold on. The CRT work at least points one in the right direction. Other search methods are aiming the darts at high-probability areas which is why they generate more records. There is arguably a benefit to searching in areas that wouldn’t be covered by the traditional methods. If gapcoin had more computational resources, it would generate more results of course, as would other methods.

Zhang’s work, and the follow-on work from Tao et al. are theorems, so don’t need any computational “proof of work”, nor would any record prime gap result help prove, disprove, or provide supporting data for their work. Record large prime gaps provide supporting data to hypotheses about prime gap upper bounds and averages.


