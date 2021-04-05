---
layout: paramtest
title: Comparison of mining on shift64 22m vs wizz’ 28m
description: Test of shift64 22m vs 28m (n=199)
author: Graham Higgins
testdir: shift64merittest
tests: dist-22m-crt0064 wizz-28m-crt0064
---


<div class="ui raised padded container segment">
  <p>Testing wizz’ optimised 28m shift 64 crt (<code>-i 5750</code>) vs standard 22m (<code>-i 5500</code>)</p>
  <div style="font-family: monospace; font-size:90%">
    <hr>
    <p style="font-size: 80%"><em>Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second, <code>gps</code> is average gaps per second, <code>glst</code> is the size of the gaplist and <code>l/s</code> is the time in seconds to scan the gaplist at the reported rate of gaps per second.</em></p>
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">dist-22m-crt0064</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">763169</td><td align="right">4410157</td><td align="right">5328</td><td align="right">153464</td><td align="right">0.56</td><td align="right">28.80</td></tr>
                <tr><td align="left">max</td><td align="right">886978</td><td align="right">8920162</td><td align="right">8350</td><td align="right">407817</td><td align="right">1.12</td><td align="right">48.84</td></tr>
                <tr><td align="left">min</td><td align="right">503299</td><td align="right">61712</td><td align="right">5123</td><td align="right">6044</td><td align="right">0.00</td><td align="right">1.18</td></tr>
                <tr><td align="left">std</td><td align="right">32609</td><td align="right">2585037</td><td align="right">253</td><td align="right">106433</td><td align="right">0.32</td><td align="right">421.39</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">wizz-28m-crt0064</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">47749399</td><td align="right">4403190</td><td align="right">5622</td><td align="right">130792</td><td align="right">26.87</td><td align="right">23.26</td></tr>
                <tr><td align="left">max</td><td align="right">192825504</td><td align="right">8882274</td><td align="right">24518</td><td align="right">350037</td><td align="right">54.75</td><td align="right">14.28</td></tr>
                <tr><td align="left">min</td><td align="right">42880113</td><td align="right">186639</td><td align="right">5278</td><td align="right">3940</td><td align="right">0.20</td><td align="right">0.75</td></tr>
                <tr><td align="left">std</td><td align="right">11738410</td><td align="right">2563592</td><td align="right">1520</td><td align="right">89164</td><td align="right">15.83</td><td align="right">58.65</td></tr>
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
  <pre style="font-size: 75%"><code class="bash">gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -d 3 -f 64 -i [as-discovered] -r crt/crt-22m-0064s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -d 3 -f 64 -i [as-discovered] -r crt/crt-28m-0064s-wizz.txt</code></pre>
</p>
</div>
