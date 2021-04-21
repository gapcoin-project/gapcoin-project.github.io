---
layout: paramtest
title: Comparison of changing --sieve-size (ineffective at shifts &lt; 768 in non-CRT mining)
description: <code>--sieve-size</code> is described as a tertiary parameter with little influence on miner performance.
author: Graham Higgins
testdir: sievesize
tests: f64-s13554397-i90000 f64-s33554397-i90000 f64-s53554397-i90000 f128-s13554397-i900000 f128-s33554397-i900000 f128-s53554397-i900000 std-f768-s33554397-i90000 std-f768-s4800000-i640000
---

<div class="ui raised padded container segment">
  <p>In a post to the bitcointalk thread, j0nn9 <a href="https://bitcointalk.org/index.php?topic=822498.msg9295189#msg9295189" target="_blank">describes the GapMiner parameters</a>: “shift should be the most sensitive parameter, because it controls the bit size of the primes, second would be sieve primes” and makes no mention of the <code>--sieve-size</code> parameter, implying that it has little influence on miner performance (it plays no role at all in CRT mining.</p> 
  <p>Confirming that changing <code>--sieve-size</code> has no <strong>statistically-significant</strong> (less than the standard deviation values in the tabular data shown below) effect at shift 64 or 128 (nor at any shift up to 512, although those results are not reported here).</p>
  <p style="margin-left:0.6em"><em>At shift 768 however, some improvement was detected when the value was <em>reduced</em> from the default (with <code>--sieve-primes</code> also adjusted away from the default).</em></p>
  <div style="font-family: monospace; font-size:90%">
    <hr>
    <p style="font-size: 80%"><em>Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second, <code>gps</code> is average gaps per second, <code>glst</code> is the size of the gaplist and <code>l/s</code> is the time in seconds to scan the gaplist at the reported rate of gaps per second.</em></p>
    <div class="ui three column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-s13554397-i90000</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">137300</td><td align="right">49101</td><td align="right">6487</td></tr>
                <tr><td align="left">max</td><td align="right">149758</td><td align="right">53266</td><td align="right">7073</td></tr>
                <tr><td align="left">min</td><td align="right">136019</td><td align="right">48650</td><td align="right">6429</td></tr>
                <tr><td align="left">std</td><td align="right">1848</td><td align="right">658</td><td align="right">87</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-s33554397-i90000</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">140185</td><td align="right">50124</td><td align="right">6625</td></tr>
                <tr><td align="left">max</td><td align="right">149329</td><td align="right">53690</td><td align="right">7058</td></tr>
                <tr><td align="left">min</td><td align="right">132452</td><td align="right">47419</td><td align="right">6258</td></tr>
                <tr><td align="left">std</td><td align="right">1722</td><td align="right">634</td><td align="right">81</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-s53554397-i90000</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">140172</td><td align="right">50141</td><td align="right">6624</td></tr>
                <tr><td align="left">max</td><td align="right">149196</td><td align="right">53336</td><td align="right">7049</td></tr>
                <tr><td align="left">min</td><td align="right">102433</td><td align="right">36744</td><td align="right">4841</td></tr>
                <tr><td align="left">std</td><td align="right">3759</td><td align="right">1325</td><td align="right">177</td></tr>
            </table>
        </div>
    </div>
    <div class="ui three column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f128-s13554397-i900000</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">81951</td><td align="right">35266</td><td align="right">3882</td></tr>
                <tr><td align="left">max</td><td align="right">97703</td><td align="right">41775</td><td align="right">4625</td></tr>
                <tr><td align="left">min</td><td align="right">80613</td><td align="right">34677</td><td align="right">3819</td></tr>
                <tr><td align="left">std</td><td align="right">1997</td><td align="right">853</td><td align="right">94</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f128-s33554397-i900000</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">82462</td><td align="right">35428</td><td align="right">3906</td></tr>
                <tr><td align="left">max</td><td align="right">87976</td><td align="right">37700</td><td align="right">4166</td></tr>
                <tr><td align="left">min</td><td align="right">58547</td><td align="right">25124</td><td align="right">2772</td></tr>
                <tr><td align="left">std</td><td align="right">2077</td><td align="right">887</td><td align="right">98</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f128-s53554397-i900000</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">82198</td><td align="right">35353</td><td align="right">3894</td></tr>
                <tr><td align="left">max</td><td align="right">86873</td><td align="right">37363</td><td align="right">4114</td></tr>
                <tr><td align="left">min</td><td align="right">81002</td><td align="right">34866</td><td align="right">3839</td></tr>
                <tr><td align="left">std</td><td align="right">1176</td><td align="right">491</td><td align="right">55</td></tr>
            </table>
        </div>
    </div>
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">std-f768-s33554397-i90000</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">3012</td><td align="right">4051</td><td align="right">142</td></tr>
                <tr><td align="left">max</td><td align="right">3299</td><td align="right">4427</td><td align="right">155</td></tr>
                <tr><td align="left">min</td><td align="right">0</td><td align="right">0</td><td align="right">0</td></tr>
                <tr><td align="left">std</td><td align="right">731</td><td align="right">983</td><td align="right">34</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">std-f768-s4800000-i640000</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">3605</td><td align="right">4234</td><td align="right">169</td></tr>
                <tr><td align="left">max</td><td align="right">3854</td><td align="right">4595</td><td align="right">181</td></tr>
                <tr><td align="left">min</td><td align="right">0</td><td align="right">0</td><td align="right">0</td></tr>
                <tr><td align="left">std</td><td align="right">259</td><td align="right">306</td><td align="right">12</td></tr>
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
  <pre style="font-size: 80%"><code class="bash">gapminer -o localhost -p 31397 -u $USER -x $USERPASS -j 5 -e -f  64 -s 13554397 -i [as-discovered] -t 3
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -j 5 -e -f  64 -s 33554397 -i [as-discovered] -t 3
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -j 5 -e -f  64 -s 53554397 -i [as-discovered] -t 3
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -j 5 -e -f 128 -s 13554397 -i [as-discovered] -t 4
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -j 5 -e -f 128 -s 33554397 -i [as-discovered] -t 3
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -j 5 -e -f 128 -s 53554397 -i [as-discovered] -t 3
</code></pre>
</p>
</div>
