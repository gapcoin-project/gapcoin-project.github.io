---
layout: paramtest
title: Comparison of mining with shift/crt match / mismatch
description: shift mismatch <code>-t 4 -d 3 -f 448</code> for&#58; <code>-i 65000 -r crt-22m-0456s</code> and <code>-i 68000 -r crt-22m-0448s.txt</code>
author: Graham Higgins
testdir: shiftcrtest
tests: crtshiftmatch-f-448-crt-0456s crtshiftmatch-f-448-crt-0448s
---


<div class="ui raised padded container segment">
 <p>It is possible to configure GapMiner to use a shift setting different from that of the crt file. The following results are reported from two tests:</p>
    <p style="padding-left: 3em">i) a “mismatch” <b><code>-t 4 -d 3 -f <span style="color:orange">448</span> for -i 65000 -r crt-22m-0<span style="color:orange">456</span>s</code></b></p>
    <p style="padding-left: 3em">ii) a “match” <b><code>-t 4 -d 3 -f <span style="color:green">448</span> for -i 65000 -r crt-22m-0<span style="color:green">448</span>s</code></b></p>
  <a href="pandasvariancetest"></a>
  <div style="font-family: monospace; font-size:90%">
    <hr>
    <p>Pandas <a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.describe.html" target="_blank">“describe”</a> summary of variance</p>
    <pre class="nohighlight">
     -f-448-crt-0456s n=999                              -f-448-crt-0448s n=999 
                     pps           tps          gps                      pps           tps          gps
     mean   5.437276e+06  1.979902e+07   855.859860      mean   5.213781e+06  2.256405e+07   920.358358 
     std    5.121476e+04  1.155445e+07     7.240389      std    1.668741e+05  1.278303e+07    12.998755 
     min    5.282791e+06  2.290900e+04   840.000000      min    5.081718e+06  2.800400e+04   908.000000 
     max    6.150059e+06  4.008869e+07   953.000000      max    8.721902e+06  4.449811e+07  1145.000000</pre>
  </div>
</div>


{% include paramtest.html %}

<div class="ui raised padded container segment">
  <p>Replication: 
  <pre style="font-size: 80%"><code class="bash">gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -d 3 -f 448 -i 65000 -r crt/crt-22m-0448s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -d 3 -f 448 -i 65000 -r crt/crt-22m-0456s.txt</code></pre>
</p>
</div>
