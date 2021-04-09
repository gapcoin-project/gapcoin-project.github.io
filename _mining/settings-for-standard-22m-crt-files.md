---
layout: post
author: BitcoinFX
title: GapMiner settings for creating the standard set of crt files
description: Settings used by j0nn9 for create the standard set of crt files
date: 2021-02--2
category: crtmining
tags: reference
---


## Settings which were used to calculate [the crt files in the GapMiner repository](https://github.com/gapcoin-project/GapMiner/tree/master/crt)


(Posted by BitcoinFX to [bitcointalk](https://bitcointalk.org/index.php?topic=822498.msg49404402#msg49404402) on 2019-01-24)

Miner call and invariant setting:

```
-t 4 --calc-ctr --ctr-evolution --ctr-strength 150000 --ctr-ivs 1000 --ctr-range 0 --ctr-merit 22
```

```none
--ctr-fixed  8 --ctr-bits 10 --ctr-primes 14  --ctr-file crt-22m-0064s.txt
--ctr-fixed  8 --ctr-bits 13 --ctr-primes 19  --ctr-file crt-22m-0096s.txt
--ctr-fixed 10 --ctr-bits 13 --ctr-primes 24  --ctr-file crt-22m-0128s.txt
--ctr-fixed 10 --ctr-bits 12 --ctr-primes 29  --ctr-file crt-22m-0160s.txt
--ctr-fixed 11 --ctr-bits  9 --ctr-primes 34  --ctr-file crt-22m-0192s.txt
--ctr-fixed 11 --ctr-bits 12 --ctr-primes 38  --ctr-file crt-22m-0224s.txt
--ctr-fixed 11 --ctr-bits 14 --ctr-primes 42  --ctr-file crt-22m-0256s.txt
--ctr-fixed 11 --ctr-bits 15 --ctr-primes 46  --ctr-file crt-22m-0288s.txt
--ctr-fixed 12 --ctr-bits 16 --ctr-primes 50  --ctr-file crt-22m-0320s.txt
--ctr-fixed 12 --ctr-bits  9 --ctr-primes 55  --ctr-file crt-22m-0352s.txt
--ctr-fixed 12 --ctr-bits 16 --ctr-primes 58  --ctr-file crt-22m-0384s.txt
--ctr-fixed 12 --ctr-bits 16 --ctr-primes 62  --ctr-file crt-22m-0416s.txt
--ctr-fixed 12 --ctr-bits 15 --ctr-primes 66  --ctr-file crt-22m-0448s.txt
--ctr-fixed 12 --ctr-bits 13 --ctr-primes 70  --ctr-file crt-22m-0480s.txt
--ctr-fixed 13 --ctr-bits 11 --ctr-primes 74  --ctr-file crt-22m-0512s.txt
--ctr-fixed 13 --ctr-bits  9 --ctr-primes 78  --ctr-file crt-22m-0544s.txt
--ctr-fixed 13 --ctr-bits 15 --ctr-primes 81  --ctr-file crt-22m-0576s.txt
--ctr-fixed 13 --ctr-bits 12 --ctr-primes 85  --ctr-file crt-22m-0608s.txt
--ctr-fixed 13 --ctr-bits 17 --ctr-primes 88  --ctr-file crt-22m-0640s.txt
--ctr-fixed 13 --ctr-bits 14 --ctr-primes 92  --ctr-file crt-22m-0672s.txt
--ctr-fixed 14 --ctr-bits 10 --ctr-primes 96  --ctr-file crt-22m-0704s.txt
--ctr-fixed 14 --ctr-bits 15 --ctr-primes 99  --ctr-file crt-22m-0736s.txt
--ctr-fixed 14 --ctr-bits 10 --ctr-primes 103 --ctr-file crt-22m-0768s.txt
--ctr-fixed 14 --ctr-bits 15 --ctr-primes 106 --ctr-file crt-22m-0800s.txt
--ctr-fixed 14 --ctr-bits 10 --ctr-primes 110 --ctr-file crt-22m-0832s.txt
--ctr-fixed 14 --ctr-bits 14 --ctr-primes 113 --ctr-file crt-22m-0864s.txt
--ctr-fixed 14 --ctr-bits  9 --ctr-primes 117 --ctr-file crt-22m-0896s.txt
--ctr-fixed 15 --ctr-bits 13 --ctr-primes 120 --ctr-file crt-22m-0928s.txt
--ctr-fixed 15 --ctr-bits 17 --ctr-primes 122 --ctr-file my-crt-file.txt
--ctr-fixed 15 --ctr-bits 11 --ctr-primes 127 --ctr-file crt-22m-0992s.txt
--ctr-fixed 15 --ctr-bits 15 --ctr-primes 130 --ctr-file crt-22m-1024s.txt
```

*Note:* Although `--ctr-primes 122` is included in the above listing, there is no corresponding crt text file in the original [GapMiner source code repository](https://github.com/gapcoin/GapMiner/tree/master/crt)

