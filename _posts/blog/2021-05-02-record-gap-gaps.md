---
layout: post
author: Graham Higgins
title: Record gaps, in a different sense
description: Submitted record gaps by prime digit length and shift 
date: 2021-05-02
category: gapcoin
tags: post
---


## Patchy coverage in the Prime Gap List

Some trivial SQL exploration of the prime gap list records SQL file [available from the Prime Gap List repository](https://github.com/primegap-list-project/prime-gap-list/blob/server/allgaps.sql) reveals interesting differences in depth of exploration of prime digit length ranges. Below is a short list of a range of prime digit lengths covering the shift ranges from 16 to 128 and a COUNT of the first known occurrence gaps recorded for that range:

```nohighlight
 82: 100,   83:010,   84:012,    85:264,   86:04,     87:053,    88:001,    89:003, 
 90: 001,   91:008,   92:000,    93:006,   94:014,    95:018,    96:010,    97:206, 
 98: 005,   99:016,  100:016,   101:002,  102:012,   103:007,   104:013,   105:015,
106: 121,  107:016,  108:010,   109:015,  110:021,   111:012,   112:034,   113:026,
114: 049,  115:023,  116:142
```

So, while there have been 100 record gaps submitted for the range of primes with length 82, only *one* record has been submitted for the range of primes with length 88 and for the range of primes with length 90. Interestingly, *no records at all* have been discovered and submitted for the range of primes of length 92.

![Submitted records by prime digit length](/img/blog/submitted_records_by_primedigitlength.png)


There is an obvious correspondence between the number of records discovered/submitted and the popular/default Gapcoin shift settings - 16 was the original default setting for GapMiner, later increased to 25 and then there are the popular multiples of 16: 32, 64, 96 and 128:

![Submitted records by shift](/img/blog/submitted_records_by_shift.png)

