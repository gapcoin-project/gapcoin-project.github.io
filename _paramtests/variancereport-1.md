---
layout: paramtest
title: Performance “noise level” variance non-crt mining over 10 x repeats
description: Variance report of non-crt mining with <b>-j 5 -t 1</b> (n=199) x 10
author: Graham Higgins
testdir: variancereport-1
tests: variancereport-1-01 variancereport-1-02 variancereport-1-03 variancereport-1-04 variancereport-1-05 variancereport-1-06 variancereport-1-07 variancereport-1-08 variancereport-1-09 variancereport-1-10
---

<div class="ui raised padded container segment">
  <p>Non-crt mining with <b>-j 5 -t 1</b> (n=199), repeated 10 times, with performance statistics reported at 5-second intervals, included to illustrate the variation in miner performance stemming from Gapcoin’s relatively fast-changing difficulty. Of note is the value for <code>std</code> (<a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.std.html#pandas.DataFrame.std" target="_blank">standard deviation</a>). Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second and <code>gps</code> is average gaps per second.</p>
  <p>The results of the individual tests were concatenated (“Concatenated Results” table) to provide an overall picture across 1990 miner reports and a table of the means for each report provides a picture of the top-level variation across reports (“Across Reports” table).</p>
  <a href="pandasvariancetest"></a>
  <p>This basic level of “noise” in the miner’s reported performance statistics sets a base level of granularity that should be acknowledged when devising tests to compare the results from one mining parameter setting value against a different setting value.</p>
  <div style="font-family: monospace; font-size:66%">
    <hr>
    <p>Pandas <a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.describe.html" target="_blank">“describe”</a> summary of variance</p>
    <pre class="nohighlight">
                 pps           tps          gps                     pps           tps          gps                    pps           tps          gps
Test #01                                           Test #02                                          Test #03
mean   169232.713568  51944.095477  7971.954774    mean   168364.633166  51824.452261  7942.879397   mean   168235.924623  51734.140704  7934.683417
std      1023.982552    296.337485    47.469958    std       994.894914    287.259371    45.697905   std       833.667193    285.329988    38.673005
min    168434.000000  51729.000000  7935.000000    min    162364.000000  50095.000000  7658.000000   min    167616.000000  51532.000000  7905.000000
max    177370.000000  54547.000000  8353.000000    max    170572.000000  52499.000000  8045.000000   max    177272.000000  54956.000000  8361.000000

Test #04                                           Test #05                                          Test #06
mean   167746.075377  51690.492462  7921.517588    mean   167382.371859  51537.648241  7894.507538   mean   167850.613065  51697.065327  7921.909548
std       254.475196    119.200403    12.848316    std       642.917013    183.103235    29.528940   std       496.924822    151.171689    22.180888
min    166316.000000  51569.000000  7858.000000    min    165841.000000  51167.000000  7824.000000   min    167198.000000  51486.000000  7891.000000
max    169715.000000  52726.000000  8019.000000    max    169708.000000  52490.000000  8007.000000   max    171663.000000  52966.000000  8099.000000

Test #07                                           Test #08                                          Test #09
mean   166678.924623  51339.663317  7869.542714    mean   167579.793970  51600.407035  7912.236181   mean   166914.713568  51395.341709  7878.668342
std       735.035112    214.659849    33.790754    std       915.211541    299.980825    42.959806   std       582.777825    139.488980    26.897121
min    163592.000000  50523.000000  7725.000000    min    166815.000000  51378.000000  7876.000000   min    163321.000000  50700.000000  7713.000000
max    167384.000000  51546.000000  7902.000000    max    172484.000000  53419.000000  8146.000000   max    167527.000000  51561.000000  7908.000000

Test #10                                           Concatenated results                              Across reports
count     199.000000    199.000000   199.000000    count    1990.000000   1990.000000  1990.000000   count      10.000000     10.000000    10.000000
mean   167018.502513  51395.979899  7883.316583    mean   167700.426633  51615.928643  7913.121608   mean   167700.423000  51615.928000  7913.122000
std       471.604492    166.139802    22.091300    std      1035.306442    293.321438    45.605653   std       770.426543    199.171257    32.111697
min    166532.000000  51172.000000  7857.000000    min    162364.000000  50095.000000  7658.000000   min    166678.920000  51339.660000  7869.540000
max    171866.000000  53079.000000  8111.000000    max    177370.000000  54956.000000  8361.000000   max    169232.710000  51944.100000  7971.950000</pre>
  </div>
  <hr>
  <p style="font-size: 80%; text-align:center"><em>The charts included below are for completeness. The figures given are the means and they differ from the pandas-produced means because, in order to support the different requirements of charting, the first 1/5th of the data is ignored in order to aid visual comparison. The chartline uses the full dataset.</em></p>
</div>


{% include paramtest.html %}

<div class="ui raised padded container segment">
  <p>Replication: 
  <pre style="font-size:90%"><code class="bash">for i in {1..10}
do
timeout 1000s gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 1 > run-${i}.txt 2>&1
done</code></pre>
</p>
</div>
