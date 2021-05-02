---
layout: paramtest
title: Comparison of GPU miner performance at different number of tests values ranging from 4 to 16
description: GPU queue size 4 - 16, repeated for comparison but affected by changes in difficulty
author: Graham Higgins
testdir: numtests
tests: f64-t1-i3000000-s12000000-z10-n4-w512 f64-t1-i3000000-s12000000-z10-n8-w512 f64-t1-i3000000-s12000000-z10-n12-w512 f64-t1-i3000000-s12000000-z10-n16-w512
---

<div class="ui raised padded container segment">
  <p>Comparison tests of running GapMiner on the GPU at different number of tests settings. The tabular data are the more communicative of the relative differences in performance.</p>
  <a href="pandasvariancetest"></a>
  <hr />
  <p style="font-size: 80%"><em>Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second, <code>gps</code> is average gaps per second, <code>glst</code> is the size of the gaplist and <code>l/s</code> is the time in seconds to scan the gaplist at the reported rate of gaps per second.</em></p>
  <div style="font-family: monospace; font-size:90%">
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-z10-n4-w512</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2823068</td><td align="right">1859941</td></tr>
                <tr><td align="left">max</td><td align="right">3193418</td><td align="right">2098287</td></tr>
                <tr><td align="left">min</td><td align="right">2776667</td><td align="right">1829004</td></tr>
                <tr><td align="left">std</td><td align="right">72415</td><td align="right">45144</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-z10-n8-w512</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2747037</td><td align="right">2085597</td></tr>
                <tr><td align="left">max</td><td align="right">2924113</td><td align="right">2208669</td></tr>
                <tr><td align="left">min</td><td align="right">2700217</td><td align="right">2050416</td></tr>
                <tr><td align="left">std</td><td align="right">44200</td><td align="right">33390</td></tr>
            </table>
        </div>
    </div>
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-z10-n12-w512</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2753522</td><td align="right">2348660</td></tr>
                <tr><td align="left">max</td><td align="right">2816817</td><td align="right">2407540</td></tr>
                <tr><td align="left">min</td><td align="right">2691229</td><td align="right">2294810</td></tr>
                <tr><td align="left">std</td><td align="right">31908</td><td align="right">28011</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-z10-n16-w512</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2667851</td><td align="right">2553380</td></tr>
                <tr><td align="left">max</td><td align="right">2778569</td><td align="right">2659649</td></tr>
                <tr><td align="left">min</td><td align="right">2629469</td><td align="right">2516231</td></tr>
                <tr><td align="left">std</td><td align="right">21842</td><td align="right">20919</td></tr>
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
