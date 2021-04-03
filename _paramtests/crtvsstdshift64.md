---
layout: paramtest
title: Performance test of non-crt vs crt on shift64
description: crtvsstdshift64 -f 64 -t 4 std vs crt
author: Graham Higgins
testdir: crtvsstdshift64
tests: std-f64-s33554397-i90000 crt-f64-s33554397-i6490 std-f96-s33554397-i90000 crt-f96-s33554397-i12000 std-f128-s33554397-i90000 crt-f128-s33554397-i14500 std-f256-s33554397-i90000 crt-f256-s33554397-i27250 std-f512-s33554397-i90000 crt-f512-s33554397-i96000 std-f768-s4800000-i640000 crt-f768-i280000
---

<div class="ui raised padded container segment">
  <p>Testing non-crt vs crt over a range of increasing shift values.</p>
  <div style="font-family: monospace; font-size:100%">
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
            <p class="ui tiny header" style="margin:0;padding:0">crt-f64-s33554397-i6490</p>
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
            <p class="ui tiny header" style="margin:0;padding:0">crt-f96-s33554397-i12000</p>
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
            <p class="ui tiny header" style="margin:0;padding:0">crt-f128-s33554397-i14500</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">896763</td><td align="right">6856103</td><td align="right">3207</td><td align="right">3508</td><td align="right">0.44</td><td align="right">1.09</td></tr>
                <tr><td align="left">max</td><td align="right">934138</td><td align="right">13500776</td><td align="right">3795</td><td align="right">18170</td><td align="right">0.87</td><td align="right">4.79</td></tr>
                <tr><td align="left">min</td><td align="right">635251</td><td align="right">80579</td><td align="right">3156</td><td align="right">9</td><td align="right">0.00</td><td align="right">0.00</td></tr>
                <tr><td align="left">std</td><td align="right">41024</td><td align="right">3882092</td><td align="right">73</td><td align="right">3613</td><td align="right">0.26</td><td align="right">49.74</td></tr>
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
            <p class="ui tiny header" style="margin:0;padding:0">crt-f256-s33554397-i27250</p>
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
                <tr><td align="left">mean</td><td align="right">14562</td><td align="right">12381</td><td align="right">682</td></tr>
                <tr><td align="left">max</td><td align="right">16939</td><td align="right">14370</td><td align="right">793</td></tr>
                <tr><td align="left">min</td><td align="right">8888</td><td align="right">7269</td><td align="right">415</td></tr>
                <tr><td align="left">std</td><td align="right">598</td><td align="right">516</td><td align="right">28</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0">crt-f512-s33554397-i96000</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th><th align="right" width="16%">glst</th><th align="right" width="16%">bpc</th><th align="right" width="16%">l/s</th></tr>
                <tr><td align="left">mean</td><td align="right">3060364</td><td align="right">2937684</td><td align="right">398</td><td align="right">5930</td><td align="right">1.38</td><td align="right">14.91</td></tr>
                <tr><td align="left">max</td><td align="right">3478810</td><td align="right">5966714</td><td align="right">467</td><td align="right">14401</td><td align="right">2.77</td><td align="right">30.84</td></tr>
                <tr><td align="left">min</td><td align="right">2858271</td><td align="right">30537</td><td align="right">388</td><td align="right">233</td><td align="right">0.01</td><td align="right">0.60</td></tr>
                <tr><td align="left">std</td><td align="right">81108</td><td align="right">1713760</td><td align="right">10</td><td align="right">4013</td><td align="right">0.81</td><td align="right">388.74</td></tr>
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
