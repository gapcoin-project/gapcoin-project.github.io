---
layout: paramtest
title: Comparison of changing --sieve-primes over increasing shift 48 - 256
description: <code>--sieve-primes</code> influence on miner performance at different shifts.
author: Graham Higgins
testdir: sieveprimesovershift
tests: f48-t3-i90000-s33554432 f48-t3-i900000-s33554432 f48-t3-i1900000-s33554432 f96-t3-i90000-s33554432 f96-t3-i900000-s33554432 f96-t3-i1900000-s33554432 f128-t3-i90000-s33554432 f128-t3-i900000-s33554432 f128-t3-i1900000-s33554432 f256-t3-i90000-s33554432 f256-t3-i900000-s33554432 f256-t3-i1900000-s33554432 f256-t3-i2000000-s33554432 f256-t3-i4000000-s33554432 f256-t3-i6000000-s33554432 f256-t3-i8000000-s33554432 f256-t3-i10000000-s33554432 f256-t3-i12000000-s33554432
---

<div class="ui raised padded container segment">
  <p>In a post to the bitcointalk thread, j0nn9 <a href="https://bitcointalk.org/index.php?topic=822498.msg9295189#msg9295189" target="_blank">describes the GapMiner parameters</a>: “shift should be the most sensitive parameter, because it controls the bit size of the primes, second would be sieve primes”. The tests reported here are of systematic changes to the value of <code>sieve-primes</code> in <strong><em>non-CRT</em></strong> mining.</p> 
  <p>Each row of three tests is a single, simultaneous run and can be compared laterally - but not vertically because for each run of three tests, the difficulty changes and thwarts comparison. Of note is the <code>std</code> value, the standard deviation</p>
  <p>Unlike <a href="/paramtests/sieveprimes/">mining at shift 25</a>, it seems that at shift 48, increasing the number of primes in the sieve above the default 900000 starts to make a small positive difference, if one can see past the noise. So, it’s worth bumping up the <code>sieve-primes</code> value for non-CRT mining at higher shifts.</p>
  <p>The final three tests check for any ceiling effect in sieve-primes settings that might be affecting the results, pushing the boundaries out to 20000000, in the interests of completeness and it appears that for the upper range of shifts with non-CRT mining, around 8000000 is optimal.</p>
  <div style="font-family: monospace; font-size:90%">
    <hr>
    <p style="font-size: 80%"><em>Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second, <code>gps</code> is average gaps per second.</em></p>
    <div class="ui three column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f48-t3-i90000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">223907</td><td align="right">89206</td><td align="right">10544</td></tr>
                <tr><td align="left">max</td><td align="right">252493</td><td align="right">101087</td><td align="right">11890</td></tr>
                <tr><td align="left">min</td><td align="right">217716</td><td align="right">86744</td><td align="right">10254</td></tr>
                <tr><td align="left">std</td><td align="right">5387</td><td align="right">2172</td><td align="right">253</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f48-t3-i900000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">254707</td><td align="right">86225</td><td align="right">11995</td></tr>
                <tr><td align="left">max</td><td align="right">285089</td><td align="right">96367</td><td align="right">13420</td></tr>
                <tr><td align="left">min</td><td align="right">248336</td><td align="right">84071</td><td align="right">11696</td></tr>
                <tr><td align="left">std</td><td align="right">5626</td><td align="right">1873</td><td align="right">263</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f48-t3-i1900000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">255478</td><td align="right">82424</td><td align="right">12031</td></tr>
                <tr><td align="left">max</td><td align="right">284765</td><td align="right">91977</td><td align="right">13403</td></tr>
                <tr><td align="left">min</td><td align="right">248594</td><td align="right">80221</td><td align="right">11708</td></tr>
                <tr><td align="left">std</td><td align="right">6137</td><td align="right">1976</td><td align="right">287</td></tr>
            </table>
        </div>
    </div>
    <div class="ui three column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f96-t3-i90000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">128288</td><td align="right">59190</td><td align="right">6040</td></tr>
                <tr><td align="left">max</td><td align="right">153577</td><td align="right">71176</td><td align="right">7230</td></tr>
                <tr><td align="left">min</td><td align="right">123775</td><td align="right">57078</td><td align="right">5828</td></tr>
                <tr><td align="left">std</td><td align="right">4753</td><td align="right">2236</td><td align="right">224</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f96-t3-i900000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">146080</td><td align="right">57240</td><td align="right">6878</td></tr>
                <tr><td align="left">max</td><td align="right">164878</td><td align="right">64735</td><td align="right">7764</td></tr>
                <tr><td align="left">min</td><td align="right">141305</td><td align="right">55379</td><td align="right">6654</td></tr>
                <tr><td align="left">std</td><td align="right">4284</td><td align="right">1675</td><td align="right">202</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f96-t3-i1900000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">149276</td><td align="right">55826</td><td align="right">7029</td></tr>
                <tr><td align="left">max</td><td align="right">178237</td><td align="right">67212</td><td align="right">8397</td></tr>
                <tr><td align="left">min</td><td align="right">144483</td><td align="right">54009</td><td align="right">6804</td></tr>
                <tr><td align="left">std</td><td align="right">4910</td><td align="right">1882</td><td align="right">231</td></tr>
            </table>
        </div>
    </div>
    <div class="ui three column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f128-t3-i90000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">104070</td><td align="right">52303</td><td align="right">4892</td></tr>
                <tr><td align="left">max</td><td align="right">125837</td><td align="right">63218</td><td align="right">5921</td></tr>
                <tr><td align="left">min</td><td align="right">100241</td><td align="right">50322</td><td align="right">4708</td></tr>
                <tr><td align="left">std</td><td align="right">4563</td><td align="right">2315</td><td align="right">217</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f128-t3-i900000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">119612</td><td align="right">50996</td><td align="right">5622</td></tr>
                <tr><td align="left">max</td><td align="right">142331</td><td align="right">60701</td><td align="right">6698</td></tr>
                <tr><td align="left">min</td><td align="right">115228</td><td align="right">49092</td><td align="right">5411</td></tr>
                <tr><td align="left">std</td><td align="right">4897</td><td align="right">2087</td><td align="right">233</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f128-t3-i1900000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">122654</td><td align="right">49932</td><td align="right">5766</td></tr>
                <tr><td align="left">max</td><td align="right">151223</td><td align="right">62271</td><td align="right">7117</td></tr>
                <tr><td align="left">min</td><td align="right">117901</td><td align="right">47973</td><td align="right">5537</td></tr>
                <tr><td align="left">std</td><td align="right">5733</td><td align="right">2383</td><td align="right">273</td></tr>
            </table>
        </div>
    </div>
    <div class="ui three column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f256-t3-i90000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">40257</td><td align="right">26933</td><td align="right">1888</td></tr>
                <tr><td align="left">max</td><td align="right">48034</td><td align="right">32132</td><td align="right">2252</td></tr>
                <tr><td align="left">min</td><td align="right">38697</td><td align="right">25938</td><td align="right">1815</td></tr>
                <tr><td align="left">std</td><td align="right">1372</td><td align="right">899</td><td align="right">64</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f256-t3-i900000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">46889</td><td align="right">26570</td><td align="right">2199</td></tr>
                <tr><td align="left">max</td><td align="right">55905</td><td align="right">31305</td><td align="right">2619</td></tr>
                <tr><td align="left">min</td><td align="right">19541</td><td align="right">10652</td><td align="right">914</td></tr>
                <tr><td align="left">std</td><td align="right">2597</td><td align="right">1465</td><td align="right">122</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f256-t3-i1900000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">48215</td><td align="right">26088</td><td align="right">2261</td></tr>
                <tr><td align="left">max</td><td align="right">58035</td><td align="right">31098</td><td align="right">2719</td></tr>
                <tr><td align="left">min</td><td align="right">19541</td><td align="right">10560</td><td align="right">916</td></tr>
                <tr><td align="left">std</td><td align="right">2608</td><td align="right">1397</td><td align="right">122</td></tr>
            </table>
        </div>
    </div>
    <div class="ui three column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f256-t3-i2000000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">48676</td><td align="right">26280</td><td align="right">2281</td></tr>
                <tr><td align="left">max</td><td align="right">57006</td><td align="right">30825</td><td align="right">2671</td></tr>
                <tr><td align="left">min</td><td align="right">21733</td><td align="right">11591</td><td align="right">1017</td></tr>
                <tr><td align="left">std</td><td align="right">2572</td><td align="right">1410</td><td align="right">120</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f256-t3-i4000000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">49589</td><td align="right">25645</td><td align="right">2324</td></tr>
                <tr><td align="left">max</td><td align="right">58187</td><td align="right">29978</td><td align="right">2726</td></tr>
                <tr><td align="left">min</td><td align="right">19863</td><td align="right">10113</td><td align="right">930</td></tr>
                <tr><td align="left">std</td><td align="right">2764</td><td align="right">1434</td><td align="right">129</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f256-t3-i6000000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">49667</td><td align="right">25097</td><td align="right">2328</td></tr>
                <tr><td align="left">max</td><td align="right">56950</td><td align="right">28916</td><td align="right">2669</td></tr>
                <tr><td align="left">min</td><td align="right">48245</td><td align="right">24387</td><td align="right">2261</td></tr>
                <tr><td align="left">std</td><td align="right">1600</td><td align="right">824</td><td align="right">75</td></tr>
            </table>
        </div>
    </div>
    <div class="ui three column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f256-t3-i8000000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">51735</td><td align="right">25739</td><td align="right">2428</td></tr>
                <tr><td align="left">max</td><td align="right">62452</td><td align="right">31471</td><td align="right">2933</td></tr>
                <tr><td align="left">min</td><td align="right">22432</td><td align="right">11320</td><td align="right">1054</td></tr>
                <tr><td align="left">std</td><td align="right">2381</td><td align="right">1180</td><td align="right">112</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f256-t3-i10000000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">51293</td><td align="right">25195</td><td align="right">2407</td></tr>
                <tr><td align="left">max</td><td align="right">61252</td><td align="right">30087</td><td align="right">2875</td></tr>
                <tr><td align="left">min</td><td align="right">50506</td><td align="right">24820</td><td align="right">2370</td></tr>
                <tr><td align="left">std</td><td align="right">1011</td><td align="right">491</td><td align="right">48</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f256-t3-i12000000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">50385</td><td align="right">24519</td><td align="right">2365</td></tr>
                <tr><td align="left">max</td><td align="right">55039</td><td align="right">26862</td><td align="right">2584</td></tr>
                <tr><td align="left">min</td><td align="right">49692</td><td align="right">24205</td><td align="right">2332</td></tr>
                <tr><td align="left">std</td><td align="right">578</td><td align="right">280</td><td align="right">27</td></tr>
            </table>
        </div>
    </div>
  </div>
  <hr>
  <p hreeyle="font-size: 80%; text-align:center"><em>The charts included below are for completeness. The figures given are the means and they differ from the means in the above table because, in order to support the different requirements of charting, the first 1/5th of the data is ignored in order to aid visual comparison. The chartline uses the full dataset.</em></p>
</div>


{% include paramtest.html %}

<div class="ui raised padded container segment">
  <p>Replication: 
  <pre style="font-size: 80%"><code class="bash">gapminer -o localhost -p 31397 -u $USER -x $USERPASS -j 5 -e -t 3 -f 25 -s 33554397 -i 600000
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -j 5 -e -t 3 -f 25 -s 33554397 -i 000000
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -j 5 -e -t 3 -f 25 -s 33554397 -i 1200000
</code></pre>
</p>
</div>
