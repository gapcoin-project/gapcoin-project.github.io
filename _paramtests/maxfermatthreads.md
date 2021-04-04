---
layout: paramtest
title: Focussed comparison test of CRT f=512 with t=6&#58; and d=3 vs. d=5
description: CRT fermat threads test&#58; -f 512 -t 6 -d 3 (-i 320000) vs -d 5 (-i 72000)
author: Graham Higgins
testdir: maxfermatthreads
tests: t6-d3-i340000-22m-crt0512 t6-d5-i74000-22m-crt0512
---

<div class="ui raised padded container segment">
  <p>Comparison between reported performance of GapMiner on CRT mining at a shift of 512 with a varying number of threads devoted to Fermat tests of primality of the gap list contents, as described by j0nn9 in <a href="https://bitcointalk.org/index.php?topic=822498.msg11296309#msg11296309" target="_blank">announcing Gapminer mining with the Chinese Remainder Theorem</a> (CRT):</p>
  <blockquote style="font-size:80%"><p>Mining with the CRT is split into sieve and primality testing using separate threads for each.</p> 
  <p>Setting the parameters <code style="color:orange">  --threads 4 --fermat-threads 1  </code> means: use 3 sieve threads and 1 gap scan thread.</p>
  <p>The scan threads always pick the most promising gap from the gaplist, therefore the gaplist value should always be at least over 100, but a too high gaplist value can slow down mining, (for example over 9000). You can alter <code>--sieve-primes</code>, <code>--threads</code> or <code>--fermat-threads</code> to achieve this.</p>
  </blockquote>
  <p>These tests are intended to validate the advice “<span style="color:orange">for best performance, set the number of fermat threads to be 1 less than the number of threads</span>”. Tests are of two values of <code>--fermatthreads</code>: 3 and 5, where total threads is 6. In order to keep the size of the gaplist within the recommended bounds, the value of <code>--sieve-primes</code> is adjusted according to the selected value of <code>--fermat-threads</code>: <code>-i 320000</code> for <code>d=3</code> and <code>-i 72000</code> for <code>d=5</code> <em>(note the difference in these settings from those used in <a href="/paramtests/fermatthreads/" target="_blank">a similar test with fewer threads</a> - illustrating the effect on the gaplist size of changing the number of threads)</em>.</p>
  <p>Tests were run simultaneously to control for changes in difficulty that otherwise affect the results to a dergee that thwarts comparison when tests are run serially.</p>
  <p style="font-size: 80%"><em>Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second, <code>gps</code> is average gaps per second, <code>glst</code> is the size of the gaplist and <code>l/s</code> is the time in seconds to scan the gaplist at the reported rate of gaps per second.</em></p>
  <a href="pandasvariancetest"></a>
  <div style="font-family: monospace; font-size:90%">
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">t6-d3-i340000-22m-crt0512</p>
            <table>
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">2322779</td><td align="right">1448064</td><td align="right">297</td><td align="right">1136</td><td align="right">1.10</td><td align="right">3.82</td></tr>
                <tr><td align="left">max</td><td align="right">3209072</td><td align="right">2756395</td><td align="right">364</td><td align="right">4194</td><td align="right">2.07</td><td align="right">11.52</td></tr>
                <tr><td align="left">min</td><td align="right">2175481</td><td align="right">21532</td><td align="right">286</td><td align="right">47</td><td align="right">0.01</td><td align="right">0.16</td></tr>
                <tr><td align="left">std</td><td align="right">150657</td><td align="right">795946</td><td align="right">11</td><td align="right">929</td><td align="right">0.59</td><td align="right">83.95</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">t6-d5-i74000-22m-crt0512</p>
            <table>
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">3303191</td><td align="right">2149112</td><td align="right">442</td><td align="right">2026</td><td align="right">1.57</td><td align="right">4.59</td></tr>
                <tr><td align="left">max</td><td align="right">5270996</td><td align="right">4084036</td><td align="right">577</td><td align="right">7261</td><td align="right">2.98</td><td align="right">12.58</td></tr>
                <tr><td align="left">min</td><td align="right">3109296</td><td align="right">23424</td><td align="right">423</td><td align="right">50</td><td align="right">0.01</td><td align="right">0.12</td></tr>
                <tr><td align="left">std</td><td align="right">231830</td><td align="right">1172788</td><td align="right">18</td><td align="right">1667</td><td align="right">0.85</td><td align="right">91.48</td></tr>
            </table>
        </div>
    </div>
  </div>
  <hr>
  <p style="font-size: 80%; text-align:center"><em>The charts included below are for completeness. The figures given are the means and they differ from the means in the above table because, in order to support the different requirements of charting, the first 1/5th of the data is ignored in order to aid visual comparison. The chartline uses the full dataset.</em></p>
</div>

{% include paramtest.html %}

<div class="ui raised padded container segment">
  <p>Replication: 
  <pre style="font-size:85%"><code class="bash">
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 6 -d 3 -f 512 -i [as-discovered] -r crt/crt-22m-0512s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 6 -d 5 -f 512 -i [as-discovered] -r crt/crt-22m-0512s.txt</code></pre>
</p>
</div>
