---
layout: post
author: BitcoinFX
title: Creating Chinese Remainder Theorem (crt) files
description: HOW-TO use GapMiner to create optimised crt files
date: 2021-02-01
category: crtmining
tags: reference
---

## Creating Chinese Remainder Theorem (crt) files

The ctr algorithm is divided into 2 parts. The first part is a simple greedy algorithm which tries to find offsets for each involved prime so that the desired number range has the least prime candidates as possible.

The second part is an evolutionary algorithm which tries to improve the results from the greedy algorithm. Therefore the greedy algorithm will be executed several times with slightly different parameters to produce ctrs which differ in quality which than can be used by the evolutionary algorithm.

The output is a text file which can be used by gapminer as an input for ctr sieving.

```none
Parameter description:

--calc-ctr          Indicates that we want to calculate a ctr file.

--ctr-strength      This is used to vary the computing time spent
                    within the greedy algorithm. Higher strength
                    can yield better results.

--ctr-primes        The number of primes to use in the ctr file. The more
                    primes the better the ctr result but the shift
                    also increases. Minimum shift can be calculated as 
                    the binary logarithm of the product of all primes:
                    log2(p1 * p2 * ... *pn).

--ctr-evolution     Whether to use the evolutionary algorithm or not.

--ctr-fixed         This number indicates the number of starting primes
                    which would get touched by the evolutionary algorithm
                    the offsets for the primes 2,3,5,7,11... are mostly
                    perfect computed by the greedy algorithm and changing
                    them only declines the result.

--ctr-ivs           The number of individuals used in the evolutionary algorithm.
                    More increases computing time but mostly also the 
                    result quality.

--ctr-range         Percent deviation from the number of primes.
                    Useful if you don't want to look for a specific number 
                    of primes.

--ctr-bits -256     The shift value you later use for sieving has to be greater
                    than log2(p1*p2*..*pn). With this flag you can fine-tune a specific
                    shift by setting this to shift - log2(p1*p2*..*pn).

--ctr-merit         The target merit (while testing the ctr it seemed that 
                    sieving for target-merit - 1 yields the best results)

--ctr-file          The target ctr output file. You can open this with a 
                    text editor. Look for the n_candidates value, the smaller
                    it is the better the ctr file.
```

## Calculating crt-bits:

In a j0nn9 [post to bitcointalk](https://bitcointalk.org/index.php?topic=822498.msg11816902#msg11816902)...

<blockquote>
  <p>If you want to generate a file for, e.g. shift 384 with <tt>ctr-primes = 58</tt></p>

  <code><pre style="font-size:90%">ctr-bits = <math>shift - log2(p1*p2*..*pn)</math></pre></code>

  <p>Or, expressed using <a href="https://en.wikipedia.org/wiki/Primorial" target="_blank">primorial notation</a>:</p>

  <code><pre style="font-size:90%">
ctr-bits = <math>384 - log2(58#)</math>

ctr-bits = <math>384 - 368 = 16</math></pre></code>
</blockquote>

*Achieving the above using Python 3*

```python
from sympy import primorial
>>> from math import log2
>>> log2(primorial(58))
367.0750275397664
```

<h4 class="ui horizontal divider teal header"><i class="cogs icon"></i></h4>

For specific settings used to calculate the set of crt files, see:

- [Settings used to create the standard set of 22m crt files]() as originally created by j0nn9 2015-04-04

- [Settings used to create the standard set of 22m crt files]() as originally created by j0nn9 2015-04-04
