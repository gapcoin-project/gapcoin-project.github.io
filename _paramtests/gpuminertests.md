---
layout: paramtest
title: Comparison of GPU miner performance at different settings
description: GPU tests, affected by changes in difficulty
author: Graham Higgins
testdir: gpuminertests
tests: f16-z16-n12-w2048 f32-z16-n12-w2048
---

<div class="ui raised padded container segment">
  <p>Comparison tests of running GapMiner on the GPU at different test settings. The tabular data are the more communicative of the relative differences in performance.</p>
  <a href="pandasvariancetest"></a>
  <hr />
  <p style="font-size: 80%"><em>Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second, <code>gps</code> is average gaps per second, <code>glst</code> is the size of the gaplist and <code>l/s</code> is the time in seconds to scan the gaplist at the reported rate of gaps per second.</em></p>
  <div style="font-family: monospace; font-size:90%">
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f16-z16-n12-w2048</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2427039</td><td align="right">2410963</td></tr>
                <tr><td align="left">max</td><td align="right">2551903</td><td align="right">5906010</td></tr>
                <tr><td align="left">min</td><td align="right">1312315</td><td align="right">2158945</td></tr>
                <tr><td align="left">std</td><td align="right">207619</td><td align="right">609766</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f32-z16-n12-w2048</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2693187</td><td align="right">2233665</td></tr>
                <tr><td align="left">max</td><td align="right">3122843</td><td align="right">2601372</td></tr>
                <tr><td align="left">min</td><td align="right">2660307</td><td align="right">2208998</td></tr>
                <tr><td align="left">std</td><td align="right">62222</td><td align="right">50107</td></tr>
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
