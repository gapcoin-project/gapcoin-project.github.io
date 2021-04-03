---
layout: paramtest
title: Performance test of non-crt vs crt on shift64
description: crtvsstdshift64 -f 64 -t 4 std vs crt
author: Graham Higgins
testdir: crtvsstdshift64
tests: std-f64-s33554397-i90000 crt-f64-s33554397-i4500 std-f96-s33554397-i90000 crt-f96-s33554397-i10500 std-f128-s33554397-i90000 crt-f128-s33554397-i13000 std-f180-s33554397-i90000 crt-f180-s33554397-i16000 std-f256-s33554397-i90000 crt-f256-s33554397-i23500 std-f512-s33554397-i90000 crt-f512-s33554397-i96000 std-f768-s4800000-i640000 crt-f768-i280000

---

<div class="ui raised padded container segment">
 <p>Testing non-crt vs crt over a range of increasing shift values.</p>
  <a href="pandasvariancetest"></a>
  <div style="font-family: monospace; font-size:80%">
    <hr>
    <p>Pandas <a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.describe.html" target="_blank">“describe”</a> summary of variance</p>
    <pre><code class="nohighlight">               pps          tps         gps                        pps           tps         gps         glst         bpc
std-f768-s4800000-i640000                          crt-f768-i280000
mean   3658.262626  4254.853535  171.611111        mean   2.316789e+06  6.076554e+05  108.570707  3146.176768    1.155061
std     141.351963   128.315734    6.613728        std    1.199929e+05  3.454760e+05    2.233240  2282.882881    0.656220
min    3576.000000  4177.000000  168.000000        min    2.243369e+06  7.539000e+03  107.000000    46.000000    0.012000
25%    3592.250000  4193.250000  169.000000        25%    2.259828e+06  3.130220e+05  107.250000  1056.500000    0.591000
50%    3619.000000  4218.000000  170.000000        50%    2.266559e+06  6.096535e+05  108.000000  2787.500000    1.148500
75%    3656.500000  4251.000000  171.750000        75%    2.317839e+06  9.054402e+05  109.000000  4960.750000    1.715000
max    4783.000000  5329.000000  224.000000        max    3.302115e+06  1.201411e+06  127.000000  8185.000000    2.283000</code></pre>
  </div>
</div>


{% include paramtest.html %}

<div class="ui raised padded container segment">
  <p>Replication: 
  <pre style="font-size: 70%"><code class="bash">timeout 1000s gapminer -o localhost -p 31397 -u $USER -x $USERPASS -j 5 -e -f 64 -t 4
timeout 1000s gapminer -o localhost -p 31397 -u $USER -x $USERPASS -j 5 -e -f 64 -i 5200 -t 4 -d 3 -r crt/dist/crt-22m-0064s.txt</code></pre>
</p>
</div>
