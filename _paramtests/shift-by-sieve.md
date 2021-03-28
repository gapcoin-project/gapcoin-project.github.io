---
layout: paramtest
title: shift at different sievesizes
description: sieve test -s 31457280 -i 13000,50000,100000,900000 -f 15,24,32,48,96,128,,256,512
author: Graham Higgins
tests: sieve-15-13000 sieve-15-50000 sieve-15-100000 sieve-15-900000 sieve-24-13000 sieve-24-50000 sieve-24-100000 sieve-24-900000 sieve-32-13000 sieve-32-50000 sieve-32-100000 sieve-32-900000 sieve-48-13000 sieve-48-50000 sieve-48-100000 sieve-48-900000 sieve-96-13000 sieve-96-50000 sieve-96-100000 sieve-96-900000 sieve-128-13000 sieve-128-50000 sieve-128-100000 sieve-128-900000 sieve-256-13000 sieve-256-50000 sieve-256-100000 sieve-256-900000 sieve-512-13000 sieve-512-50000 sieve-512-100000 sieve-512-900000 
---

<div class="ui raised very padded container segment">
  <div style="font-style:italic; font-size:90%">
    <p><a href="https://bitcointalk.org/index.php?topic=822498.msg10687403#msg10687403" target="_blank">pdazzl</a></p>
    <p>I’ll venture a hypothesis from various things I’ve read on this whole thread.  The miner sets up the sieve, in the default case <math>2^25</math> (the shift being <tt>25</tt>) and the resultant value as the required sieve size - <math>33554432</math>.  Now the question is how many primes to use.</p>
    <p>All the primes chosen are (from my understanding) each multiplied by <math>3</math>, then the miner starts with the highest value <tt>prime*3</tt> and works backwards scanning for the desired gap length and not bothering with sections that obviously won’t net a coin. So the largest prime value(times 3) would ideally stop just short of the end of the sieve.</p>
    <p>So here is where a bit of math leg work comes in if you want to be precise.  Absolute value of <math>33554432/3</math> is <math>11184810</math>.  The first prime less than that is <math>11184799</math>.  <math>11184799*3</math> is <math>33554397</math> which fits nicely near the top of the seive.  A check of bigprimes.net shows it as the <math>737948</math>th prime and thus the number of primes for shift <tt>25</tt>.</p> 
    <p>Can someone verify if this logic is correct?  I think the default primes is <math>500000</math>,  Maybe it could be more efficient?  Also we could build a table of primes for different shift values¹, perhaps blocks would be found faster if everyone wasn’t trying to scan <math>2^25</math> at the same time on each round.</p>
  </div>
  <hr style="margin:1.5em 1em;" />
  <div style="font-size:90%">
    <p><a href="https://bitcointalk.org/index.php?topic=822498.msg10765912#msg10765912" target="_blank">j0nn9</a></p>
    <p>Since revision 4, the default values are the same as from dcct’s mod:
    <code><pre class="plaintext">     --shift 25 --sieve-primes 900000 --sieve-size 33554432</pre></code></p>
    <p>In the beginning, we sieve with the first <math>n</math> primes. For the first <math>2063689</math> primes, every prime eliminates at least one candidate in the sieve. For the primes behind that point, the possibility for eliminating a prime candidate in the sieve decreases.</p>
    <p>After sieving, the remaining prime candidates are scanned for prime gaps. When a prime is found while scanning the gap, the whole gap is skipped and the miner scans the next possible gap in the sieve.</p>
    <p>A more detailed description can be found here: <a href="https://github.com/gapcoin/Gapcoin-PoWCore" target="_blanK">https://github.com/gapcoin/Gapcoin-PoWCore</a></p>
  </div>
  <hr style="margin:1.5em 1em;" />
  <p style="font-style:italic;margin-top:1.5em;">¹ Now available on this web site as <a href="/gapgraphs/shiftfrequency/#shifts" target="_blank">Number of blocks mined at shift setting</a></p>
</div>

{% include paramtest.html %}

