---
layout: paramtest
title: Basic test of CRT f=512 with t=4&#58; and d varying through 1 to 3
description: CRT fermat threads test&#58; -f 512 -t 4 -d 1 (-i 720000), 2 (-i 120000), 3 (-i 115000)
author: Graham Higgins
testdir: fermatthreads
tests: t4-d1-i720000-22m-crt0512 t4-d2-i120000-22m-crt0512 t4-d3-i115000-22m-crt0512 t4-d1-i13000-22m-crt0512
---

<div class="ui raised padded container segment">
  <p>Comparison between reported performance of GapMiner on CRT mining at a shift of 512 with a varying number of threads devoted to Fermat tests of primality of the gap list contents, as described by j0nn9 in <a href="https://bitcointalk.org/index.php?topic=822498.msg11296309#msg11296309" target="_blank">announcing Gapminer mining with the Chinese Remainder Theorem</a> (CRT):</p>
  <blockquote style="font-size:80%"><p>Mining with the CRT is split into sieve and primality testing using separate threads for each.</p> 
  <p>Setting the parameters <code style="color:orange">  --threads 4 --fermat-threads 1  </code> means: use 3 sieve threads and 1 gap scan thread.</p>
  <p>The scan threads always pick the most promising gap from the gaplist, therefore the gaplist value should always be at least over 100, but a too high gaplist value can slow down mining, (for example over 9000). You can alter <code>--sieve-primes</code>, <code>--threads</code> or <code>--fermat-threads</code> to achieve this.</p>
  </blockquote>
  <p>Tests are of increasing values of <code>--fermatthreads</code> from 1 to 3 where total threads is 4. In order to keep the size of the gaplist within the recommended bounds, the value of <code>--sieve-primes</code> is adjusted according to the selected value of <code>--fermat-threads</code>. The included chart for <code>-t 4 -d1 -i 13000 -r 22m-crt0512</code> is something of a worst-case example and illustrates the cost of selecting an inappropriate value for <code>--sieve-primes</code> (in this instance, 13000) which results in an excessive gap list that takes a lot of time to scan, reducing performance significantly.</p>
  <p>Tests were run simultaneously to control for changes in difficulty that otherwise affect the results to a dergee that thwarts comparison when tests are run serially.</p>
  <p style="font-size: 80%"><em>Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second, <code>gps</code> is average gaps per second, <code>glst</code> is the size of the gaplist and <code>l/s</code> is the time in seconds to scan the gaplist at the reported rate of gaps per second.</em></p>
  <div style="font-family: monospace; font-size:90%">
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">t4-d1-i720000-22m-crt0512</p>
            <table>
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">1040689</td><td align="right">541175</td><td align="right">106</td><td align="right">3672</td><td align="right">0.59</td><td align="right">34.50</td></tr>
                <tr><td align="left">max</td><td align="right">2145069</td><td align="right">1065529</td><td align="right">130</td><td align="right">10544</td><td align="right">1.16</td><td align="right">81.11</td></tr>
                <tr><td align="left">min</td><td align="right">993910</td><td align="right">5535</td><td align="right">105</td><td align="right">112</td><td align="right">0.01</td><td align="right">1.07</td></tr>
                <tr><td align="left">std</td><td align="right">104575</td><td align="right">308565</td><td align="right">2</td><td align="right">2725</td><td align="right">0.34</td><td align="right">1147.38</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">t4-d2-i120000-22m-crt0512</p>
            <table>
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">2183195</td><td align="right">1463491</td><td align="right">285</td><td align="right">1804</td><td align="right">0.65</td><td align="right">6.32</td></tr>
                <tr><td align="left">max</td><td align="right">3826268</td><td align="right">2874007</td><td align="right">354</td><td align="right">5585</td><td align="right">1.49</td><td align="right">15.78</td></tr>
                <tr><td align="left">min</td><td align="right">2119943</td><td align="right">11716</td><td align="right">280</td><td align="right">10</td><td align="right">0.01</td><td align="right">0.04</td></tr>
                <tr><td align="left">std</td><td align="right">168763</td><td align="right">830941</td><td align="right">9</td><td align="right">1375</td><td align="right">0.40</td><td align="right">159.63</td></tr>
            </table>
        </div>
    </div>
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">t4-d3-i115000-22m-crt0512</p>
            <table>
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">2232791</td><td align="right">1454262</td><td align="right">285</td><td align="right">2755</td><td align="right">1.29</td><td align="right">9.65</td></tr>
                <tr><td align="left">max</td><td align="right">3600458</td><td align="right">2845990</td><td align="right">342</td><td align="right">7581</td><td align="right">2.51</td><td align="right">22.17</td></tr>
                <tr><td align="left">min</td><td align="right">2133573</td><td align="right">12110</td><td align="right">278</td><td align="right">102</td><td align="right">0.01</td><td align="right">0.37</td></tr>
                <tr><td align="left">std</td><td align="right">143957</td><td align="right">815918</td><td align="right">9</td><td align="right">2080</td><td align="right">0.72</td><td align="right">221.59</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">t4-d1-i13000-22m-crt0512</p>
            <table>
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">904401</td><td align="right">92297</td><td align="right">37</td><td align="right">259672</td><td align="right">0.49</td><td align="right">6970.83</td></tr>
                <tr><td align="left">max</td><td align="right">1123260</td><td align="right">183486</td><td align="right">44</td><td align="right">744146</td><td align="right">0.96</td><td align="right">16912.41</td></tr>
                <tr><td align="left">min</td><td align="right">882441</td><td align="right">1148</td><td align="right">36</td><td align="right">3299</td><td align="right">0.00</td><td align="right">91.64</td></tr>
                <tr><td align="left">std</td><td align="right">30035</td><td align="right">52192</td><td align="right">1</td><td align="right">194535</td><td align="right">0.28</td><td align="right">204349.55</td></tr>
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
  <pre style="font-size:85%"><code class="bash">gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -d 1 -f 512 -i 720000 -r crt/crt-22m-0512s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -d 2 -f 512 -i [as-discovered] -r crt/crt-22m-0512s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -d 3 -f 512 -i [as-discovered] -r crt/crt-22m-0512s.txt</code></pre>
</p>
</div>

<!--
  d4-i13000-crt0512 d4-i350000-crt0512 d5-i13000-crt0512 d5-i225000-crt0512 d6-i13000-crt0512 d6-i120000-crt0512 d7-i13000-crt0512 d7-i50000-crt0512
-->
