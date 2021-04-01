---
layout: paramtest
title: Comparison of mining with shift/crt match / mismatch
description: shift mismatch <code>-t 4 -d 3 -f 448</code> for&#58; <code>-i 65000 -r crt-22m-0456s</code> and <code>-i 68000 -r crt-22m-0448s.txt</code>
author: Graham Higgins
testdir: shiftcrtest
tests: crt448-i65000-crt0448 crt448-i65000-crt0456
---


<div class="ui raised padded container segment">
 <p>It is possible to configure GapMiner to use a shift setting different from that of the crt file. The following results are reported from two tests (run in parallel on a single machine to factor out the impact of change in difficulty over time that otherwise causes sequentially-run tests to produce different results).</p>
    <p style="padding-left: 3em">i) a “match” <b><code>-t 4 -d 3 -f <span style="color:green">448</span> for -i 65000 -r crt-22m-0<span style="color:green">448</span>s</code></b></p>
    <p style="padding-left: 3em">ii) a “mismatch” <b><code>-t 4 -d 3 -f <span style="color:orange">448</span> for -i 65000 -r crt-22m-0<span style="color:orange">456</span>s</code></b></p>
  <a href="pandasvariancetest"></a>
  <div style="font-family: monospace; font-size:65%">
    <hr>
    <p>Pandas <a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.describe.html" target="_blank">“describe”</a> summary of variance</p>
    <pre><code class="nohighlight">                pps           tps         gps          glst         bpc                         pps           tps         gps          glst         bpc
crt448-i65000-crt0448                                                           crt448-i65000-crt0456
mean   3.132931e+06  2.209903e+06  408.582915  18920.286432    2.312985         mean   3.200170e+06  2.207076e+06  400.653266  17375.572864    2.345412
std    1.452072e+05  1.272493e+06   34.553164  12516.721861    1.358579         std    9.996107e+04  1.295141e+06    7.780796  11438.374173    1.383898
min    2.922151e+06  7.024800e+04  393.000000    536.000000    0.023000         min    2.261843e+06  1.462100e+04  378.000000    714.000000    0.007000
25%    3.063133e+06  1.060377e+06  401.000000   8251.500000    1.108000         25%    3.154603e+06  1.043149e+06  393.500000   7699.000000    1.129500
50%    3.141425e+06  2.281791e+06  404.000000  17582.000000    2.350000         50%    3.239446e+06  2.279580e+06  403.000000  16142.000000    2.364000
75%    3.184248e+06  3.299498e+06  408.000000  27831.500000    3.467000         75%    3.258402e+06  3.304436e+06  406.000000  25301.000000    3.507500
max    4.545159e+06  4.410068e+06  812.000000  50869.000000    4.686000         max    3.311071e+06  4.441743e+06  411.000000  47519.000000    4.787000</code></pre>
  </div>
</div>


{% include paramtest.html %}

<div class="ui raised padded container segment">
  <p>Replication: 
  <pre style="font-size: 80%"><code class="bash">gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -d 3 -f 448 -i 65000 -r crt/crt-22m-0448s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -d 3 -f 448 -i 65000 -r crt/crt-22m-0456s.txt</code></pre>
</p>
</div>
