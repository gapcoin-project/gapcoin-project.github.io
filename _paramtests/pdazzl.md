---
layout: paramtest 
title: Comparison of pdazzl’s improved CRT files vs standard
description: pdazzl contributed several improved CRT files
author: Graham Higgins
testdir: pdazzl
tests: f416-dist f416-pdazzl f512-dist f512-pdazzl f1024-dist f1024-pdazzl
---

<div class="ui raised padded container segment">
  <p>Comparison tests of pdazzl’s contributed improved CRT files for shift 416, 512 and 1024 versus the CRT files in the standard distribution. The tabular data are the more communicative of the performance improvement in primes per sec that increases with shift size.</p>
  <a href="pandasvariancetest"></a>
  <hr />
  <p style="font-size: 80%"><em>Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second, <code>gps</code> is average gaps per second, <code>glst</code> is the size of the gaplist and <code>l/s</code> is the time in seconds to scan the gaplist at the reported rate of gaps per second.</em></p>
  <div style="font-family: monospace; font-size:90%">
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f416-dist</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">1957819</td><td align="right">2140442</td><td align="right">447</td><td align="right">1641</td><td align="right">0.92</td><td align="right">3.67</td></tr>
                <tr><td align="left">max</td><td align="right">2172018</td><td align="right">4252831</td><td align="right">481</td><td align="right">6299</td><td align="right">1.83</td><td align="right">13.10</td></tr>
                <tr><td align="left">min</td><td align="right">1756714</td><td align="right">18395</td><td align="right">442</td><td align="right">7</td><td align="right">0.01</td><td align="right">0.02</td></tr>
                <tr><td align="left">std</td><td align="right">38025</td><td align="right">1230051</td><td align="right">7</td><td align="right">1251</td><td align="right">0.53</td><td align="right">170.23</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f416-pdazzl</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">2195881</td><td align="right">2087528</td><td align="right">440</td><td align="right">2078</td><td align="right">1.04</td><td align="right">4.73</td></tr>
                <tr><td align="left">max</td><td align="right">2639096</td><td align="right">4166281</td><td align="right">471</td><td align="right">7001</td><td align="right">2.08</td><td align="right">14.86</td></tr>
                <tr><td align="left">min</td><td align="right">2046706</td><td align="right">17059</td><td align="right">436</td><td align="right">50</td><td align="right">0.01</td><td align="right">0.11</td></tr>
                <tr><td align="left">std</td><td align="right">44599</td><td align="right">1207122</td><td align="right">4</td><td align="right">1665</td><td align="right">0.60</td><td align="right">415.28</td></tr>
            </table>
        </div>
    </div>
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f512-dist</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">2332323</td><td align="right">1610234</td><td align="right">297</td><td align="right">4272</td><td align="right">1.07</td><td align="right">14.39</td></tr>
                <tr><td align="left">max</td><td align="right">2487441</td><td align="right">3173364</td><td align="right">312</td><td align="right">10348</td><td align="right">2.12</td><td align="right">33.17</td></tr>
                <tr><td align="left">min</td><td align="right">2262761</td><td align="right">10965</td><td align="right">294</td><td align="right">103</td><td align="right">0.00</td><td align="right">0.35</td></tr>
                <tr><td align="left">std</td><td align="right">27394</td><td align="right">920097</td><td align="right">3</td><td align="right">2771</td><td align="right">0.61</td><td align="right">1085.45</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f512-pdazzl</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">3326481</td><td align="right">1596678</td><td align="right">296</td><td align="right">4296</td><td align="right">1.59</td><td align="right">14.51</td></tr>
                <tr><td align="left">max</td><td align="right">4023035</td><td align="right">3166622</td><td align="right">327</td><td align="right">9970</td><td align="right">3.18</td><td align="right">30.49</td></tr>
                <tr><td align="left">min</td><td align="right">2849719</td><td align="right">12432</td><td align="right">294</td><td align="right">148</td><td align="right">0.01</td><td align="right">0.50</td></tr>
                <tr><td align="left">std</td><td align="right">81105</td><td align="right">914440</td><td align="right">4</td><td align="right">2837</td><td align="right">0.92</td><td align="right">692.23</td></tr>
            </table>
        </div>
    </div>
    <div class="ui two column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f1024-dist</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">1659123</td><td align="right">246377</td><td align="right">46</td><td align="right">3399</td><td align="right">0.69</td><td align="right">73.36</td></tr>
                <tr><td align="left">max</td><td align="right">2042915</td><td align="right">489480</td><td align="right">50</td><td align="right">8487</td><td align="right">1.37</td><td align="right">169.74</td></tr>
                <tr><td align="left">min</td><td align="right">1569151</td><td align="right">1073</td><td align="right">32</td><td align="right">95</td><td align="right">0.00</td><td align="right">2.97</td></tr>
                <tr><td align="left">std</td><td align="right">50704</td><td align="right">140997</td><td align="right">1</td><td align="right">2522</td><td align="right">0.39</td><td align="right">2011.18</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">f1024-pdazzl</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">2598131</td><td align="right">250154</td><td align="right">47</td><td align="right">3399</td><td align="right">1.11</td><td align="right">73.05</td></tr>
                <tr><td align="left">max</td><td align="right">3399555</td><td align="right">494788</td><td align="right">53</td><td align="right">8459</td><td align="right">2.19</td><td align="right">159.60</td></tr>
                <tr><td align="left">min</td><td align="right">2546295</td><td align="right">1152</td><td align="right">37</td><td align="right">94</td><td align="right">0.00</td><td align="right">2.54</td></tr>
                <tr><td align="left">std</td><td align="right">85572</td><td align="right">143107</td><td align="right">1</td><td align="right">2459</td><td align="right">0.63</td><td align="right">2135.05</td></tr>
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
  <pre style="font-size:78%"><code class="bash">gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -f  416 -i [as-discovered] -r crt/dist/crt-22m-0416s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -f  416 -i [as-discovered] -r crt/pdazzl/crt-22m-0416s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -f  512 -i [as-discovered] -r crt/dist/crt-22m-0512s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -f  512 -i [as-discovered] -r crt/pdazzl/crt-22m-0512s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -f 1024 -i [as-discovered] -r crt/dist/crt-22m-1024s.txt
gapminer -o localhost -p 31397 -u $USER -x $USERPASS -e -j 5 -t 4 -f 1024 -i [as-discovered] -r crt/pdazzl/crt-22m-1024s.txt</code></pre>
</p>
</div>
