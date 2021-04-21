---
layout: paramtest
title: Comparison of changing --sieve-primes (essentially ineffective in non-CRT mining)
description: <code>--sieve-primes</code> is described as a secondary parameter with some influence on miner performance.
author: Graham Higgins
testdir: sieveprimes
tests: f25-t3-i600000-s33554432 f25-t3-i900000-s33554432-0 f25-t3-i1200000-s33554432 f25-t3-i300000-s33554432 f25-t3-i900000-s33554432-1 f25-t3-i1500000-s33554432 f25-t3-i50000-s33554432 f25-t3-i900000-s33554432-2 f25-t3-i1750000-s33554432 f25-t3-i5000-s33554432 f25-t3-i900000-s33554432-3 f25-t3-i2750000-s33554432
---

<div class="ui raised padded container segment">
  <p>In a post to the bitcointalk thread, j0nn9 <a href="https://bitcointalk.org/index.php?topic=822498.msg9295189#msg9295189" target="_blank">describes the GapMiner parameters</a>: “shift should be the most sensitive parameter, because it controls the bit size of the primes, second would be sieve primes”. The tests reported here are of systematic changes to the value of <code>sieve-primes</code> in <strong><em>non-CRT</em></strong> mining.</p> 
  <p>Each row of three tests is a single, simultaneous run and can be compared laterally - but not vertically because for each run of three tests, the difficulty changes and thwarts comparison. Of note is the <code>std</code> value, the standard deviation - it swamps any lateral differences, meaning that the changes had no statistically significant effect - apart from the last run in which the number of primes in the sieve was reduced to 5000 and that does seem have cramped GapMiner’s style somewhat. Increasing the value has no apparent effect for <strong><em>non-CRT</em></strong> mining.</p>
  <p>The basic conclusion - for non-CRT mining (), the default of 900000 is just fine and doesn’t benefit from being increased. (I needed to check this for the purposes of designing the GUI for the client’s Mining tab). By contrast, the value set for <code>sieve-primes</code> <em>is</em> influential on <a href="/paramtests/crtvsstdshift64/" target="_blank">performance when mining with CRT</a>.</p>
  <div style="font-family: monospace; font-size:90%">
    <hr>
    <p style="font-size: 80%"><em>Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second, <code>gps</code> is average gaps per second.</em></p>
    <div class="ui three column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f25-t3-i600000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">288742</td><td align="right">92340</td><td align="right">13545</td></tr>
                <tr><td align="left">max</td><td align="right">317649</td><td align="right">101501</td><td align="right">14901</td></tr>
                <tr><td align="left">min</td><td align="right">284330</td><td align="right">90966</td><td align="right">13340</td></tr>
                <tr><td align="left">std</td><td align="right">6017</td><td align="right">1906</td><td align="right">282</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f25-t3-i900000-s33554432-0</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">291217</td><td align="right">90716</td><td align="right">13662</td></tr>
                <tr><td align="left">max</td><td align="right">312908</td><td align="right">97541</td><td align="right">14680</td></tr>
                <tr><td align="left">min</td><td align="right">287962</td><td align="right">88782</td><td align="right">13511</td></tr>
                <tr><td align="left">std</td><td align="right">4913</td><td align="right">1513</td><td align="right">231</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f25-t3-i1200000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">293831</td><td align="right">89845</td><td align="right">13784</td></tr>
                <tr><td align="left">max</td><td align="right">317022</td><td align="right">96827</td><td align="right">14871</td></tr>
                <tr><td align="left">min</td><td align="right">276128</td><td align="right">84359</td><td align="right">12952</td></tr>
                <tr><td align="left">std</td><td align="right">4815</td><td align="right">1471</td><td align="right">226</td></tr>
            </table>
        </div>
    </div>
    <div class="ui three column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f25-t3-i300000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">270476</td><td align="right">90892</td><td align="right">12709</td></tr>
                <tr><td align="left">max</td><td align="right">318964</td><td align="right">107074</td><td align="right">14981</td></tr>
                <tr><td align="left">min</td><td align="right">264944</td><td align="right">89056</td><td align="right">12450</td></tr>
                <tr><td align="left">std</td><td align="right">9208</td><td align="right">3073</td><td align="right">432</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f25-t3-i900000-s33554432-1</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">282476</td><td align="right">88161</td><td align="right">13273</td></tr>
                <tr><td align="left">max</td><td align="right">321449</td><td align="right">100207</td><td align="right">15101</td></tr>
                <tr><td align="left">min</td><td align="right">277234</td><td align="right">86505</td><td align="right">13027</td></tr>
                <tr><td align="left">std</td><td align="right">8394</td><td align="right">2623</td><td align="right">394</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f25-t3-i1500000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">285626</td><td align="right">86265</td><td align="right">13420</td></tr>
                <tr><td align="left">max</td><td align="right">336856</td><td align="right">102028</td><td align="right">15828</td></tr>
                <tr><td align="left">min</td><td align="right">279746</td><td align="right">84464</td><td align="right">13145</td></tr>
                <tr><td align="left">std</td><td align="right">9871</td><td align="right">3038</td><td align="right">463</td></tr>
            </table>
        </div>
    </div>
    <div class="ui three column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f25-t3-i50000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">235022</td><td align="right">90550</td><td align="right">11048</td></tr>
                <tr><td align="left">max</td><td align="right">263020</td><td align="right">101571</td><td align="right">12363</td></tr>
                <tr><td align="left">min</td><td align="right">227548</td><td align="right">87664</td><td align="right">10697</td></tr>
                <tr><td align="left">std</td><td align="right">7667</td><td align="right">2975</td><td align="right">360</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f25-t3-i900000-s33554432-2</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">278185</td><td align="right">86807</td><td align="right">13076</td></tr>
                <tr><td align="left">max</td><td align="right">309569</td><td align="right">96421</td><td align="right">14548</td></tr>
                <tr><td align="left">min</td><td align="right">269209</td><td align="right">84029</td><td align="right">12656</td></tr>
                <tr><td align="left">std</td><td align="right">9111</td><td align="right">2801</td><td align="right">427</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f25-t3-i1750000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">281366</td><td align="right">84170</td><td align="right">13226</td></tr>
                <tr><td align="left">max</td><td align="right">318632</td><td align="right">95051</td><td align="right">14973</td></tr>
                <tr><td align="left">min</td><td align="right">271544</td><td align="right">81234</td><td align="right">12766</td></tr>
                <tr><td align="left">std</td><td align="right">10291</td><td align="right">3055</td><td align="right">482</td></tr>
            </table>
        </div>
     </div>
    <div class="ui three column doubling stackable grid container">
       <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f25-t3-i5000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">205187</td><td align="right">97723</td><td align="right">9651</td></tr>
                <tr><td align="left">max</td><td align="right">234228</td><td align="right">112672</td><td align="right">11026</td></tr>
                <tr><td align="left">min</td><td align="right">202922</td><td align="right">96647</td><td align="right">9547</td></tr>
                <tr><td align="left">std</td><td align="right">3656</td><td align="right">1834</td><td align="right">173</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f25-t3-i900000-s33554432-3</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">296291</td><td align="right">92537</td><td align="right">13936</td></tr>
                <tr><td align="left">max</td><td align="right">342869</td><td align="right">107368</td><td align="right">16136</td></tr>
                <tr><td align="left">min</td><td align="right">293649</td><td align="right">91739</td><td align="right">13816</td></tr>
                <tr><td align="left">std</td><td align="right">5782</td><td align="right">1869</td><td align="right">274</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f25-t3-i2750000-s33554432</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">295028</td><td align="right">85945</td><td align="right">13877</td></tr>
                <tr><td align="left">max</td><td align="right">329991</td><td align="right">95986</td><td align="right">15526</td></tr>
                <tr><td align="left">min</td><td align="right">292370</td><td align="right">85215</td><td align="right">13756</td></tr>
                <tr><td align="left">std</td><td align="right">4948</td><td align="right">1445</td><td align="right">234</td></tr>
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
