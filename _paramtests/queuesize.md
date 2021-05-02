---
layout: paramtest 
title: Comparison of GPU miner performance at different queue size values ranging from 5 to 30
description: GPU queue size 5 - 30, repeated for comparison but affected by changes in difficulty
author: Graham Higgins
testdir: queuesize
tests: f64-t1-i3000000-s12000000-z5-n8-w512 f64-t1-i3000000-s12000000-z10-n8-w512 f64-t1-i3000000-s12000000-z20-n8-w512 f64-t1-i3000000-s12000000-z30-n8-w512
---

<div class="ui raised padded container segment">
  <p>Comparison tests of running GapMiner on the GPU at different queue size settings. The tabular data are the more communicative of the relative differences in performance.</p>
  <a href="pandasvariancetest"></a>
  <hr />
  <p style="font-size: 80%"><em>Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second, <code>gps</code> is average gaps per second, <code>glst</code> is the size of the gaplist and <code>l/s</code> is the time in seconds to scan the gaplist at the reported rate of gaps per second.</em></p>
  <div style="font-family: monospace; font-size:90%">
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-z5-n8-w512</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2722038</td><td align="right">2055509</td></tr>
                <tr><td align="left">max</td><td align="right">3120218</td><td align="right">2359843</td></tr>
                <tr><td align="left">min</td><td align="right">2672679</td><td align="right">2018498</td></tr>
                <tr><td align="left">std</td><td align="right">59997</td><td align="right">45482</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-z10-n8-w512</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2725573</td><td align="right">2057521</td></tr>
                <tr><td align="left">max</td><td align="right">3178352</td><td align="right">2392060</td></tr>
                <tr><td align="left">min</td><td align="right">2674148</td><td align="right">2018796</td></tr>
                <tr><td align="left">std</td><td align="right">74038</td><td align="right">55660</td></tr>
            </table>
        </div>
    </div>
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-z20-n8-w512</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2640409</td><td align="right">1994529</td></tr>
                <tr><td align="left">max</td><td align="right">2683620</td><td align="right">2027112</td></tr>
                <tr><td align="left">min</td><td align="right">2453759</td><td align="right">1844421</td></tr>
                <tr><td align="left">std</td><td align="right">33151</td><td align="right">25871</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-z30-n8-w512</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2687596</td><td align="right">2028362</td></tr>
                <tr><td align="left">max</td><td align="right">2741437</td><td align="right">2069912</td></tr>
                <tr><td align="left">min</td><td align="right">2587098</td><td align="right">1947674</td></tr>
                <tr><td align="left">std</td><td align="right">32710</td><td align="right">25326</td></tr>
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
  <pre style="font-size:78%"><code class="bash"></code></pre>
</p>
</div>
