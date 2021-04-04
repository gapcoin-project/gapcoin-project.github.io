---
layout: paramtest
title: Comparison of non-CRT vs CRT at various shift settings
description: CRT vs non-CRT at shifts 64, 96, 128, 179, 256, 512 and 768
author: Graham Higgins
testdir: crtvsstdshift64
tests: std-f64-s33554397-i90000 crt-f64-i6490 std-f96-s33554397-i90000 crt-f96-i12000 std-f128-s33554397-i90000 crt-f128-i14550 std-f179-s33554397-i90000 crt-f179-i16381 std-f256-s33554397-i90000 crt-f256-i27250 std-f512-s33554397-i90000 crt-f512-i130000 std-f768-s4800000-i640000 crt-f768-i280000
---

<div class="ui raised padded container segment">
  <p>In <a href="https://bitcointalk.org/index.php?topic=822498.msg11296309#msg11296309" target="_blank">the announcement of Revision 5</a>, the Gapcoin miner is described as “capable of using the Chinese Remainder Theorem to speed up mining with large shift”. Unfortunately, the announcement was unaccompanied by any indication of what level of shift was considered “large”, although some insight can be gained from the fact that the minimum shift level supported by the associated “crt files” was - and is - 64.</p>
  <p>Tests are non-CRT vs. CRT mining over a selected range of <code>--shift</code> settings: <span style="color:orange">64</span>, <span style="color:orange">96</span>, <span style="color:orange">128</span>, <span style="color:orange">179</span>, <span style="color:orange">256</span>, <span style="color:orange">512</span> and <span style="color:orange">768</span>.</p>
  <p>Except for shift 768, non-CRT tests used default settings for <code>--sieve-size</code> and <code>--sieve-primes</code>. For the CRT tests, in order to keep the size of the gaplist within the recommended bounds, the value of <code>--sieve-primes</code> is adjusted according to the selected value of <code>--shift</code>.</p>
  <p>Tests were run simultaneously to control for changes in difficulty that otherwise affect the results to a degree that thwarts comparison when tests are run serially.</p>
  <p><em>Choosing an appropriate value for <code>--sieve-size</code> proved to be something of a “black art”. At shift 179, it proved impossible to discover a value for <code>--sieve-size</code> which produced a gaplist that neither reached zero nor exceeded 9000. Selecting a value of 1638<b>2</b> resulted in a frequently-empty gaplist but selecting the minimum decrement of one less (1638<b>1</b>) resulted in a gaplist size that approached 50000 at times.</em></p>
  <p><em>A shift of 768 proved to be the highest shift setting possible to use with non-CRT mining. At any higher setting the miner-reported statistics become nonsensical - which can be taken as a useful proxy for “only use CRT at this shift setting”).</em></p>
  <hr/>
  <p style="font-size: 80%"><em>Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second, <code>gps</code> is average gaps per second, <code>glst</code> is the size of the gaplist and <code>l/s</code> is the time in seconds to scan the gaplist at the reported rate of gaps per second.</em></p>
  <div style="font-family: monospace; font-size:90%">
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">std-f64-s33554397-i90000</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">280837</td><td align="right">99472</td><td align="right">13148</td></tr>
                <tr><td align="left">max</td><td align="right">354288</td><td align="right">125605</td><td align="right">16586</td></tr>
                <tr><td align="left">min</td><td align="right">275451</td><td align="right">97571</td><td align="right">12896</td></tr>
                <tr><td align="left">std</td><td align="right">10932</td><td align="right">3872</td><td align="right">511</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">crt-f64-i6490</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">517700</td><td align="right">7187127</td><td align="right">6884</td><td align="right">2095</td><td align="right">0.23</td><td align="right">0.30</td></tr>
                <tr><td align="left">max</td><td align="right">706107</td><td align="right">14294784</td><td align="right">9883</td><td align="right">6671</td><td align="right">0.47</td><td align="right">0.67</td></tr>
                <tr><td align="left">min</td><td align="right">463066</td><td align="right">108904</td><td align="right">6740</td><td align="right">3</td><td align="right">0.00</td><td align="right">0.00</td></tr>
                <tr><td align="left">std</td><td align="right">20342</td><td align="right">4067984</td><td align="right">300</td><td align="right">1542</td><td align="right">0.14</td><td align="right">5.15</td></tr>
            </table>
        </div>
    </div>
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">std-f96-s33554397-i90000</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">150002</td><td align="right">58421</td><td align="right">7023</td></tr>
                <tr><td align="left">max</td><td align="right">158244</td><td align="right">61486</td><td align="right">7408</td></tr>
                <tr><td align="left">min</td><td align="right">149244</td><td align="right">58156</td><td align="right">6988</td></tr>
                <tr><td align="left">std</td><td align="right">934</td><td align="right">331</td><td align="right">43</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">crt-f96-i12000</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">733254</td><td align="right">5148324</td><td align="right">3808</td><td align="right">3008</td><td align="right">0.32</td><td align="right">0.79</td></tr>
                <tr><td align="left">max</td><td align="right">878003</td><td align="right">10191541</td><td align="right">5664</td><td align="right">13327</td><td align="right">0.61</td><td align="right">2.35</td></tr>
                <tr><td align="left">min</td><td align="right">365175</td><td align="right">61626</td><td align="right">3755</td><td align="right">12</td><td align="right">0.00</td><td align="right">0.00</td></tr>
                <tr><td align="left">std</td><td align="right">43174</td><td align="right">2948194</td><td align="right">133</td><td align="right">2696</td><td align="right">0.18</td><td align="right">20.23</td></tr>
            </table>
        </div>
    </div>
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">std-f128-s33554397-i90000</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">125108</td><td align="right">53430</td><td align="right">5878</td></tr>
                <tr><td align="left">max</td><td align="right">138720</td><td align="right">59596</td><td align="right">6519</td></tr>
                <tr><td align="left">min</td><td align="right">123788</td><td align="right">52851</td><td align="right">5816</td></tr>
                <tr><td align="left">std</td><td align="right">2055</td><td align="right">916</td><td align="right">96</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">crt-f128-i14550</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">662783</td><td align="right">6857580</td><td align="right">3202</td><td align="right">3338</td><td align="right">0.36</td><td align="right">1.04</td></tr>
                <tr><td align="left">max</td><td align="right">922795</td><td align="right">13527877</td><td align="right">3839</td><td align="right">12381</td><td align="right">0.71</td><td align="right">3.23</td></tr>
                <tr><td align="left">min</td><td align="right">620894</td><td align="right">90517</td><td align="right">3161</td><td align="right">8</td><td align="right">0.00</td><td align="right">0.00</td></tr>
                <tr><td align="left">std</td><td align="right">29901</td><td align="right">3884665</td><td align="right">71</td><td align="right">2569</td><td align="right">0.20</td><td align="right">36.09</td></tr>
            </table>
        </div>
    </div>
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">std-f179-s33554397-i90000</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">110018</td><td align="right">53537</td><td align="right">5203</td></tr>
                <tr><td align="left">max</td><td align="right">142859</td><td align="right">69938</td><td align="right">6759</td></tr>
                <tr><td align="left">min</td><td align="right">106573</td><td align="right">51837</td><td align="right">5039</td></tr>
                <tr><td align="left">std</td><td align="right">5305</td><td align="right">2607</td><td align="right">252</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">crt-f179-i16381</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">1719581</td><td align="right">11259653</td><td align="right">2801</td><td align="right">15803</td><td align="right">0.95</td><td align="right">5.64</td></tr>
                <tr><td align="left">max</td><td align="right">2097464</td><td align="right">21849802</td><td align="right">3640</td><td align="right">48129</td><td align="right">1.89</td><td align="right">13.22</td></tr>
                <tr><td align="left">min</td><td align="right">1634362</td><td align="right">176471</td><td align="right">2715</td><td align="right">936</td><td align="right">0.01</td><td align="right">0.34</td></tr>
                <tr><td align="left">std</td><td align="right">40319</td><td align="right">6237012</td><td align="right">133</td><td align="right">11759</td><td align="right">0.55</td><td align="right">88.32</td></tr>
            </table>
        </div>
    </div>
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">std-f256-s33554397-i90000</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">61600</td><td align="right">35056</td><td align="right">2894</td></tr>
                <tr><td align="left">max</td><td align="right">78988</td><td align="right">44501</td><td align="right">3708</td></tr>
                <tr><td align="left">min</td><td align="right">59878</td><td align="right">33584</td><td align="right">2810</td></tr>
                <tr><td align="left">std</td><td align="right">2707</td><td align="right">1496</td><td align="right">127</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">crt-f256-i27250</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">2504918</td><td align="right">8233398</td><td align="right">1587</td><td align="right">1799</td><td align="right">1.19</td><td align="right">1.13</td></tr>
                <tr><td align="left">max</td><td align="right">3225400</td><td align="right">16197158</td><td align="right">2139</td><td align="right">6084</td><td align="right">2.32</td><td align="right">2.84</td></tr>
                <tr><td align="left">min</td><td align="right">2433006</td><td align="right">110793</td><td align="right">1533</td><td align="right">4</td><td align="right">0.01</td><td align="right">0.00</td></tr>
                <tr><td align="left">std</td><td align="right">119752</td><td align="right">4568658</td><td align="right">89</td><td align="right">1400</td><td align="right">0.67</td><td align="right">15.71</td></tr>
            </table>
        </div>
    </div>
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">std-f512-s33554397-i90000</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">10748</td><td align="right">9234</td><td align="right">507</td></tr>
                <tr><td align="left">max</td><td align="right">11115</td><td align="right">9591</td><td align="right">524</td></tr>
                <tr><td align="left">min</td><td align="right">10683</td><td align="right">9152</td><td align="right">503</td></tr>
                <tr><td align="left">std</td><td align="right">71</td><td align="right">85</td><td align="right">3</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">crt-f512-i130000</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">2338017</td><td align="right">1642804</td><td align="right">301</td><td align="right">2369</td><td align="right">1.22</td><td align="right">7.87</td></tr>
                <tr><td align="left">max</td><td align="right">3549117</td><td align="right">3269947</td><td align="right">318</td><td align="right">5893</td><td align="right">2.44</td><td align="right">18.53</td></tr>
                <tr><td align="left">min</td><td align="right">2173579</td><td align="right">8416</td><td align="right">299</td><td align="right">38</td><td align="right">0.01</td><td align="right">0.13</td></tr>
                <tr><td align="left">std</td><td align="right">97558</td><td align="right">946970</td><td align="right">3</td><td align="right">1645</td><td align="right">0.71</td><td align="right">496.96</td></tr>
            </table>
        </div>
    </div>
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">std-f768-s4800000-i640000</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">3658</td><td align="right">4255</td><td align="right">172</td></tr>
                <tr><td align="left">max</td><td align="right">4783</td><td align="right">5329</td><td align="right">224</td></tr>
                <tr><td align="left">min</td><td align="right">3576</td><td align="right">4177</td><td align="right">168</td></tr>
                <tr><td align="left">std</td><td align="right">141</td><td align="right">128</td><td align="right">7</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">crt-f768-i280000</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">2316789</td><td align="right">607655</td><td align="right">109</td><td align="right">3146</td><td align="right">1.16</td><td align="right">28.98</td></tr>
                <tr><td align="left">max</td><td align="right">3302115</td><td align="right">1201411</td><td align="right">127</td><td align="right">8185</td><td align="right">2.28</td><td align="right">64.45</td></tr>
                <tr><td align="left">min</td><td align="right">2243369</td><td align="right">7539</td><td align="right">107</td><td align="right">46</td><td align="right">0.01</td><td align="right">0.43</td></tr>
                <tr><td align="left">std</td><td align="right">119993</td><td align="right">345476</td><td align="right">2</td><td align="right">2283</td><td align="right">0.66</td><td align="right">1022.23</td></tr>
            </table>
        </div>
    </div>
  </div>
</div>

{% include paramtest.html %}

<div class="ui raised padded container segment">
  <p>Replication: 
  <pre style="font-size: 70%"><code class="bash">timeout 1000s gapminer -o localhost -p 31397 -u $USER -x $USERPASS -j 5 -e -f 64 -t 4
timeout 1000s gapminer -o localhost -p 31397 -u $USER -x $USERPASS -j 5 -e -f 64 -i [as-discovered] -t 4 -d 3 -r crt/dist/crt-22m-0064s.txt</code></pre>
</p>
</div>
