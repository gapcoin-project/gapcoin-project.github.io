---
layout: paramtest 
title: Performance “noise level” variance, non-crt (n=1396) and crt (n=3011)
description: Variance report non-crt <b>-f 25</b> (1396 reports) and <b>-f 64 crt-22m-64s</b> (3011 reports)
author: Graham Higgins
testdir: variancereport-0
tests: variancereport-0-01 variancereport-0-01crt
---

<div class="ui raised padded container segment">
  <p>Comparison between reported performance of GapMiner for non-crt and crt mining. Of note is the value for <code>std</code> (<a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.std.html#pandas.DataFrame.std" target="_blank">standard deviation</a>). Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second, <code>gps</code> is average gaps per second and, for crt mining, glst is the size of the gap list.</p>
  <a href="pandasvariancetest"></a>
  <p>This basic level of “noise” in the miner’s reported performance statistics sets a base level of granularity that should be acknowledged when devising tests to compare the results from one mining parameter setting value against a different setting value.</p>
  <a href="pandasvariancetest"></a>
  <div style="font-family: monospace; font-size:85%">
    <hr>
    <p>Pandas <a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.describe.html" target="_blank">“describe”</a> summary of variance</p>
    <pre><code class="nohighlight">
-t 2 -f 25 -s 33554432 -i 900000                      -t 2 -d 1 -f 64 -i 16300 -r crt-22m-64s
                 pps           tps           gps                       pps           tps          gps          glst
count    1396.000000   1396.000000   1396.000000      count    3011.000000  3.011000e+03  3011.000000   3011.000000
mean   201345.737106  93362.854585  14059.191261      mean   296615.872800  2.209359e+08  4175.967453  11873.141481
std      1162.504695    205.418244     30.552968      std     17684.741105  1.273910e+08     8.655627   8514.218057
min    200037.000000  93149.000000  14027.000000      min    190954.000000  1.833550e+05  4167.000000      0.000000
25%    200862.000000  93187.000000  14032.000000      25%    283217.500000  1.108248e+08  4173.000000   4577.000000
50%    201320.000000  93275.000000  14047.000000      50%    296408.000000  2.208485e+08  4174.000000  10506.000000
75%    201500.000000  93536.250000  14085.000000      75%    313735.000000  3.309344e+08  4178.000000  17734.000000
max    213954.000000  96321.000000  14466.000000      max    363381.000000  4.416700e+08  4446.000000  38080.000000

Correlation between columns
                  pps       tps       gps                                pps       tps       gps
        pps  1.000000  0.236737  0.201119                     pps   1.000000  0.510353 -0.408007
        tps  0.236737  1.000000  0.997566                     tps   0.510353  1.000000 -0.414272
        gps  0.201119  0.997566  1.000000                     gps  -0.408007 -0.414272  1.000000</code></pre>
  </div>
  <hr>
  <p style="font-size: 80%; text-align:center"><em>The charts included below are for completeness. The figures given are the means and they differ from the pandas-produced means because, in order to support the different requirements of charting, the first 1/5th of the data is ignored in order to aid visual comparison. The chartline uses the full dataset.</em></p>
</div>


{% include paramtest.html %}

<div class="ui raised padded container segment">
  <p>Replication: 
  <pre style="font-size:75%"><code class="bash">gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 2
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 2 -d 1 -f 64 -i [as-discovered] -r crt/crt-22m-0064s.txt</code></pre>
</p>
</div>
