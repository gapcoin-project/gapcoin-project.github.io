---
layout: paramtest 
title: Comparison of miner performance with optimised gmp/mpfr libs
description: Comparison of standard vs optimised at -t 4 -f 32
author: Graham Higgins
testdir: stdvsopt
tests: gapminer-standard gapminer-optimised
---

<div class="ui raised padded container segment">
  <p>Are there performance advantages to be gained by linking GapMiner against locally-compiled static GMP and MPFR libraries which have been optimised for the host CPU, as opposed to using the standard distro packages which are only configured for the host OS?</p>
  <p>This test is a comparison between reported performance of standard GapMiner versus one compiled with optimised GMP/MPFR (where “optimised” means “compiled with GCC flags <code>-static -march=native -mtune=native</code>”).</p>
  <hr />
  <p style="font-size: 80%"><em>Column labels map directly to miner output: <code>pps</code> is average primes per second, <code>tps</code> is average tests per second, <code>gps</code> is average gaps per second, <code>glst</code> is the size of the gaplist and <code>l/s</code> is the time in seconds to scan the gaplist at the reported rate of gaps per second.</em></p>
  <div style="font-family: monospace; font-size:90%">
    <div class="ui three column doubling stackable grid container">
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0;color:blue">standard gapminer</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">381417</td><td align="right">121373</td><td align="right">17836</td></tr>
                <tr><td align="left">max</td><td align="right">450402</td><td align="right">143195</td><td align="right">21061</td></tr>
                <tr><td align="left">min</td><td align="right">371074</td><td align="right">118095</td><td align="right">17352</td></tr>
                <tr><td align="left">std</td><td align="right">15163</td><td align="right">4804</td><td align="right">709</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0;color:blue">optimised gapminer</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right">409228</td><td align="right">130275</td><td align="right">19137</td></tr>
                <tr><td align="left">max</td><td align="right">479724</td><td align="right">152951</td><td align="right">22436</td></tr>
                <tr><td align="left">min</td><td align="right">398576</td><td align="right">126829</td><td align="right">18638</td></tr>
                <tr><td align="left">std</td><td align="right">15814</td><td align="right">5077</td><td align="right">740</td></tr>
            </table>
        </div>
        <div class="column">
            <p class="ui tiny header" style="margin:0;padding:0;color:blue">per cent improvement</p>
            <table width="100%">
                <tr><th align="left">measure</th><th align="right" width="16%">pps</th><th align="right" width="16%">tps</th><th align="right" width="16%">gps</th></tr>
                <tr><td align="left">mean</td><td align="right"><span style="color: green">7.29</span></td><td align="right"><span style="color: green">7.33</span></td><td align="right"><span style="color: green">7.29</span></td></tr>
                <tr><td align="left">max</td><td align="right"><span style="color: green">6.51</span></td><td align="right"><span style="color: green">6.81</span></td><td align="right"><span style="color: green">6.53</span></td></tr>
                <tr><td align="left">min</td><td align="right"><span style="color: green">7.41</span></td><td align="right"><span style="color: green">7.34</span></td><td align="right"><span style="color: green">7.41</span></td></tr>
                <tr><td align="left">std</td><td align="right"><span style="color: orange">4.29</span></td><td align="right"><span style="color: orange">5.68</span></td><td align="right"><span style="color: orange">4.37</span></td></tr>
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
  <pre style="font-size:80%"><code class="bash">./bin/gapminer-standard  -o localhost -p 31397 -u $(RPCUSER) -x $(RPCPASSWORD) -e -t 4 -f 32  > standard-miner.log 2>&1
./bin/gapminer-optimised -o localhost -p 31397 -u $(RPCUSER) -x $(RPCPASSWORD) -e -t 4 -f 32  > optimised-miner.log 2>&1
</code></pre>
</p>
</div>
