---
layout: post
author: Graham Higgins
title:  Technical convos on bitcointalk 
description: Discourse by apparently-knowledgable Gapcoin users
date: 2021-04-06
category: gapcoin
tags:
---


<p><span style="color: orange">2014-11-13</span> <a href="https://bitcointalk.org/index.php?topic=822498.msg9409541#msg9409541" target="_blank">bsunau7</a>: To me the primes/s metric looks to be useless.  It is a counter which is only incremented when a composite isn’t found which makes it a valid comparison only for the same sieve parameters.<br/><br/>Example; assume that there are on average 100 non-composite number in the gap to test, your chance of finding a block is primes/s divide by 100 multiplied by the chance of a gap.<br/><br/>Now lets increase the efficiency of the sieve (add more primes) so that you only have 80 non-composite numbers to test.  The equation used above is now wrong by 25% and your reported primes/s has hardly changed at all.<br/><br/>This also means profit calculators based on primes/s are not accurate if you change <code>-s</code> or <code>-r</code> when mining.<br/><br/>Using <code>10g/s</code> or <code>15g/s</code> would be a better method to calculating profits as it includes a way of seeing the effects of sieve efficiency.</p>

<hr/>

<p><span style="color: orange">2014-11-13</span> <a href="https://bitcointalk.org/index.php?topic=822498.msg9456472#msg9456472" target="_blank">bsunau7</a>: Thanks to riecoin my gmp is already custom compiled and tuned. I only mentioned testnet as the difficulty was high and was increasing at a steady rate. Interesting that you get some performance out of SIMD with the code as is. One of the first things I did was to compile with <code>-ftree-vectorize -mavx2 -ftree-vectorizer-verbose=5</code> to see what auto-vectorising found.  It didn’t find much (any?) to vectorise as most of the size of the loops aren’t know at compile time (there are trick you can use however) or a non-uniform step being used. PS. The fact that GCC couldn’t vectorise what should be very conducive to vectorising is a good avenue to work on for speed-ups.</p>

<hr/>

<p><span style="color: orange">2014-11-13</span> <a href="https://bitcointalk.org/index.php?topic=822498.msg9550009#msg9550009" target="_blank">bsunau7</a>: Not sure if anyone else thinks this is a good idea, but can we replace those 10 & 15 gap metrics with something else?<br/><br/>I am using primes/s and candidates/s eg:</p>

<pre>[2014-11-15 10:59:11] pps: 14669 / 14287  candidates/s 63998895
[2014-11-15 10:59:41] pps: 13121 / 14136  candidates/s 63321793
[2014-11-15 11:00:11] pps: 13572 / 14100  candidates/s 63159069</pre>


<p>This is just the number of "numbers" scanned, in effect how fast numbers are skipped/tested.  I just accumulate <code>sievesize</code> for every call of <code>run_sieve</code>.<br/><br/>It is the only way I can see of measuring performance across different miners and different parameters (tuning parameters is why I added it to mine).</p>

<hr/>

<p><span style="color: orange">2014-11-13</span> <a href="https://bitcointalk.org/index.php?topic=822498.msg9472660#msg9472660" target="_blank">bsunau7</a>: The miner does not stop mining the sieve until the original one is verified by a slow <code>mpz_nextprime()</code> call. When your miner is significantly faster than the PoW function you tend to find lots of shares before the PoW can stop the sieve from mining.</p>

<hr/>

<p><span style="color: orange">2014-11-13</span> <a href="https://bitcointalk.org/index.php?topic=822498.msg9473075#msg9473075" target="_blank">Supercomputing</a>: @bsunau7 Thanks for the info and I will implement a small sieve for validation and use a single exponentiation test at each end point; it should be at least 100x faster and less than <math>1/(2<sup>128</sup>)</math> probability of it being a larger gap.</p>

<hr/>

<p><span style="color: orange">2014-11-13</span> <a href="https://bitcointalk.org/index.php?topic=822498.msg9473240#msg9473240" target="_blank">bsunau7</a>: There was talk on GMP mailing lists about speeding up gmp_nextprime in a very similar manner, sieve the start/end gap before running expensive MR tests. As the gap has been pre-sieved you might just be able to MR test the non-composite in the mining sieve and get the same result. I personally didn’t bother with the PoW validation code as for larger gaps it just isn’t called enough to matter. Also you can tweak the <code>pprocessor->process()</code> to terminate the sieve early which will cure the stales and get you to the next "block" a few seconds faster at the risk of having a slightly wrong difficulty (in effect a non issue).</p>

<hr/>

<p><span style="color: orange">2014-11-13</span> <a href="https://bitcointalk.org/index.php?topic=822498.msg9476851#msg9476851" target="_blank">bsunau7</a>: Here is a little fix which increased my block count (got your attention)?<br/><br/>Added TCP keep alives with a sub 5 minute period to the wallet.  Three lines of code in <code>net.cpp</code> and <code>netbase.cpp</code> and a tweak of the Linux kernel.</p>

<code>net.cpp diff:</code>

<pre>--- net.cpp_orig        2014-11-07 19:38:26.941369345 +0100
+++ net.cpp     2014-11-07 19:42:11.077371850 +0100
@@ -1594,6 +1594,7 @@
     // Different way of disabling SIGPIPE on BSD
     setsockopt(hListenSocket, SOL_SOCKET, SO_NOSIGPIPE, (void*)&nOne, sizeof(int));
 #endif
+    setsockopt(hListenSocket, SOL_SOCKET, SO_KEEPALIVE, (void*)&nOne, sizeof(int));

 #ifndef WIN32
     // Allow binding if the port is still in TIME_WAIT state after

</pre>

<code>netbase.cp diff:</code>

<pre>--- netbase.cpp_orig    2014-11-07 19:38:21.365369283 +0100
+++ netbase.cpp 2014-11-07 19:41:02.549371084 +0100
@@ -329,6 +329,8 @@
     int set = 1;
     setsockopt(hSocket, SOL_SOCKET, SO_NOSIGPIPE, (void*)&set, sizeof(int));
 #endif
+    int set = 1;
+    setsockopt(hSocket, SOL_SOCKET, SO_KEEPALIVE, (void*)&set, sizeof(int));

 #ifdef WIN32
     u_long fNonblock = 1;
</pre>

Add into /etc/sysctl.conf

<pre>net.ipv4.tcp_keepalive_time = 240
net.ipv4.tcp_keepalive_intvl = 15
net.ipv4.tcp_keepalive_probes = 9</pre>

<p>Then "sysctl -p /etc/sysctl.conf" to make it take effect.</p>

<p>I went from spending half my time in 45 minute limbo land mining dead blocks due to the wallet hanging to no issues in the last 24 hours (no wasted mining).</p>

<p>Just quick and dirty hack (this is code for "It could have been done in a nicer way") which seems to have sorted out a big source pain for my little 4-core mining rig.</p>

<p>Oh, this might also address stratum mining issues this coin seems to have.  Monotonic coins don't go 15+ minutes without a transactions (i.e network traffic) so they would not see this issue.</p>


<hr/>

<p><span style="color: orange">2014-11-13</span> <a href="https://bitcointalk.org/index.php?topic=822498.msg9546828#msg9546828" target="_blank">bsunau7</a>: Starting point is derived from the block you are mining so effectively the starting point is random.  The "absolute end point" is defined by the "shift" which you get to pick. People only mine part of the "space" which is defined by the sieve size. Difficulty is logarithmic, it is on the gapcoin website, so a difficulty or 23 is significantly harder than one of 22. Summary; random range of numbers are scanned looking for a run (currently a few thousand) of composite numbers.</p>

<hr/>

<p><span style="color: orange">2014-11-13</span> <a href="https://bitcointalk.org/index.php?topic=822498.msg9356583#msg9356583" target="_blank">Supercomputing</a>: Make no mistake about it, this is a GPU coin for AMD R9 and Nvidia Maxwell GPUs. The algorithm used for this coin falls in the sweet spot as afar as GPU register usage is concerned for modular arithmetic implementation (512-bit or less). Also, sieving is much faster on these GPUs.</p>

<hr/>

<p><span style="color: orange">2014-11-13</span> <a href="https://bitcointalk.org/index.php?topic=822498.msg9359453#msg9359453" target="_blank">Supercomputing</a>: I will not have time this coming weekend. But during the following weekend, I will integrate Gapcoin mining with the open source Primecoin miner below. Less than an hour's worth of work: <a href="https://github.com/eXtremal-ik7/xpmclient" target="_blank">https://github.com/eXtremal-ik7/xpmclient</a></p>

<hr/>

<p><span style="color: orange">2014-11-13</span> <a href="https://bitcointalk.org/index.php?topic=822498.msg9537739#msg9537739" target="_blank">Supercomputing</a>: No worries, I will help Gapcoin break the world record. I still need to optimize the GPU miner for Nvidia (Maxwell) with 2GB of VRAM. For now it only works on R9 cards with 3+ GB of VRAM.</p>

<hr/>

<p><span style="color: orange">2014-11-13</span> <a href="https://bitcointalk.org/index.php?topic=822498.msg9525963#msg9525963" target="_blank">Supercomputing</a>: ... my implementation of the GPU miner is deadly and will surely kill the coin without a doubt. The coin is too young and let us give it some time to grow. I have mined enough BTCs and XPMs therefore I am going to shelve it at this time.<br/><br/>GPU Miner Test Run:
<pre>
[2014-11-12 17:32:17] pps: 0 / 0.0000 10g/h 0.0000 / 0.0000  15g/h 0.0000 / 0.0000</pre>

<p>We found our gap...</p>
<pre>1054835642665510130316115181531813465485913069989570483763342784779359674641399 765143
[2014-11-12 17:32:24] Found Share: 22.8244760624  =>  accepted
[2014-11-12 17:32:27] pps:  0 / 0.0000  10g/h 0.0000 / 0.0000  15g/h 0.0000 / 0.0000
[2014-11-12 17:32:28] Got new target: 22.5718696617


[2014-11-12 17:34:40] pps: 0 / 0.0000 10g/h 0.0000 / 0.0000  15g/h 0.0000 / 0.0000
</pre>
<p>We found our gap...</p>

<pre>1460023432727399844421086333295273985776598611867186573289828851669587467837029 674331
[2014-11-12 17:34:41] curl_easy_perform() failed: Failed initialization
[2014-11-12 17:34:41] waiting for gapcoind ...
[2014-11-12 17:34:41] Found Share: 22.8490689436  =>  accepted
[2014-11-12 17:34:46] Got new target: 22.5826074437</pre>

<hr/>

<p><span style="color: orange">2014-11-13</span> <a href="https://bitcointalk.org/index.php?topic=822498.msg9547094#msg9547094" target="_blank">Supercomputing</a>: In addition, please see the proof-of-work verification code for restrictions - see lines 99 onwards:
<a href="https://github.com/gapcoin/Gapcoin-PoWCore/blob/master/src/PoW.cpp" target="_blank">https://github.com/gapcoin/Gapcoin-PoWCore/blob/master/src/PoW.cpp</a>. Also, because the merit of the gap is the ratio of the gap size relative to the natural logarithm of the smaller prime, the size of the prime does not have to increase by much as the difficulty increases.</p>

<hr />
<p>The dcct's optimisation uses an idea to skip prime tests for a range of numbers between two primes if it is less than the gap minimum length. This works only for sequential searching.</p>

<hr/>

<p><span style="color: orange">2014-11-20</span> <a href="https://bitcointalk.org/index.php?topic=822498.msg9606135#msg9606135" target="_blank">angelovAlex</a>: for experiment decided to create a cuda miner in free time. I rewrite mpz's powmod function for cuda and ran it on my old 9600gt.</p>

<hr/>

<p><span style="color: orange">2014-11-21</span> <a href="https://bitcointalk.org/index.php?topic=822498.msg9610528#msg9610528" target="_blank">Palmdetroit</a>: “Seems like the gpu miner isn't fully optimized yet and still uses a good amount of the cpu also.”<br/><br/>I think lots of gpu speed issues may be cpu related, look at gpu usage to see if there's a bottleneck. Hopefully someone can improve on the cpu part of the gpu miner, even small improvements would likely bump speeds.</p>

<hr/>

<p><span style="color: orange">2014-11-21</span> <a href="https://bitcointalk.org/index.php?topic=822498.msg9610528#msg9610528" target="_blank">SpeedDemon13</a>: The GPU usage is between 80%~95% fluctuations and the cpu is around 50% usage. I'm mining the AMD cpu on a different rig than the gpu, just to see how they both do. The the gpu is teamed with a Core i5. Hopefully, the gpu miner will be optimized in the near. But for now, cpu mining is better at the moment...

<hr/>

<p><span style="color: orange">2014-12-06</span> <a href="https://bitcointalk.org/index.php?topic=822498.msg9761793#msg9761793" target="_blank">altpooler</a>: Best I've been able to get with a radeon 7970 is between 1,500,000 - 1,700,000 PPS with the following settings:<br/>
<pre>
    -g -j 5 -n 4 -w 1000 -i 50000

The flags used above are explained below:

Enable GPU mining:
-g

Stats interval (in the settings above, I have stats printing every 5 seconds):
-j

Number of tests per gap per gpu run:
-n

Number of primes for sieving:
-i

Tried many different values for the -n and -i flags and actually had it around 2,000,000 PPS, but the test/s kept going to 0. I preferred stability so I adjusted the settings to lower the PPS and keep tests/s high.

A few other settings that may have an effect on PPS, just for some quick reference. These can all be seen by running the help command ./gapminer -h:
--work-items (gpu work items - default: 2048)
--queue-size (gpu waiting queue size - note: memory intensive)
--sieve-size (prime sieve size)
--shift (the adder shift)
</pre></p>

<hr/>

<p><span style="color: orange">2015-04-16</span> <a href="https://bitcointalk.org/index.php?topic=822498.msg11109264#msg11109264" target="_blank">pdazzl</a>: “How do you attempt particular records?”<br/><br/>I don't have solid proof this is always true but I seem to have had the best luck on large shift block hits when mining solo at night (during night time the large firepower pool miners don't mine as hard making the rounds longer though I've gotten large shift records on both solo and pool).<br/><br/>All you do is append --shift (bigger number than default 25).  Example:<pre>
./gapminer -o mine3.gap.nonce-pool.com -p 3385 -u &lt;user.worker> -x &lt;password> -c -t 16 --shift 256</pre>The default <code>--sieve-size</code> and <code>--sieve-primes</code> have worked fine for me when being speculative with large shifts.  A shift of 256 has gotten me into the 8000-9998 list several times.  Did some calculations and shift 380 &amp; 381 got into the 10000-14998 range which if you solve any block with difficulty 22-23 you have a very good probability of a world record every time with where the records are.<br/><br/>Keep in mind, these higher shifts will severely punish your pps rate since you're looking for larger overall gaps AND all the numbers you're testing are bigger: shift 25 are 85 digit numbers vs shift 256 are 155 digit numbers.....which is why solo mining probably gives you better odds (with a solo target you're putting all your chips in the middle to solve the block, not accumulate shares/coins).<br/><br/>If nscythe or skif (the two powerhouse pool miners) are reading this, they could probably set a couple hundred new world records within a week with these higher shifts if they really wanted to.  Gapcoin taking over more of the record lists I would think could only help it.<br/><br/>EDIT: Just set another record a few minutes ago with length @ 11202 (on block #109634). You can see it was set with shift 391 from <a href="https://chainz.cryptoid.info/gap/block.dws?9248f5e0765cd8618f55aea2c3c46270b0304eb14be32a6ae879d9198134cfb9" target="_blank">the block record</a></p>

<hr/>

<p><span style="color: orange">2015-04-226</span> <a href="https://bitcointalk.org/index.php?topic=822498.msg11166207#msg11166207" target="_blank">pdazzl</a>: “So many questions...Like what shift means exactly.”<br/><br/>All shift does is affect the size of the numbers you are searching.  Larger shifts means bigger raw numbers you are scanning/testing and subsequently larger gaps are found in larger number ranges (though you need larger overall gap lengths to get equivalent merit scores to solve the block compared to smaller number ranges).<br/><br/>A block solution is calculated by <code>sha256(Blockheader) * 2^shift + adder</code>.  During a particular round, the miner is searching through all the "adder" possibilities to find a gap.<br/><br/>An example of what shift does using solved block <a href="https://chainz.cryptoid.info/gap/block.dws?d6173fb8d38ec64dabb92d9af96290e68d02c3494f758d7274931fecb4c60490" target="_blank">#113196</a>
<pre>256 bit hash = 96836026872238572127838827186667600687197793668933440162407221099313404183696 
(Hash is stored in hexadecimal format of d6173fb8d38ec64dabb92d9af96290e68d02c3494f758d7274931fecb4c60490)
Shift = 32
Adder = 739033261</pre>Solution is <math>(96836026872238572127838827186667600687197793668933440162407221099313404183696) * (2<sup>32</sup>) + 739033261</math>. That's the first prime before the gap of length 5034 begins.  The last prime that ends the gap would be of course plus 5034 to the solution above.<br/><br/>The number above is 87 digits number long, 13 digits away from a <a href="https://en.wikipedia.org/wiki/Googol" target="_blank">googol</a>.  Theoretically if the shift was instead 381 then the resultant number would 192 digits.<br/><br/>It's up to you how you do the shifts, I personally think a wider dragnet (different simultaneous shifts on different machines) will yield more solutions.  Also different shifts seem like they have better yields in my observation but I don't have concrete proof of that.</p>

<hr/>