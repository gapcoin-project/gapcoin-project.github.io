---
layout: paramtest
title: Comparison of mining with shift/crt match vs. mismatch
description: CRT mining with a shift setting different from that of the crt file vs mining with a shift setting that matches that of the crt file
author: Graham Higgins
testdir: shiftcrtest
tests: crt448-i97000-crt0448 crt448-i92000-crt0456
---

<div class="ui raised padded container segment">
  <p>With GapMiner, it is possible to configure CRT mining to use a shift setting different from that of the crt file. Excessive differences between shift and selected crt file are rejected by the miner. Otherwise, for a given shift, the lack of a precisely-matching CRT shift file presents no obstacle to using one with a closely-approximating shift, nor does it appear¹ to result in reduced performance as the tabulated results show a small degree of performance <em>improvement</em> for this particular test run.</p>
  <p style="font-size:80%;padding-left:0.6em">¹ <em>the neccessity of using different values for <code>-i</code> to control for gaplist size means that the results of these two tests cannot be directly compared</em></p>
  <p style="padding-left: 3em">i) a “match” <b><code>-t 4 -d 3 -f <span style="color:green">448</span> for -i 97000 -r crt-22m-0<span style="color:green">448</span>s</code></b></p>
  <p style="padding-left: 3em">ii) a “mismatch” <b><code>-t 4 -d 3 -f <span style="color:orange">448</span> for -i 92000 -r crt-22m-0<span style="color:orange">456</span>s</code></b></p>
  <hr />
  <p style="font-size: 80%"><em>Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second, <code>gps</code> is average gaps per second, <code>glst</code> is the size of the gaplist and <code>l/s</code> is the time in seconds to scan the gaplist at the reported rate of gaps per second.</em></p>
  <div style="font-family: monospace; font-size:90%">
    <div class="ui two column doubling stackable grid container">
      <div class="column">
          <p class="ui tiny header" style="margin:0;padding:0">crt448-i97000-crt0448</p>
          <table>
              <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
              <tr><td align="left">mean</td><td align="right">2338404</td><td align="right">2089219</td><td align="right">400</td><td align="right">2223</td><td align="right">1.12</td><td align="right">5.55</td></tr>
              <tr><td align="left">max</td><td align="right">2640848</td><td align="right">4147737</td><td align="right">427</td><td align="right">6538</td><td align="right">2.21</td><td align="right">15.31</td></tr>
              <tr><td align="left">min</td><td align="right">2117836</td><td align="right">16463</td><td align="right">386</td><td align="right">24</td><td align="right">0.01</td><td align="right">0.06</td></tr>
              <tr><td align="left">std</td><td align="right">50812</td><td align="right">1197611</td><td align="right">3</td><td align="right">1480</td><td align="right">0.64</td><td align="right">448.12</td></tr>
          </table>
      </div>
      <div class="column">
          <p class="ui tiny header" style="margin:0;padding:0">crt448-i92000-crt0456</p>
          <table>
              <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
              <tr><td align="left">mean</td><td align="right">2410050</td><td align="right">2084904</td><td align="right">399</td><td align="right">2558</td><td align="right">1.15</td><td align="right">6.41</td></tr>
              <tr><td align="left">max</td><td align="right">3892658</td><td align="right">4161044</td><td align="right">423</td><td align="right">7212</td><td align="right">2.30</td><td align="right">17.05</td></tr>
              <tr><td align="left">min</td><td align="right">2363818</td><td align="right">16986</td><td align="right">396</td><td align="right">5</td><td align="right">0.01</td><td align="right">0.01</td></tr>
              <tr><td align="left">std</td><td align="right">113999</td><td align="right">1202649</td><td align="right">4</td><td align="right">1867</td><td align="right">0.67</td><td align="right">481.53</td></tr>
          </table>
      </div>
    </div>
  </div>
  <hr>
  <p style="font-size: 80%; text-align:center"><em>The charts included below are for completeness. The figures given are the means and they differ from the means in the above table because, in order to support the different requirements of charting, the first 1/5th of the data is ignored in order to aid visual comparison. The chartline uses the full dataset.</em></p>
</div>


{% include paramtest.html %}

<div class="ui raised padded container segment">
  <p>Replication: 
  <pre style="font-size: 80%"><code class="bash">gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -d 3 -f 448 -i [as-discovered] -r crt/crt-22m-0448s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -d 3 -f 448 -i [as-discovered] -r crt/crt-22m-0456s.txt</code></pre>
</p>
</div>
