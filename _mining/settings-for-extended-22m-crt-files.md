---
layout: post
author: Wizz, edited by Graham Higgins
title: GapMiner settings for creating Wizz’ extended range of crt files
description: Settings used by Wizz to create the extended set of 22m crt files
date: 2021-02-03
category: crtmining
tags: reference
---

## Settings used by Wizz to create the extended set of 22m crt files.

Below are listed the settings which were used to calculate Wizz’ contributed [extended set of 22m ctr](https://github.com/wizz13150/GapcoinStuff/tree/main/crtwizz/crtwizz-m22) files. 

For tuning, you *can* change the values for `--ctr-strength`, `--ctr-merit`, `--ctr-ivs`, `--ctr-range`, `-t` and `--ctr-file`.

But **don’t** change `--ctr-fixed` or `--ctr-bits`.

Miner call and invariant setting:

```bash
-t 15 --calc-ctr  --ctr-evolution --ctr-strength 150000 --ctr-merit 22 --ctr-ivs 1000 --ctr-range 0
```

```none
--ctr-fixed  8 --ctr-bits 10 --ctr-primes  14 --ctr-file crt-file-m22-s0064.txt
--ctr-fixed  8 --ctr-bits 11 --ctr-primes  15 --ctr-file crt-file-m22-s0070.txt
--ctr-fixed  8 --ctr-bits 12 --ctr-primes  16 --ctr-file crt-file-m22-s0077.txt
--ctr-fixed  8 --ctr-bits 12 --ctr-primes  17 --ctr-file crt-file-m22-s0083.txt
--ctr-fixed  8 --ctr-bits 13 --ctr-primes  18 --ctr-file crt-file-m22-s0090.txt
--ctr-fixed  8 --ctr-bits 14 --ctr-primes  19 --ctr-file crt-file-m22-s0096.txt
--ctr-fixed  8 --ctr-bits 13 --ctr-primes  20 --ctr-file crt-file-m22-s0102.txt
--ctr-fixed  8 --ctr-bits 14 --ctr-primes  21 --ctr-file crt-file-m22-s0109.txt
--ctr-fixed  8 --ctr-bits 14 --ctr-primes  22 --ctr-file crt-file-m22-s0115.txt
--ctr-fixed  8 --ctr-bits 14 --ctr-primes  23 --ctr-file crt-file-m22-s0122.txt
--ctr-fixed 10 --ctr-bits 13 --ctr-primes  24 --ctr-file crt-file-m22-s0128.txt
--ctr-fixed 10 --ctr-bits 13 --ctr-primes  25 --ctr-file crt-file-m22-s0134.txt
--ctr-fixed 10 --ctr-bits 13 --ctr-primes  26 --ctr-file crt-file-m22-s0141.txt
--ctr-fixed 10 --ctr-bits 13 --ctr-primes  27 --ctr-file crt-file-m22-s0147.txt
--ctr-fixed 10 --ctr-bits 13 --ctr-primes  28 --ctr-file crt-file-m22-s0154.txt
--ctr-fixed 10 --ctr-bits 12 --ctr-primes  29 --ctr-file crt-file-m22-s0160.txt
--ctr-fixed 10 --ctr-bits 11 --ctr-primes  30 --ctr-file crt-file-m22-s0166.txt
--ctr-fixed 10 --ctr-bits 11 --ctr-primes  31 --ctr-file crt-file-m22-s0173.txt
--ctr-fixed 10 --ctr-bits 10 --ctr-primes  32 --ctr-file crt-file-m22-s0179.txt
--ctr-fixed 10 --ctr-bits 10 --ctr-primes  33 --ctr-file crt-file-m22-s0186.txt
--ctr-fixed 11 --ctr-bits  9 --ctr-primes  34 --ctr-file crt-file-m22-s0192.txt
--ctr-fixed 11 --ctr-bits 10 --ctr-primes  35 --ctr-file crt-file-m22-s0200.txt
--ctr-fixed 11 --ctr-bits 11 --ctr-primes  36 --ctr-file crt-file-m22-s0208.txt
--ctr-fixed 11 --ctr-bits 11 --ctr-primes  37 --ctr-file crt-file-m22-s0216.txt
--ctr-fixed 11 --ctr-bits 12 --ctr-primes  38 --ctr-file crt-file-m22-s0224.txt
--ctr-fixed 11 --ctr-bits 13 --ctr-primes  39 --ctr-file crt-file-m22-s0232.txt
--ctr-fixed 11 --ctr-bits 13 --ctr-primes  40 --ctr-file crt-file-m22-s0240.txt
--ctr-fixed 11 --ctr-bits 14 --ctr-primes  41 --ctr-file crt-file-m22-s0248.txt
--ctr-fixed 11 --ctr-bits 14 --ctr-primes  42 --ctr-file crt-file-m22-s0256.txt
--ctr-fixed 11 --ctr-bits 15 --ctr-primes  43 --ctr-file crt-file-m22-s0264.txt
--ctr-fixed 11 --ctr-bits 15 --ctr-primes  44 --ctr-file crt-file-m22-s0272.txt
--ctr-fixed 11 --ctr-bits 16 --ctr-primes  45 --ctr-file crt-file-m22-s0280.txt
--ctr-fixed 11 --ctr-bits 15 --ctr-primes  46 --ctr-file crt-file-m22-s0288.txt
--ctr-fixed 11 --ctr-bits 16 --ctr-primes  47 --ctr-file crt-file-m22-s0296.txt
--ctr-fixed 11 --ctr-bits 16 --ctr-primes  48 --ctr-file crt-file-m22-s0304.txt
--ctr-fixed 11 --ctr-bits 17 --ctr-primes  49 --ctr-file crt-file-m22-s0312.txt
--ctr-fixed 12 --ctr-bits 16 --ctr-primes  50 --ctr-file crt-file-m22-s0320.txt
--ctr-fixed 12 --ctr-bits 15 --ctr-primes  51 --ctr-file crt-file-m22-s0326.txt
--ctr-fixed 12 --ctr-bits 14 --ctr-primes  52 --ctr-file crt-file-m22-s0333.txt
--ctr-fixed 12 --ctr-bits 12 --ctr-primes  53 --ctr-file crt-file-m22-s0339.txt
--ctr-fixed 12 --ctr-bits 11 --ctr-primes  54 --ctr-file crt-file-m22-s0346.txt
--ctr-fixed 12 --ctr-bits  9 --ctr-primes  55 --ctr-file crt-file-m22-s0352.txt
--ctr-fixed 12 --ctr-bits 11 --ctr-primes  56 --ctr-file crt-file-m22-s0362.txt
--ctr-fixed 12 --ctr-bits 14 --ctr-primes  57 --ctr-file crt-file-m22-s0373.txt
--ctr-fixed 12 --ctr-bits 16 --ctr-primes  58 --ctr-file crt-file-m22-s0384.txt
--ctr-fixed 12 --ctr-bits 17 --ctr-primes  59 --ctr-file crt-file-m22-s0392.txt
--ctr-fixed 12 --ctr-bits 17 --ctr-primes  60 --ctr-file crt-file-m22-s0400.txt
--ctr-fixed 12 --ctr-bits 16 --ctr-primes  61 --ctr-file crt-file-m22-s0408.txt
--ctr-fixed 12 --ctr-bits 16 --ctr-primes  62 --ctr-file crt-file-m22-s0416.txt
--ctr-fixed 12 --ctr-bits 16 --ctr-primes  63 --ctr-file crt-file-m22-s0424.txt
--ctr-fixed 12 --ctr-bits 16 --ctr-primes  64 --ctr-file crt-file-m22-s0432.txt
--ctr-fixed 12 --ctr-bits 16 --ctr-primes  65 --ctr-file crt-file-m22-s0440.txt
--ctr-fixed 12 --ctr-bits 15 --ctr-primes  66 --ctr-file crt-file-m22-s0448.txt
--ctr-fixed 12 --ctr-bits 15 --ctr-primes  67 --ctr-file crt-file-m22-s0456.txt
--ctr-fixed 12 --ctr-bits 14 --ctr-primes  68 --ctr-file crt-file-m22-s0464.txt
--ctr-fixed 12 --ctr-bits 14 --ctr-primes  69 --ctr-file crt-file-m22-s0472.txt
--ctr-fixed 12 --ctr-bits 14 --ctr-primes  70 --ctr-file crt-file-m22-s0480.txt
--ctr-fixed 12 --ctr-bits 13 --ctr-primes  71 --ctr-file crt-file-m22-s0488.txt
--ctr-fixed 12 --ctr-bits 13 --ctr-primes  72 --ctr-file crt-file-m22-s0496.txt
--ctr-fixed 12 --ctr-bits 12 --ctr-primes  73 --ctr-file crt-file-m22-s0504.txt
--ctr-fixed 13 --ctr-bits 11 --ctr-primes  74 --ctr-file crt-file-m22-s0512.txt
--ctr-fixed 13 --ctr-bits 11 --ctr-primes  75 --ctr-file crt-file-m22-s0520.txt
--ctr-fixed 13 --ctr-bits 10 --ctr-primes  76 --ctr-file crt-file-m22-s0528.txt
--ctr-fixed 13 --ctr-bits 10 --ctr-primes  77 --ctr-file crt-file-m22-s0536.txt
--ctr-fixed 13 --ctr-bits  9 --ctr-primes  78 --ctr-file crt-file-m22-s0544.txt
--ctr-fixed 13 --ctr-bits 11 --ctr-primes  79 --ctr-file crt-file-m22-s0555.txt
--ctr-fixed 13 --ctr-bits 13 --ctr-primes  80 --ctr-file crt-file-m22-s0565.txt
--ctr-fixed 13 --ctr-bits 15 --ctr-primes  81 --ctr-file crt-file-m22-s0576.txt
--ctr-fixed 13 --ctr-bits 14 --ctr-primes  82 --ctr-file crt-file-m22-s0584.txt
--ctr-fixed 13 --ctr-bits 14 --ctr-primes  83 --ctr-file crt-file-m22-s0592.txt
--ctr-fixed 13 --ctr-bits 13 --ctr-primes  84 --ctr-file crt-file-m22-s0600.txt
--ctr-fixed 13 --ctr-bits 12 --ctr-primes  85 --ctr-file crt-file-m22-s0608.txt
--ctr-fixed 13 --ctr-bits 14 --ctr-primes  86 --ctr-file crt-file-m22-s0619.txt
--ctr-fixed 13 --ctr-bits 16 --ctr-primes  87 --ctr-file crt-file-m22-s0629.txt
--ctr-fixed 13 --ctr-bits 17 --ctr-primes  88 --ctr-file crt-file-m22-s0640.txt
--ctr-fixed 13 --ctr-bits 17 --ctr-primes  89 --ctr-file crt-file-m22-s0648.txt
--ctr-fixed 13 --ctr-bits 16 --ctr-primes  90 --ctr-file crt-file-m22-s0656.txt
--ctr-fixed 13 --ctr-bits 15 --ctr-primes  91 --ctr-file crt-file-m22-s0664.txt
--ctr-fixed 13 --ctr-bits 14 --ctr-primes  92 --ctr-file crt-file-m22-s0672.txt
--ctr-fixed 13 --ctr-bits 13 --ctr-primes  93 --ctr-file crt-file-m22-s0680.txt
--ctr-fixed 13 --ctr-bits 12 --ctr-primes  94 --ctr-file crt-file-m22-s0688.txt
--ctr-fixed 13 --ctr-bits 11 --ctr-primes  95 --ctr-file crt-file-m22-s0696.txt
--ctr-fixed 14 --ctr-bits 10 --ctr-primes  96 --ctr-file crt-file-m22-s0704.txt
--ctr-fixed 14 --ctr-bits 12 --ctr-primes  97 --ctr-file crt-file-m22-s0715.txt
--ctr-fixed 14 --ctr-bits 13 --ctr-primes  98 --ctr-file crt-file-m22-s0725.txt
--ctr-fixed 14 --ctr-bits 15 --ctr-primes  99 --ctr-file crt-file-m22-s0736.txt
--ctr-fixed 14 --ctr-bits 14 --ctr-primes 100 --ctr-file crt-file-m22-s0744.txt
--ctr-fixed 14 --ctr-bits 13 --ctr-primes 101 --ctr-file crt-file-m22-s0752.txt
--ctr-fixed 14 --ctr-bits 12 --ctr-primes 102 --ctr-file crt-file-m22-s0760.txt
--ctr-fixed 14 --ctr-bits 11 --ctr-primes 103 --ctr-file crt-file-m22-s0768.txt
--ctr-fixed 14 --ctr-bits 13 --ctr-primes 104 --ctr-file crt-file-m22-s0779.txt
--ctr-fixed 14 --ctr-bits 14 --ctr-primes 105 --ctr-file crt-file-m22-s0789.txt
--ctr-fixed 14 --ctr-bits 15 --ctr-primes 106 --ctr-file crt-file-m22-s0800.txt
--ctr-fixed 14 --ctr-bits 14 --ctr-primes 107 --ctr-file crt-file-m22-s0808.txt
--ctr-fixed 14 --ctr-bits 13 --ctr-primes 108 --ctr-file crt-file-m22-s0816.txt
--ctr-fixed 14 --ctr-bits 12 --ctr-primes 109 --ctr-file crt-file-m22-s0824.txt
--ctr-fixed 14 --ctr-bits 11 --ctr-primes 110 --ctr-file crt-file-m22-s0832.txt
--ctr-fixed 14 --ctr-bits 12 --ctr-primes 111 --ctr-file crt-file-m22-s0843.txt
--ctr-fixed 14 --ctr-bits 13 --ctr-primes 112 --ctr-file crt-file-m22-s0853.txt
--ctr-fixed 14 --ctr-bits 14 --ctr-primes 113 --ctr-file crt-file-m22-s0864.txt
--ctr-fixed 14 --ctr-bits 14 --ctr-primes 114 --ctr-file crt-file-m22-s0872.txt
--ctr-fixed 14 --ctr-bits 12 --ctr-primes 115 --ctr-file crt-file-m22-s0880.txt
--ctr-fixed 14 --ctr-bits 11 --ctr-primes 116 --ctr-file crt-file-m22-s0888.txt
--ctr-fixed 14 --ctr-bits 10 --ctr-primes 117 --ctr-file crt-file-m22-s0896.txt
--ctr-fixed 14 --ctr-bits 11 --ctr-primes 118 --ctr-file crt-file-m22-s0907.txt
--ctr-fixed 14 --ctr-bits 12 --ctr-primes 119 --ctr-file crt-file-m22-s0917.txt
--ctr-fixed 15 --ctr-bits 13 --ctr-primes 120 --ctr-file crt-file-m22-s0928.txt
--ctr-fixed 15 --ctr-bits 14 --ctr-primes 121 --ctr-file crt-file-m22-s0938.txt
--ctr-fixed 15 --ctr-bits 16 --ctr-primes 122 --ctr-file crt-file-m22-s0949.txt
--ctr-fixed 15 --ctr-bits 13 --ctr-primes 123 --ctr-file crt-file-m22-s0956.txt
--ctr-fixed 15 --ctr-bits 13 --ctr-primes 124 --ctr-file crt-file-m22-s0965.txt
--ctr-fixed 15 --ctr-bits 12 --ctr-primes 125 --ctr-file crt-file-m22-s0974.txt
--ctr-fixed 15 --ctr-bits 12 --ctr-primes 126 --ctr-file crt-file-m22-s0983.txt
--ctr-fixed 15 --ctr-bits 11 --ctr-primes 127 --ctr-file crt-file-m22-s0992.txt
--ctr-fixed 15 --ctr-bits 13 --ctr-primes 128 --ctr-file crt-file-m22-s1003.txt
--ctr-fixed 15 --ctr-bits 14 --ctr-primes 129 --ctr-file crt-file-m22-s1013.txt
--ctr-fixed 15 --ctr-bits 15 --ctr-primes 130 --ctr-file crt-file-m22-s1024.txt
```
