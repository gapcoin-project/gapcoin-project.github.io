---
layout: paramtest
title: Comparison of mining on shift64 22m vs wizz’ 28m
description: Test of shift64 22m vs 28m (n=199)
author: Graham Higgins
testdir: shift64merittest
tests: dist-22m-crt0064 wizz-28m-crt0064
---


<div class="ui raised padded container segment">
 <p>Testing wizz’ optimised 28m shift 64 crt vs standard 22m</p>
  <a href="pandasvariancetest"></a>
  <div style="font-family: monospace; font-size:65%">
    <hr>
    <p>Pandas <a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.describe.html" target="_blank">“describe”</a> summary of variance</p>
    <pre><code class="nohighlight">                 pps           tps          gps          glst         bpc                       pps           tps           gps          glst         bpc
dist-22m-crt0064                                                                wizz-28m-crt0064
mean   438841.899497  1.242629e+07  8976.919598  23384.241206    0.232925       mean   5.937507e+07  1.210524e+07   8867.356784  23020.175879   25.410221
std     32422.125932  7.074958e+06    89.387781  15974.373136    0.134989       std    4.277594e+06  6.984356e+06    190.956387  16229.481579   14.527908
min    412651.000000  1.507860e+05  8903.000000    499.000000    0.001000       min    5.409232e+07  1.174970e+05   8812.000000    135.000000    0.250000
25%    419792.000000  6.362762e+06  8915.000000   9137.500000    0.122000       25%    5.817579e+07  6.137451e+06   8823.000000   9785.500000   12.927000
50%    431631.000000  1.241440e+07  8935.000000  20815.000000    0.228000       50%    5.862697e+07  1.205152e+07   8828.000000  20262.000000   25.375000
75%    446210.000000  1.846354e+07  9000.500000  37077.500000    0.335000       75%    5.922878e+07  1.812111e+07   8865.000000  34272.500000   37.400500
max    666712.000000  2.465837e+07  9375.000000  54575.000000    0.484000       max    1.132380e+08  2.412820e+07  11157.000000  62833.000000   50.634000</code></pre>
  </div>
</div>


{% include paramtest.html %}

<div class="ui raised padded container segment">
  <p>Replication: 
  <pre style="font-size: 80%"><code class="bash">gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -d 3 -f 448 -i 65000 -r crt/crt-22m-0448s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -d 3 -f 448 -i 65000 -r crt/crt-22m-0456s.txt</code></pre>
</p>
</div>
