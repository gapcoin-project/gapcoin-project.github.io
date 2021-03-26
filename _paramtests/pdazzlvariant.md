---
layout: paramtest
title: pdazzl variants of sieve-size and sieve-primes vs defaults for shifts 21, 22, 23, 24, 26 and 27
description: pdazzl variant test -f 21 -s 2097152 -i 56474, -f 22 -s 4194304 -i 106974, -f 23 -s 8388608 -i 203094, -f 24 -s 16777216 -i 386702, -f 26 -s 67108864 -i 1410973, -f 27 -s 134217728 -i 2703387
author: Graham Higgins
tests: default-21-33554432-900000 pdazzlvariant-21-2097152-56474 default-22-33554432-900000 pdazzlvariant-22-4194304-106974 default-23-33554432-900000 pdazzlvariant-23-8388608-203094 default-24-33554432-900000 pdazzlvariant-24-6777216-386702 default-26-33554432-900000 pdazzlvariant-26-67108864-1410973 default-27-33554432-900000 pdazzlvariant-27-134217728-2703387 
---

<div class="ui vertical segment">
  <div class="ui centered page grid">
    <div class="row">
      <div class="column">
        <h2 class="ui teal header">Performance of default miner settings vs pdazzl’s suggested variants.</h2>
        <p>Tests of the default sieve-size (33554432) and sieve-primes (900000) values versus (i.e. immediately followed by) pdazzl’s proposed parameter variants of sieve-size and sieve-primes over a specific range of shifts.</p>
      </div>
    </div> <!-- /row -->
  </div>
</div>


{% include paramtest.html %}

