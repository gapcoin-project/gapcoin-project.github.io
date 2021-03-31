---
layout: paramtest
title: Default vs pdazzl’s -i and -s variants at shifts 21, 22, 23, 24, 26 and 27
description: pdazzl variants -f 21 -s 2097152 -i 56474, -f 22 -s 4194304 -i 106974, -f 23 -s 8388608 -i 203094, -f 24 -s 16777216 -i 386702, -f 26 -s 67108864 -i 1410973, -f 27 -s 134217728 -i 2703387
author: Graham Higgins
testdir: pdazzlvariant
tests: default-21-33554432-900000 pdazzlvariant-21-2097152-56474 default-22-33554432-900000 pdazzlvariant-22-4194304-106974 default-23-33554432-900000 pdazzlvariant-23-8388608-203094 default-24-33554432-900000 pdazzlvariant-24-6777216-386702 default-26-33554432-900000 pdazzlvariant-26-67108864-1410973 default-27-33554432-900000 pdazzlvariant-27-134217728-2703387 
---

<div class="ui vertical segment">
  <div class="ui centered page grid">
    <div class="row">
      <div class="column">
        <h2 class="ui teal header">Performance of default miner settings vs pdazzl’s suggested variants.</h2>
        <p>Tests of the default sieve-size (33554432) and sieve-primes (900000) values versus (i.e. immediately followed by) pdazzl’s proposed parameter variants of sieve-size and sieve-primes over the given range of shifts.</p>
      </div>
    </div> <!-- /row -->
  </div>
</div>

<div class="ui raised padded container segment">
  <a href="pandasvariancetest"></a>
  <div style="font-family: monospace; font-size:48%">
    <hr>
    <p>Pandas <a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.describe.html" target="_blank">“describe”</a> summary of variance</p>
    <pre class="nohighlight">
default-21-33554432-900000                           pdazzlvariant-21-2097152-56474                      default-22-33554432-900000                           pdazzlvariant-22-4194304-106974
                 pps           tps           gps                      pps           tps           gps                     pps           tps           gps                      pps           tps           gps
mean   223197.200803  69678.429719  10643.638554     mean   222900.477912  69560.538153  10626.148594    mean   225900.622490  70690.445783  10761.903614     mean   225983.453815  70714.289157  10757.903614
std      2040.689415    593.217597     97.051314     std       811.720813    261.425588     38.672712    std      1897.323202    574.487287     93.137942     std      1145.551849    349.734641     54.579761
min    221148.000000  69010.000000  10546.000000     min    220787.000000  68917.000000  10526.000000    min    223809.000000  70026.000000  10659.000000     min    223734.000000  70087.000000  10651.000000
max    236536.000000  73499.000000  11279.000000     max    228129.000000  71347.000000  10877.000000    max    235089.000000  72705.000000  11199.000000     max    234992.000000  73162.000000  11184.000000

default-23-33554432-900000                           pdazzlvariant-23-8388608-203094                     default-24-33554432-900000                           pdazzlvariant-24-6777216-386702
                 pps           tps           gps                      pps           tps           gps                     pps           tps           gps                      pps           tps           gps
mean   226166.381526  71047.144578  10767.064257     mean   220684.738956  69323.506024  10512.871486    mean   218568.823293  68809.967871  10399.140562     mean   221770.160643  69773.309237  10544.084337
std      3208.058791   1012.423591    152.926756     std      2907.561528    941.060804    138.764797    std      1055.217063    311.793742     50.936713     std       935.729381    312.543656     43.844172
min    185094.000000  58140.000000   8811.000000     min    218201.000000  68531.000000  10394.000000    min    217221.000000  68404.000000  10334.000000     min    216421.000000  67787.000000  10292.000000
max    227902.000000  71570.000000  10849.000000     max    229777.000000  72447.000000  10947.000000    max    222792.000000  69640.000000  10598.000000     max    223786.000000  70189.000000  10639.000000

default-26-33554432-900000                           pdazzlvariant-26-67108864-1410973                   default-27-33554432-900000                           pdazzlvariant-27-134217728-2703387
                 pps           tps           gps                      pps           tps           gps                     pps           tps           gps                      pps           tps           gps
mean   221770.160643  69773.309237  10544.084337     mean   214460.510040  67925.088353  10186.401606    mean   217476.128514  69164.939759  10331.955823     mean   213252.493976  67752.799197  10129.746988
std       935.729381    312.543656     43.844172     std      1465.206798    429.524841     68.823402    std      1892.153541    615.261268     88.888761     std      2661.540641    878.696312    126.602710
min    216421.000000  67787.000000  10292.000000     min    203954.000000  64648.000000   9689.000000    min    214577.000000  68227.000000  10195.000000     min    178101.000000  56428.000000   8460.000000
max    223786.000000  70189.000000  10639.000000     max    216356.000000  68467.000000  10275.000000    max    221878.000000  70487.000000  10538.000000     max    214523.000000  68204.000000  10191.000000
    </pre>
  </div>
  <hr>
  <p style="font-size: 80%; text-align:center"><em>The charts included below are for completeness. The figures given are the means and they differ from the pandas-produced means because, in order to support the different requirements of charting, the first 1/5th of the data is ignored in order to aid visual comparison. The chartline uses the full dataset.</em></p>
</div>

{% include paramtest.html %}

<div class="ui raised padded container segment">
  <p>Replication: 
  <pre><code class="bash"># shift 21
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 1 -f 21
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 1 -f 21 -s 2097152 -i 56474
# shift 22
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 1 -f 22
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 1 -f 22 -s 4194304 -i 106974
# shift 23
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 1 -f 23
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 1 -f 23 -s 8388608 -i 203094
# shift 24
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 1 -f 24
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 1 -f 24 -s 16777216 -i 386702
# shift 26
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 1 -f 26
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 1 -f 26 -s 67108864 -i 1410973
# shift 27
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 1 -f 27
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 1 -f 27 -s 134217728 -i 2703387</code></pre>
</p>
</div>


