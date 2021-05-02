---
layout: paramtest 
title: Comparison of GPU miner performance at different workunit values ranging from  64 to 2048
description: GPU workunits 64 - 2048, repeated for comparison but affected by changes in difficulty
author: Graham Higgins
testdir: workunits
tests: f64-t1-i3000000-s12000000-w64 f64-t1-i3000000-s12000000-w64-2 f64-t1-i3000000-s12000000-w128 f64-t1-i3000000-s12000000-w128-2 f64-t1-i3000000-s12000000-w256 f64-t1-i3000000-s12000000-w256-2 f64-t1-i3000000-s12000000-w512 f64-t1-i3000000-s12000000-w512-2 f64-t1-i3000000-s12000000-w1024 f64-t1-i3000000-s12000000-w1024-2 f64-t1-i3000000-s12000000-w1536 f64-t1-i3000000-s12000000-w1536-2 f64-t1-i3000000-s12000000-w2048 f64-t1-i3000000-s12000000-w2048-2
---

<div class="ui raised padded container segment">
  <p>Comparison tests of running GapMiner on the GPU at different workunit settings. The tabular data are the more communicative of the relative stability of the performance, apparently irrespective of work group size.</p>
  <a href="pandasvariancetest"></a>
  <hr />
  <p style="font-size: 80%"><em>Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second, <code>gps</code> is average gaps per second, <code>glst</code> is the size of the gaplist and <code>l/s</code> is the time in seconds to scan the gaplist at the reported rate of gaps per second.</em></p>
  <div style="font-family: monospace; font-size:90%">
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-w64</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2737322</td><td align="right">2108754</td></tr>
                <tr><td align="left">max</td><td align="right">3163026</td><td align="right">2443377</td></tr>
                <tr><td align="left">min</td><td align="right">2674775</td><td align="right">2059636</td></tr>
                <tr><td align="left">std</td><td align="right">84251</td><td align="right">65675</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-w64-2</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2759526</td><td align="right">2125126</td></tr>
                <tr><td align="left">max</td><td align="right">3025367</td><td align="right">2336820</td></tr>
                <tr><td align="left">min</td><td align="right">2692220</td><td align="right">2072906</td></tr>
                <tr><td align="left">std</td><td align="right">64533</td><td align="right">50123</td></tr>
            </table>
        </div>
    </div>
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-w128</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2680383</td><td align="right">2063433</td></tr>
                <tr><td align="left">max</td><td align="right">3184772</td><td align="right">2450552</td></tr>
                <tr><td align="left">min</td><td align="right">2621292</td><td align="right">2017818</td></tr>
                <tr><td align="left">std</td><td align="right">100449</td><td align="right">77643</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-w128-2</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2765207</td><td align="right">2124437</td></tr>
                <tr><td align="left">max</td><td align="right">3151566</td><td align="right">2421127</td></tr>
                <tr><td align="left">min</td><td align="right">2703129</td><td align="right">2077218</td></tr>
                <tr><td align="left">std</td><td align="right">70246</td><td align="right">54381</td></tr>
            </table>
        </div>
    </div>
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-w256</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2804137</td><td align="right">2151973</td></tr>
                <tr><td align="left">max</td><td align="right">3175939</td><td align="right">2429929</td></tr>
                <tr><td align="left">min</td><td align="right">2745985</td><td align="right">2106971</td></tr>
                <tr><td align="left">std</td><td align="right">74992</td><td align="right">57290</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-w256-2</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2725860</td><td align="right">2086968</td></tr>
                <tr><td align="left">max</td><td align="right">3106625</td><td align="right">2376314</td></tr>
                <tr><td align="left">min</td><td align="right">2667572</td><td align="right">2042771</td></tr>
                <tr><td align="left">std</td><td align="right">84491</td><td align="right">64955</td></tr>
            </table>
        </div>
    </div>
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-w512</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2710271</td><td align="right">2062601</td></tr>
                <tr><td align="left">max</td><td align="right">3093761</td><td align="right">2339704</td></tr>
                <tr><td align="left">min</td><td align="right">2678754</td><td align="right">2038645</td></tr>
                <tr><td align="left">std</td><td align="right">62097</td><td align="right">46008</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-w512-2</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2799433</td><td align="right">2127873</td></tr>
                <tr><td align="left">max</td><td align="right">3207097</td><td align="right">2427369</td></tr>
                <tr><td align="left">min</td><td align="right">2715224</td><td align="right">2063722</td></tr>
                <tr><td align="left">std</td><td align="right">71311</td><td align="right">53558</td></tr>
            </table>
        </div>
    </div>
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-w1024</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2653671</td><td align="right">1996553</td></tr>
                <tr><td align="left">max</td><td align="right">3124300</td><td align="right">2336881</td></tr>
                <tr><td align="left">min</td><td align="right">2614748</td><td align="right">1968835</td></tr>
                <tr><td align="left">std</td><td align="right">71326</td><td align="right">50495</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-w1024-2</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2625907</td><td align="right">1965258</td></tr>
                <tr><td align="left">max</td><td align="right">2699170</td><td align="right">2020437</td></tr>
                <tr><td align="left">min</td><td align="right">2494227</td><td align="right">1868545</td></tr>
                <tr><td align="left">std</td><td align="right">58805</td><td align="right">44273</td></tr>
            </table>
        </div>
    </div>
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-w1536</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2775661</td><td align="right">2050179</td></tr>
                <tr><td align="left">max</td><td align="right">2812113</td><td align="right">2067402</td></tr>
                <tr><td align="left">min</td><td align="right">2720995</td><td align="right">1956028</td></tr>
                <tr><td align="left">std</td><td align="right">11525</td><td align="right">15230</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-w1536-2</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2811299</td><td align="right">2089269</td></tr>
                <tr><td align="left">max</td><td align="right">2844131</td><td align="right">2109555</td></tr>
                <tr><td align="left">min</td><td align="right">2792547</td><td align="right">2013919</td></tr>
                <tr><td align="left">std</td><td align="right">7719</td><td align="right">8694</td></tr>
            </table>
        </div>
    </div>
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-w2048</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2727639</td><td align="right">2002407</td></tr>
                <tr><td align="left">max</td><td align="right">3171164</td><td align="right">2280500</td></tr>
                <tr><td align="left">min</td><td align="right">2638171</td><td align="right">1937303</td></tr>
                <tr><td align="left">std</td><td align="right">102494</td><td align="right">69539</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f64-t1-i3000000-s12000000-w2048-2</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th></tr>
                <tr><td align="left">mean</td><td align="right">2632909</td><td align="right">1935633</td></tr>
                <tr><td align="left">max</td><td align="right">2684031</td><td align="right">1970492</td></tr>
                <tr><td align="left">min</td><td align="right">2605448</td><td align="right">1815580</td></tr>
                <tr><td align="left">std</td><td align="right">18431</td><td align="right">15236</td></tr>
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
