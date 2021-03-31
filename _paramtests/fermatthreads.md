---
layout: paramtest
title: Performance test of varying the number of fermat threads over the range 4,5,6,7 for crt 512
description: crt fermat threads test -i 13000 -f 512 -t 8 -d 4 5 6 7
author: Graham Higgins
testdir: fermatthreads
tests: d4-i13000-crt0512 d4-i350000-crt0512 d5-i13000-crt0512 d5-i225000-crt0512 d6-i120000-crt0512 d6-i13000-crt0512 d7-i13000-crt0512 d7-i50000-crt0512
---

<div class="ui raised padded container segment">
  <p>Comparison between reported performance of GapMiner on crt mining at a shift of 512 with a varying number of threads devoted to Fermat tests, one run with <code>--sieve-primes</code> at 13000 and a comparison run with a “tuned” value. Of note is the value for <code>std</code> (<a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.std.html#pandas.DataFrame.std" target="_blank">standard deviation</a>). Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second, <code>gps</code> is average gaps per second and <code>glst</code> is the size of the gaplist</p>
  <a href="pandasvariancetest"></a>
  <div style="font-family: monospace; font-size:80%">
    <hr>
    <p>Pandas <a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.describe.html" target="_blank">“describe”</a> summary of variance</p>
    <pre><code class="nohighlight">                pps           tps         gps          glst                      pps           tps         gps          glst
d4-i13000-crt0512                                                d4-i350000-crt0512
mean   6.031856e+06  1.448187e+06  298.819095  8.510254e+05      mean   3.057558e+06  1.837046e+06  382.242424   3606.646465
std    1.065509e+05  8.211101e+05    7.462190  6.045115e+05      std    1.501358e+05  1.046409e+06    3.717406   2629.271364
min    5.947158e+06  1.340400e+04  294.000000  6.130000e+02      min    2.914587e+06  1.788800e+04  379.000000     25.000000
25%    5.966202e+06  7.434630e+05  295.000000  3.160240e+05      25%    3.015135e+06  9.452472e+05  380.000000   1466.500000
50%    5.998845e+06  1.450392e+06  296.000000  7.580890e+05      50%    3.041001e+06  1.833868e+06  381.000000   3131.500000
75%    6.078542e+06  2.158178e+06  300.000000  1.336200e+06      75%    3.076756e+06  2.733174e+06  384.000000   5229.500000
max    6.865716e+06  2.851303e+06  360.000000  2.127753e+06      max    4.579058e+06  3.632550e+06  407.000000  10421.000000

d5-i13000-crt0512                                                d5-i225000-crt0512
mean   6.797970e+06  1.760570e+06  366.407035  4.706450e+05      mean   3.548916e+06  2.217387e+06  459.454545  3595.297980
std    5.349916e+04  1.012455e+06    4.124349  3.448049e+05      std    8.642101e+04  1.274938e+06    1.462025  2347.567964
min    6.206343e+06  1.323200e+04  364.000000  2.406000e+03      min    3.494682e+06  2.493200e+04  451.000000    13.000000
25%    6.780680e+06  8.961860e+05  364.000000  1.910150e+05      25%    3.507500e+06  1.124702e+06  459.250000  1672.250000
50%    6.789582e+06  1.751986e+06  365.000000  4.076490e+05      50%    3.526783e+06  2.211920e+06  460.000000  3224.000000
75%    6.815648e+06  2.626211e+06  368.000000  6.667945e+05      75%    3.542514e+06  3.319665e+06  460.000000  5198.250000
max    6.935222e+06  3.502203e+06  386.000000  1.543914e+06      max    4.129409e+06  4.407644e+06  463.000000  9932.000000

d6-i13000-crt0512                                                d6-i120000-crt0512
mean   7.184311e+06  2.184909e+06  445.055276  4.624968e+05      mean   4.271916e+06  2.564469e+06  527.673367   6289.718593
std    1.490760e+05  1.258527e+06    8.012740  2.985611e+05      std    7.266516e+04  1.491498e+06   13.722313   4709.134938
min    5.572082e+06  8.998000e+03  343.000000  6.000000e+00      min    3.981451e+06  8.474000e+03  337.000000    185.000000
25%    7.186678e+06  1.104506e+06  445.000000  1.931295e+05      25%    4.234959e+06  1.276376e+06  528.000000   2341.000000
50%    7.198386e+06  2.187909e+06  446.000000  4.502600e+05      50%    4.268224e+06  2.549342e+06  529.000000   5449.000000
75%    7.212098e+06  3.269956e+06  447.000000  7.207380e+05      75%    4.285614e+06  3.853434e+06  530.000000   9225.500000
max    7.279910e+06  4.341163e+06  448.000000  1.000536e+06      max    4.884404e+06  5.125720e+06  531.000000  17468.000000

d7-i13000-crt0512                                                d7-i50000-crt0512
mean   6.725950e+06  2.533952e+06  514.050251  183165.683417     mean   4.697977e+06  2.860719e+06  583.145729  12532.447236
std    2.121562e+05  1.477188e+06   14.850687  127560.090957     std    1.304306e+05  1.656511e+06    8.002138   8268.367933
min    4.577901e+06  3.818000e+03  390.000000      78.000000     min    2.935204e+06  5.345000e+03  482.000000     36.000000
25%    6.728317e+06  1.270877e+06  517.000000   75530.500000     25%    4.685234e+06  1.436462e+06  584.000000   5030.000000
50%    6.770254e+06  2.522844e+06  518.000000  157214.000000     50%    4.711990e+06  2.869109e+06  584.000000  11912.000000
75%    6.790262e+06  3.801984e+06  518.000000  284127.500000     75%    4.733404e+06  4.286908e+06  585.000000  19283.500000
max    6.812491e+06  5.090242e+06  520.000000  446135.000000     max    4.824237e+06  5.691272e+06  586.000000  29685.000000</code></pre>
  </div>
  <hr>
  <p style="font-size: 80%; text-align:center"><em>The charts included below are for completeness. The figures given are the means and they differ from the pandas-produced means because, in order to support the different requirements of charting, the first 1/5th of the data is ignored in order to aid visual comparison. The chartline uses the full dataset.</em></p>
</div>

{% include paramtest.html %}

<div class="ui raised padded container segment">
  <p>Replication: 
  <pre style="font-size:85%"><code class="bash">gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 8 -d4 -f 64 -i 350000 -r crt/crt-22m-0512s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 8 -d5 -f 64 -i 225000 -r crt/crt-22m-0512s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 8 -d6 -f 64 -i 120000 -r crt/crt-22m-0512s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 8 -d7 -f 64 -i 50000 -r crt/crt-22m-0512s.txt</code></pre>
</p>
</div>
