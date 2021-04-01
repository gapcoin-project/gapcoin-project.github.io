---
layout: paramtest
title: Comparison of mining on shift64 22m vs wizz’ 28m
description: Test of shift64 22m vs 28m (n=199)
author: Graham Higgins
testdir: shift64merittest
tests: dist-22m-crt0064 wizz-28m-crt0064
---


<div class="ui raised padded container segment">
 <p>Testing wizz’ optimised 28m shift 64 crt (<code>-i 5750</code>) vs standard 22m (<code>-i 5500</code>)</p>
  <a href="pandasvariancetest"></a>
  <div style="font-family: monospace; font-size:65%">
    <hr>
    <p>Pandas <a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.describe.html" target="_blank">“describe”</a> summary of variance</p>
    <pre><code class="nohighlight">                 pps           tps          gps           glst         bpc                      pps           tps           gps           glst         bpc
dist-22m-crt0064                                                                wizz-28m-crt0064
mean   763168.934673  4.410157e+06  5328.482412  153463.798995    0.564965      mean   4.774940e+07  4.403190e+06   5622.447236  130792.110553   26.872121
std     32608.790582  2.585037e+06   252.576278  106432.996058    0.318103      std    1.173841e+07  2.563592e+06   1520.263971   89163.657421   15.830843
min    503299.000000  6.171200e+04  5123.000000    6044.000000    0.002000      min    4.288011e+07  1.866390e+05   5278.000000    3940.000000    0.202000
25%    751210.000000  2.057210e+06  5227.000000   64903.000000    0.303000      25%    4.586751e+07  2.067770e+06   5357.000000   55848.500000   12.669500
50%    765174.000000  4.573663e+06  5331.000000  137936.000000    0.571000      50%    4.657821e+07  4.558328e+06   5390.000000  116547.000000   27.204000
75%    779886.000000  6.592802e+06  5372.000000  224491.500000    0.830000      75%    4.694375e+07  6.568596e+06   5453.500000  189861.500000   40.402500
max    886978.000000  8.920162e+06  8350.000000  407817.000000    1.120000      max    1.928255e+08  8.882274e+06  24518.000000  350037.000000   54.754000</code></pre>
  </div>
</div>


{% include paramtest.html %}

<div class="ui raised padded container segment">
  <p>Replication: 
  <pre style="font-size: 80%"><code class="bash">gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -d 3 -f 64 -i 5500 -r crt/crt-22m-0064s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -d 3 -f 64 -i 5750 -r crt/crt-28m-0064s-wizz.txt</code></pre>
</p>
</div>
