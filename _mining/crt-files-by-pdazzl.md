---
layout: post
author: Graham Higgins
title: Specific Chinese Remainder Theorem crt files contributed by pdazzl
description: Selected crt files published by pdazzl on bitcointalk
date: 2021-02-04
category: crtmining
tags: reference
---

## Selected crt optimisation files for shift 416, 479, 512 and 1024, as published by [pdazzl](https://bitcointalk.org/index.php?action=profile;u=470347)

***Note*** - values for the `offset` field have been broken into shorter pieces for presentational purposes, either edit them back into a single unbroken line or *use the download link to retrieve an unedited version*. 


<h4 class="ui horizontal divider teal header"><i class="cogs icon"></i></h4>


### Shift 416

```bash
-t 8 -f 416 -i 13000 -d 6 -r crt/crt-22m-416s.txt
```
<a href="/static-data/crt-22m-0416s-pdazzl.txt" target="_blank"><i class="dolly icon"></i> <tt>crt-22m-0416s.txt</tt></a>

```none
|== ChineseSet ==|
n_primes:     62
size:         10242
n_candidates: 765
offset:       1146441612406461563657892639195504712824084356280432767521872923
              137076875201036461817017569202830059679582232394065759000</pre>
```


### Shift 479

```bash
-t 8 -f 479 -i 13000 -d 6 -r crt/crt-22m-480s.txt
```

<a href="/static-data/crt-22m-0480s-pdazzl.txt" target="_blank"><i class="dolly icon"></i> <tt>crt-22m-480s-dif22084c.txt</tt></a>

```none
|== ChineseSet ==|
n_primes:     70
size:         11058
n_candidates: 769
offset:       1476535438052344808249114914435996661778930746178207307948586337728699041748900
69973599252984037935841114047624491809544987485395054755413948</pre>
```

### Shift 512

```bash
-t 8 -f 511 -i 13000 -d 6 -r crt/crt-22m-512s.txt
```

<a href="/static-data/crt-22m-0512s-pdazzl.txt" target="_blank"><i class="dolly icon"></i> <tt>crt-22m-0512s.txt</tt></a>

```none
|== ChineseSet ==|
  n_primes:     74
  size:         11319
  n_candidates: 766
  offset:       13367585452126639104917704816714921555816311173860045616400049444
  7292353448190019244690512990951578355363092990034085565298376116749903009975197
  7773980
```

### Shift 1024

If anyone wants to go after the 1020-1024 range here is my best customized sieve file. Strange thing is Gapcoin seems to not record about 15-20% of found blocks for these much higher shifts for some reason, not sure if it's a bug or something else.  Anyways if you’re more interested in setting a bunch of new records than getting more coins and have the cpus available then this should do you well.

```bash
-t 8 -f 1021 -i 23000 -d 6 -r crt/crt-22m-1024s.txt
```
<a href="/static-data/crt-22m-1024s-pdazzl.txt" target="_blank"><i class="dolly icon"></i> <tt>crt-22m-1024s.txt</tt></a>

```none
|== ChineseSet ==|
n_primes:     130
size:         18863
n_candidates: 1039
offset:       4626081985258152152387146716381104236401743138963348264823465389447497680671113 
1850105279036924603869257530367004081634142637510553687550996988149393864286408 
0741632575037157518785072850028569785866506191383414969297175673797072420119844 
8403639569393650350154418384633294148378069691014056008325991106608
```
<h4 class="ui horizontal divider teal header"><i class="cogs icon"></i></h4>

Doing some more performance testing, here’s another one that appears to yield good results if someone wants to try it out.

```bash
-t 8 --shift 508 --crt crt/crt-22m-512s.txt --fermat-threads 7 --sieve-primes 10000
```

It’s a very low number of primes to sieve with but results in generating a LOT of candidate gaps in the gaplist.  The gaplist grows by 50000 every 10 seconds.  But the block percentage goes up very quickly.  The reason I think it does is because of j0nn9’s algo picking the best candidate gaps from a bigger applicant pool in the heap and thus yielding block solving gaps more quickly.

You’ll want to monitor your memory usage for a couple rounds at first, the high watermark for the above arguments on my machine is about 2.6Gb of RAM so you'll want to make sure you’re not too close to maxing out your memory.