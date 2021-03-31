---
layout: paramtest
title: Comparison of variance of shift settings 20-23 (all have primedigit length of 84)
description: shift test (defaults of -s 33554432 -i 900000) and -f 21, 22, 23
author: Graham Higgins
testdir: earlytwenties
tests: default-21-33554432-900000 default-22-33554432-900000 default-23-33554432-900000
---

<div class="ui raised padded container segment">
  <p>Comparison between reported performance of GapMiner with successive shift settings of 21, 22, 23 - all of which map to a prime digits length of 84, so performance results should not differ significantly. Of note is the value for <code>std</code> (<a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.std.html#pandas.DataFrame.std" target="_blank">standard deviation</a>). Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second and <code>gps</code> is average gaps per second.</p>
  <a href="pandasvariancetest"></a>
  <p>This basic level of “noise” in the miner’s reported performance statistics sets a base level of granularity that should be acknowledged when devising tests to compare the results from one mining parameter setting value against a different setting value.</p>
  <div style="font-family: monospace; font-size:62%">
    <hr>
    <p>Pandas <a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.describe.html" target="_blank">“describe”</a> summary of variance</p>
    <pre class="nohighlight">
default-21-33554432-90                               default-22-33554432-90                               default-23-33554432-90
                 pps           tps           gps                      pps           tps           gps                      pps           tps           gps
mean   223197.200803  69678.429719  10643.638554     mean   225900.622490  70690.445783  10761.903614     mean   226166.381526  71047.144578  10767.064257
std      2040.689415    593.217597     97.051314     std      1897.323202    574.487287     93.137942     std      3208.058791   1012.423591    152.926756
min    221148.000000  69010.000000  10546.000000     min    223809.000000  70026.000000  10659.000000     min    185094.000000  58140.000000   8811.000000
25%    222198.000000  69379.000000  10596.000000     25%    224292.000000  70187.000000  10683.000000     25%    226295.000000  71087.000000  10773.000000
50%    222953.000000  69639.000000  10633.000000     50%    225261.000000  70492.000000  10730.000000     50%    226492.000000  71145.000000  10783.000000
75%    223539.000000  69797.000000  10660.000000     75%    227489.000000  71207.000000  10841.000000     75%    226794.000000  71250.000000  10798.000000
max    236536.000000  73499.000000  11279.000000     max    235089.000000  72705.000000  11199.000000     max    227902.000000  71570.000000  10849.000000</pre>
  </div>
  <hr>
  <p style="font-size: 80%; text-align:center"><em>The charts included below are for completeness. The figures given are the means and they differ from the pandas-produced means because, in order to support the different requirements of charting, the first 1/5th of the data is ignored in order to aid visual comparison. The chartline uses the full dataset.</em></p>
</div>


{% include paramtest.html %}

<div class="ui raised padded container segment">
  <p>Replication: 
  <pre><code class="bash">gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 1 -f 21
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 1 -f 22
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 1 -f 23</code></pre>
</p>
</div>
