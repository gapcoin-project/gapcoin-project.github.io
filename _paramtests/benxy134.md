---
layout: paramtest
title: Performance test of benxy031’s optimisation of crt-22m-0134
description: benxy - f 134 -t 4 -d 3 -i 12000 -r crt-22m-0134s
author: Graham Higgins
testdir: benxy-0134
tests: dist-i12000-crt0134 benxy-i12000-crt0134
---

<div class="ui raised padded container segment">
  <p>Comparison of benxy031’s optimisation of wizz’s contribution of crt-22m-0134 (n=199). Of note is the value for <code>std</code> (<a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.std.html#pandas.DataFrame.std" target="_blank">standard deviation</a>). Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second, <code>gps</code> is average gaps per second and <code>glst</code> is the size of the gaplist</p>
  <a href="pandasvariancetest"></a>
  <div style="font-family: monospace; font-size:75%">
    <hr>
    <p>Pandas <a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.describe.html" target="_blank">“describe”</a> summary of variance</p>
    <pre><code class="nohighlight">dist-i12000-crt0134                                                 benxy-i12000-crt0134
                 pps           tps          gps          glst                       pps           tps          gps          glst
mean   239124.477387  2.208095e+07  5424.628141   5553.532663       mean   1.784617e+06  2.359628e+07  5538.587940   5222.371859
std     19955.860671  1.250876e+07   172.675302   3820.548992       std    1.003734e+05  1.387071e+07   110.884056   4195.555153
min    223250.000000  2.898650e+05  5290.000000     38.000000       min    1.638624e+06  2.746600e+05  5473.000000      7.000000
25%    231680.000000  1.162665e+07  5313.000000   2344.000000       25%    1.752550e+06  1.167034e+07  5493.000000   1731.500000
50%    233546.000000  2.172128e+07  5348.000000   5119.000000       50%    1.766285e+06  2.319926e+07  5518.000000   3928.000000
75%    235077.500000  3.281469e+07  5471.000000   8871.000000       75%    1.804863e+06  3.549138e+07  5561.500000   8249.000000
max    346912.000000  4.417791e+07  6079.000000  15185.000000       max    2.813653e+06  4.792775e+07  6853.000000  14903.000000</code></pre>
  </div>
  <hr>
  <p style="font-size: 80%; text-align:center"><em>The charts included below are for completeness. The figures given are the means and they differ from the pandas-produced means because, in order to support the different requirements of charting, the first 1/5th of the data is ignored in order to aid visual comparison. The chartline uses the full dataset.</em></p>
</div>

{% include paramtest.html %}

<div class="ui raised padded container segment">
  <p>Replication: 
  <pre style="font-size:85%"><code class="bash">gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -d 3 -f 134 -i 12000 -r crt/dist/crt-22m-0134s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -d 3 -f 134 -i 12000 -r crt/benxy-031/crt-22m-0134s.txt</code></pre>
</p>
</div>
