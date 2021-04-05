---
layout: paramtest 
title: Comparison of wizz’ merit 28 CRT files vs standard merit 22
description: Wizz has contributed a set of CRT files targeting merit 28
author: Graham Higgins
testdir: merit28
tests: f64-dist f64-wizz28
---

<div class="ui raised padded container segment">
  <p>Comparison tests of wizz’ contributed “merit 28” CRT files for shift 64, 160 versus the “merit 22” CRT files in the standard distribution.</p>

  <hr />
  <p style="font-size: 80%"><em>Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second, <code>gps</code> is average gaps per second, <code>glst</code> is the size of the gaplist and <code>l/s</code> is the time in seconds to scan the gaplist at the reported rate of gaps per second.</em></p>
  <div style="font-family: monospace; font-size:90%">
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-dist</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">518408</td><td align="right">4279241</td><td align="right">5421</td><td align="right">6283</td><td align="right">0.23</td><td align="right">1.16</td></tr>
                <tr><td align="left">max</td><td align="right">577741</td><td align="right">8382344</td><td align="right">7827</td><td align="right">21554</td><td align="right">0.45</td><td align="right">2.75</td></tr>
                <tr><td align="left">min</td><td align="right">256622</td><td align="right">69752</td><td align="right">5300</td><td align="right">0</td><td align="right">0.00</td><td align="right">0.00</td></tr>
                <tr><td align="left">std</td><td align="right">34494</td><td align="right">2409337</td><td align="right">240</td><td align="right">5197</td><td align="right">0.14</td><td align="right">21.66</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-wizz28</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">31279284</td><td align="right">4254828</td><td align="right">5419</td><td align="right">5878</td><td align="right">9.94</td><td align="right">1.08</td></tr>
                <tr><td align="left">max</td><td align="right">72042060</td><td align="right">8453167</td><td align="right">9318</td><td align="right">19295</td><td align="right">19.74</td><td align="right">2.07</td></tr>
                <tr><td align="left">min</td><td align="right">28624810</td><td align="right">71919</td><td align="right">5288</td><td align="right">0</td><td align="right">0.08</td><td align="right">0.00</td></tr>
                <tr><td align="left">std</td><td align="right">5514862</td><td align="right">2425777</td><td align="right">368</td><td align="right">5225</td><td align="right">5.56</td><td align="right">14.20</td></tr>
            </table>
        </div>
    </div>

  </div>
  <hr>
  <p style="font-sizegapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -f 512 -i [as-discovered] -r crt/dist/crt-22m-0512s.txt: 80%; text-align:center"><em>The charts included below are for completeness. The figures given are the means and they differ from the pandas-produced means because, in order to support the different requirements of charting, the first 1/5th of the data is ignored in order to aid visual comparison. The chartline uses the full dataset.</em></p>
</div>


{% include paramtest.html %}

<div class="ui raised padded container segment">
  <p>Replication: 
  <pre style="font-size:78%"><code class="bash">gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -f  416 -i [as-discovered] -r crt/dist/crt-22m-0416s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -f  416 -i [as-discovered] -r crt/wizz28/crt-28m-0416s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -f  512 -i [as-discovered] -r crt/dist/crt-22m-0512s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -f  512 -i [as-discovered] -r crt/wizz28/crt-28m-0512s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -f 1024 -i [as-discovered] -r crt/dist/crt-22m-1024s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -f 1024 -i [as-discovered] -r crt/wizz28/crt-28m-1024s.txt</</code></pre>
</p>
</div>
