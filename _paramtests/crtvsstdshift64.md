---
layout: paramtest
title: Performance test of non-crt vs crt on shift64
description: crtvsstdshift64 -f 64 -t 4 std vs crt
author: Graham Higgins
testdir: crtvsstdshift64
tests: std-f64 crt-f64
---

<div class="ui raised padded container segment">
 <p>Testing non-crt shift 64 vs crt</p>
  <a href="pandasvariancetest"></a>
  <div style="font-family: monospace; font-size:65%">
    <hr>
    <p>Pandas <a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.describe.html" target="_blank">“describe”</a> summary of variance</p>
    <pre><code class="nohighlight">                 pps            tps           gps                        pps           tps           gps          glst
std-f64                                                  crt-f64
mean   444281.994975  160246.025126  21173.929648        mean   8.560806e+05  1.731806e+07  10565.572864  29749.185930
std     14214.159581    5219.951684    678.382014        std    3.353770e+04  1.000349e+07    241.851389  19781.975277
min    432458.000000  155926.000000  20610.000000        min    8.001790e+05  1.801880e+05  10451.000000    607.000000
25%    435116.000000  156880.500000  20734.500000        25%    8.382725e+05  8.680316e+06  10522.000000  12171.500000
50%    438823.000000  158236.000000  20913.000000        50%    8.498470e+05  1.733635e+07  10526.000000  27753.000000
75%    447374.500000  161357.000000  21323.500000        75%    8.669700e+05  2.587986e+07  10534.500000  45925.000000
max    513592.000000  185498.000000  24478.000000        max    1.011433e+06  3.451516e+07  13595.000000  73356.000000</code></pre>
  </div>
</div>


{% include paramtest.html %}

<div class="ui raised padded container segment">
  <p>Replication: 
  <pre style="font-size: 80%"><code class="bash">timeout 1000s gapminer -o localhost -p 31397 -u $USER -x $USERPASS -j 5 -e -f 64 -t 4
timeout 1000s gapminer -o localhost -p 31397 -u $USER -x $USERPASS -j 5 -e -f 64 -i 5200 -t 4 -d 3 -r crt/dist/crt-22m-0064s.txt</code></pre>
</p>
</div>
