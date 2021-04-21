---
layout: paramtest 
title: Comparison of -s 1533554432 -i 4090000 vs standard -s 33554432 -i 900000 
description: Extreme settings hard-coded as default in other reference client implementations
author: Graham Higgins
testdir: defaultvsextremes
tests: f64-t4-i40900000-s1533554432 f64-t4-i900000-s33554432
---

<div class="ui raised padded container segment">
  <p>Comparison tests of shift 64 at extreme default settings of <code>-s 1533554432</code> <code>-i 4090000</code> with shift 64 at standard default settings of <code>-s 33554432</code> <code>-i 900000</code>.</p>
  <hr />
  <p style="font-size: 80%"><em>Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second, <code>gps</code> is average gaps per second.</em></p>
  <div style="font-family: monospace; font-size:90%">
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t4-i40900000-s1533554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">306036</td><td align="right">87062</td><td align="right">14359</td></tr>
                <tr><td align="left">max</td><td align="right">318818</td><td align="right">90751</td><td align="right">14959</td></tr>
                <tr><td align="left">min</td><td align="right">75368</td><td align="right">21459</td><td align="right">3536</td></tr>
                <tr><td align="left">std</td><td align="right">23125</td><td align="right">6586</td><td align="right">1086</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t4-i900000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">324394</td><td align="right">115101</td><td align="right">15220</td></tr>
                <tr><td align="left">max</td><td align="right">529462</td><td align="right">186719</td><td align="right">24831</td></tr>
                <tr><td align="left">min</td><td align="right">314905</td><td align="right">111784</td><td align="right">14777</td></tr>
                <tr><td align="left">std</td><td align="right">28409</td><td align="right">10003</td><td align="right">1332</td></tr>
            </table>
        </div>
    </div>
  </div>
  <hr>
  <p style="font-size: 80%; text-align:center"><em>The charts included below are for completeness. The figures given are the means and they differ from the pandas-produced means because, in order to support the different requirements of charting, the first 1/5th of the data is ignored in order to aid visual comparison. The chartline uses the full dataset.</em></p>
</div>


{% include paramtest.html %}

<div class="ui raised padded container segment">
  <p>Replication: 
  <pre style="font-size:78%"><code class="bash">gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -f 64 -s 1533554432 -i 4090000
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -f 64 -s 33554432 -i 900000</code></pre>
</p>
</div>
