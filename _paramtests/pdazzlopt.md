---
layout: paramtest
title: Default vs pdazzl’s optimised crt files for shifts 416, 480, 512 and 1024
description: pdazzl’s optimised crt files vs default for <code>-t 4 -d 3 -f 416 480 512 1024</code>, -i as discovered
author: Graham Higgins
testdir: pdazzloptretrial
tests: default-i60000-crt416 pdazzl-i60000-crt416 default-i80000-crt480 pdazzl-i80000-crt480 default-i90000-crt512 pdazzl-i90000-crt512 default-i250000-crt1024 pdazzl-i250000-crt1024
---

<div class="ui raised padded container segment">
  <p>Comparison between reported performance of GapMiner when using pdazzl’s optimised crt files for shifts of 416, 480, 512 and 1024. Of note is the value for <code>std</code> (<a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.std.html#pandas.DataFrame.std" target="_blank">standard deviation</a>). Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second, <code>gps</code> is average gaps per second and <code>glst</code> is the size of the gaplist.</p>
  <a href="pandasvariancetest"></a>
  <p>This basic level of “noise” in the miner’s reported performance statistics sets a base level of granularity that should be acknowledged when devising tests to compare the results from one mining parameter setting value against a different setting value.</p>
  <div style="font-family: monospace; font-size:80%">
    <hr>
    <p>Pandas <a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.describe.html" target="_blank">“describe”</a> summary of variance</p>
    <pre class="nohighlight">
                pps           tps         gps          glst                      pps           tps         gps          glst
default-i60000-crt416                                            pdazzl-i60000-crt416
mean   1.904381e+06  1.875603e+06  406.386935  15935.668342      mean   2.128678e+06  6.743273e+06  787.065327   6516.095477
std    4.076343e+04  1.173270e+06   12.240273  11414.505983      std    7.578296e+04  3.811199e+06   23.648110   4335.415428
min    1.854059e+06  1.219500e+04  399.000000     61.000000      min    2.077549e+06  7.555800e+04  772.000000     98.000000
max    2.067848e+06  4.620588e+06  455.000000  46061.000000      max    2.617708e+06  1.325469e+07  961.000000  15928.000000

default-i80000-crt480                                            pdazzl-i80000-crt480
mean   2.934127e+06  5.205335e+06  571.869347   6509.261307      mean   5.321534e+06  5.114632e+06  565.733668   3512.713568
std    5.156301e+04  2.988033e+06    3.675336   4417.523389      std    1.428435e+05  2.958942e+06    2.423459   2543.327559
min    2.815074e+06  4.114600e+04  569.000000    282.000000      min    4.285718e+06  3.541100e+04  554.000000     45.000000
max    3.049290e+06  1.032935e+07  605.000000  15941.000000      max    5.494903e+06  1.018838e+07  578.000000  10116.000000

default-i90000-crt512                                            pdazzl-i90000-crt512             
mean   3.834104e+06  5.065043e+06  519.236181   5024.030151      mean   5.473705e+06  5.029057e+06  517.035176  3276.718593
std    6.444532e+04  2.925852e+06    2.009949   3080.300889      std    8.815041e+04  2.906075e+06    2.357830  2080.763829
min    3.403485e+06  3.560600e+04  504.000000    158.000000      min    4.704741e+06  3.544100e+04  508.000000    37.000000
max    4.123994e+06  1.009384e+07  522.000000  11954.000000      max    5.951581e+06  1.001841e+07  536.000000  7413.000000

default-i250000-crt1024                                          pdazzl-i250000-crt1024
mean   3.056781e+06  7.516939e+05   79.462312   7908.015075      mean   4.779540e+06  7.444908e+05   78.788945   9923.065327
std    8.471553e+04  4.318201e+05    1.013712   6230.713944      std    2.098293e+05  4.320028e+05    3.877633   6528.864248
min    2.992165e+06  2.574000e+03   75.000000      0.000000      min    1.907264e+06  8.510000e+02   25.000000     51.000000
max    3.644344e+06  1.493372e+06   85.000000  23903.000000      max    4.839087e+06  1.488375e+06   82.000000  23184.000000</pre>
  </div>
</div>

{% include paramtest.html %}

<div class="ui raised padded container segment">
  <p>Replication: 
  <pre style="font-size:80%"><code class="bash"># 416
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 2 -d 1 -f 416  -i  60000 -r crt/crt-22m-0416s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 2 -d 1 -f 416  -i  60000 -r pdazzl/crt-22m-0416s.txt
# 480
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 2 -d 1 -f 480  -i  80000 -r crt/crt-22m-0480s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 2 -d 1 -f 480  -i  80000 -r pdazzl/crt-22m-0480s.txt
# 512
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 2 -d 1 -f 512  -i  80000 -r crt/crt-22m-0512s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 2 -d 1 -f 512  -i  80000 -r pdazzl/crt-22m-0512s.txt
# 1024
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 2 -d 1 -f 1024 -i 250000 -r crt/crt-22m-1024s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 2 -d 1 -f 1024 -i 250000 -r pdazzl/crt-22m-1024s.txt</code></pre>
</p>
</div>
