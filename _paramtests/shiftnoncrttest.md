---
layout: paramtest
title: Performance of non-crt miner over a range of shift settings
description: shift test -s 33554432 -i 500000 -f 15, 24, 32, 48, 96, 128, 256, 512
author: Graham Higgins
testdir: shiftnoncrt
tests: shift-15 shift-24 shift-32 shift-48 shift-96 shift-128 shift-256 shift-512
---

<div class="ui raised padded container segment">
 <p>Illustration of at which point in the range of available shifts (from 16 - 1024) it is worth switching to mining with the Chinese Remainder Theorem.</p>
  <a href="pandasvariancetest"></a>
  <div style="font-family: monospace; font-size:90%">
    <hr>
    <p>Pandas <a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.describe.html" target="_blank">“describe”</a> summary of variance</p>
    <pre><code class="nohighlight">pps           tps           gps                 pps           tps           gps
shift-15                                                shift-24
mean   230655.959184  73107.183673  10976.244898        mean   205211.918367  67125.020408  9769.591837
std      4471.987799   1439.687346    212.754214        std      2114.705868    703.006505   100.553451
min    224150.000000  70969.000000  10666.000000        min    196788.000000  64256.000000  9368.000000
25%    226540.000000  71767.000000  10780.000000        25%    204790.000000  66985.000000  9749.000000
50%    231668.000000  73395.000000  11025.000000        50%    205372.000000  67202.000000  9777.000000
75%    234165.000000  74389.000000  11144.000000        75%    206551.000000  67547.000000  9834.000000
max    242883.000000  76353.000000  11553.000000        max    208184.000000  67892.000000  9908.000000

shift-32                                                shift-48
mean   200134.571429  67308.000000  9523.673469         mean   180466.918367  64229.020408  8585.163265
std      2009.424057    694.035032    96.133888         std      2460.678437    903.997384   117.240911
min    192972.000000  64784.000000  9184.000000         min    178585.000000  63639.000000  8496.000000
25%    199038.000000  66946.000000  9470.000000         25%    179197.000000  63758.000000  8524.000000
50%    200318.000000  67361.000000  9533.000000         50%    179579.000000  63900.000000  8543.000000
75%    201250.000000  67703.000000  9576.000000         75%    180546.000000  64254.000000  8589.000000
max    207149.000000  69556.000000  9859.000000         max    192490.000000  68491.000000  9157.000000

shift-96                                                shift-128
mean   109554.346939  45082.306122  5211.877551         mean   87985.795918  39713.918367  4187.448980
std      1326.475602    493.503808    62.789208         std     1814.951549    727.191081    86.582827
min    107061.000000  44153.000000  5094.000000         min    79323.000000  36038.000000  3774.000000
25%    108607.000000  44725.000000  5167.000000         25%    88108.000000  39812.000000  4193.000000
50%    110006.000000  45222.000000  5233.000000         50%    88532.000000  39936.000000  4213.000000
75%    110261.000000  45338.000000  5245.000000         75%    88826.000000  40008.000000  4227.000000
max    114111.000000  46436.000000  5427.000000         max    89326.000000  40179.000000  4251.000000

shift-256                                               shift-512
mean   34085.583333  20414.145833  1622.145833          mean   8020.086957  7230.521739  381.347826
std      409.175915    252.013592    19.410449          std      64.760697    71.411714    3.121377
min    33635.000000  20081.000000  1601.000000          min    7924.000000  7150.000000  377.000000
25%    33879.750000  20286.000000  1612.000000          25%    7973.000000  7176.000000  379.000000
50%    34038.000000  20370.000000  1620.000000          50%    7996.000000  7226.000000  380.000000
75%    34164.250000  20462.000000  1626.250000          75%    8073.000000  7253.500000  383.750000
max    35569.000000  21427.000000  1692.000000          max    8155.000000  7427.000000  388.000000 </code></pre>
  </div>
  <hr>
  <p style="font-size: 80%; text-align:center"><em>The charts included below are for completeness. The figures given are the means and they differ from the pandas-produced means because, in order to support the different requirements of charting, the first 1/5th of the data is ignored in order to aid visual comparison. The chartline uses the full dataset.</em></p>
</div>

{% include paramtest.html %}

<div class="ui raised padded container segment">
  <p>Replication: 
  <pre style="font-size: 80%"><code class="bash">gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -d 3 -f 448 -i 65000 -r crt/crt-22m-0448s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -d 3 -f 448 -i 65000 -r crt/crt-22m-0456s.txt</code></pre>
</p>
</div>
