---
layout: post
author: Graham Higgins
title: "How shift setting determines the number of digits in the primes to be searched"
description: From the bitcointalk ANN, back in 2014 ...
date: 2021-03-16
category: mining
tags:
---





**Q. Why does specifying a shift of 25 result in the miner using an 85-digit prime?**

**A. (From J0nn9) “`256 + shift` is the bit size of the prime you are searching for. The shift size
has to be greater than 13.”**

In using the phrase “the bit size of the prime”, he is referencing *bits* and *bytes* of
information.


## Bits and bytes

One “bit” of information is 0 or 1. This is the smallest piece of storable
information. “bit” is short for ”binary digit” and can store two states: off or
on, 0 or 1, false or true.

One “byte” of information is defined as 8 bits. So 256 bits is 32 bytes in the
same way that 2500 millimeters is 2.5 meters. A byte can represent any
combination of 0s and 1s between 00000000 and 11111111 and all stations
in-between e.g. 00001111, 10101010, 01010101, 00110100.

This combination can be more readably expressed in hexadecimal. 0x00 (0 in
decimal) represents 00000000, 0xff (256 in decimal) represents 11111111 and, as
examples of the stations in-between: 0xf0 (240 in decimal) represents 11110000
and 0x0f (16 in decimal) represents 00001111.

(I'm following standard practice by denoting a hexadecimal representation by the
leading pair of “0x” characters)

So the 256 bits of the “bit size of the prime” would be written out in full as:

    000000000000000000000000000000000000000000000000000000000000000000000000000000
    000000000000000000000000000000000000000000000000000000000000000000000000000000
    000000000000000000000000000000000000000000000000000000000000000000000000000000
    0000000000000000000000

or

    111111111111111111111111111111111111111111111111111111111111111111111111111111
    111111111111111111111111111111111111111111111111111111111111111111111111111111
    111111111111111111111111111111111111111111111111111111111111111111111111111111
    1111111111111111111111

and (just one example of) all stations in-between:

    010101010101010101010101010101010101010101010101010101010101010101010101010101
    010101010101010101010101010101010101010101010101010101010101010101010101010101
    010101010101010101010101010101010101010101010101010101010101010101010101010101
    0101010101010101010101

The same 256 bits expressed in hexadecimal representation is less unwieldy.

    0x0000000000000000000000000000000000000000000000000000000000000000

or

    0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff

and stations in-between

    0xf8f8f8f8f8f8f8f8f8f8f8f8f8f8f8f8f8f8f8f8f8f8f8f8f8f8f8f8f8f8f8f8

And so the hexadecimal representation is generally preferred --- and
supported so I’ll be using for preference in the next section of this
explainer

...

---

## Bit size and “shift”

You’ll likely be aware that digital computers use bits (0s and 1s) to represent
numbers.

The Python programming language offers a readable way of playing with bits,
bytes and numerical representations, including hexadecimal.

If I feed my Python interpreter with a hexadecimal number, it tells me what that
number is in decimal.

I can feed it the hexadecimal for 256 bits, all set to 1:

```python
>>> 0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff
115792089237316195423570985008687907853269984665640564039457584007913129639935
```

And I can ask it how many digits are in that decimal number:

```python
>>> len("115792089237316195423570985008687907853269984665640564039457584007913129639935")
78
```

Given J0nn9’s reply of “`256 + shift` is the bit size of the prime” ...

We can try this with a shift of *25*, making the bit size *256 + 25* which totals *281*.

*281* bits expressed in hexadecmal is:

    0x00000000000000000000000000000000000000000000000000000000000000000000000

(as opposed to the *256* bits of):

    0x0000000000000000000000000000000000000000000000000000000000000000

Python’s quite good for throwing numbers around. It can readily turn sequences
of strings of “1”s and “0”s into numbers.

Here's an example of it printing out the decimal representation of the byte
`11111111` (hexadecimal `0xff`):

```python
>> print(int('11111111', 2)) # parse the string '11111111' as an integer with base 2
255
>>> print(hex(int('11111111', 2)))
0xff
```

Handily, Python has a shorthand that allows one to print a string several times,
e.g. 32 “1”s:

```python
>>> print("1"*32)
11111111111111111111111111111111
```

This shorthand can be used with the previous explict bit string of '11111111' (eight “1”s)

```python
>>> print(int('1'*8, 2))
255
```

Now, we we can use this shorthand to print out the new bit size of 281 “1”s

```python
>> print(int('1'*281, 2))
3885337784451458141838923813647037813284813678104279042503624819477808570410416996351
```

So, how many digits in *that* number?

```python
>>> len("3885337784451458141838923813647037813284813678104279042503624819477808570410416996351")
85
```

And there you have the numbers that lie behind J0nn9's statement:

    “`256 + shift` is the bit size of the prime you are searching for”

Using a shift of *25* means a bit size of *256 + 25* (= *281*) which results in Gapcoin searching
for gaps between *85*-digit primes.

---

## Shifts and bit sizes

To find the length of the prime for a *specific* shift, we can use a variable.

Rather than the usual but cryptic `x`, we can use a more descriptive variable name: `SHIFT` ...

```python
print(len(str(int('1'*(256+SHIFT),2))))
```

And by assigning different values to `SHIFT`, we can get a sense of its
impact on the length of the primes to be searched.

.
.
.


A shift of *25* will result in primes with *85* digits

```python
>>> SHIFT = 25
>>> print(len(str(int('1'*(256+SHIFT),2))))
85
```

A shift of *128* will result in primes with *116* digits

```python
>>> SHIFT = 128
>>> print(len(str(int('1'*(256+SHIFT),2))))
116
```

The allowed minimum shift of *13* results in *81*-digit primes

```python
>>> SHIFT = 13
>>> print(len(str(int('1'*(256+SHIFT),2))))
81
```

The default shift of *25* (as [encoded in the Gapcoin C++ source](https://github.com/gapcoin/gapcoin/blob/9a2991f83c60a996e351ef73f02b281ee4ee14d0/src/miner.cpp#L367) and [in the GapMiner source](https://github.com/gapcoin/GapMiner/blob/2f66e908e52dab503de77835f31ac1603b1c23fc/src/main.cpp#L310)) results in *85*-digit primes

```python
>>> SHIFT = 25
>>> print(len(str(int('1'*(256+SHIFT),2))))
85
```

(So by default Gapcoin searches for gaps between 85-digit primes and that is
why there’s such a strong concentration of Gapcoin-discovered gaps in
[Seth Troisi’s end-of-2020 graph](/news/2021/03/13/state-of-play-end-2020/)
of prime-length vs gap coverage.)

---

## Upper limits

Back in 2014, J0nn9 observed: “shift can theoretically be in range `[14, 2^16]`,
but nodes can choose to only accept shifts till a given amount (e.g. 512 for the
main nodes)”

However, this upper limit of 512 was [later increased](https://github.com/gapcoin/Gapcoin-PoWCore/commit/ca5e863b1ff6c0a9655fadb951f1d9653ba24ef1#diff-db91942ad84e196dde1256bf1cb1cf7670c56c824acd40b5a9adfab8744352a4) to *1024*.

```python
>>> SHIFT = 1024
>>> print(len(str(int('1'*(256+SHIFT),2))))
386
```

A 386-digit prime is quite a large number:

    1983423893055277343771839442553463759456121569397634422513819961
    1507538399093415101489223407213551698761866068732737252027269776
    7154619951173536174717936999718490306477336080747887166904476954
    8319471533223333475285033669837852384808841224768815857595158432
    1880080025074484205788751028980294739160978233965869789764051556
    5099862840015057267339368918911954021678927068721903471912239965
    89

According to wikipedia¹, a septillion is only 25 digits long.

Even a Millinillion² at 10^3003 is “only” 3004 digits in length:

```python
>> pow(10, 3003)
100000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
000000000000000000000000000000000000000000000000000000000000000000000
0000000000000000000000000000000000000
```

Using the maximum shift of 2^16 gets you into the serious territory of
primes with nearly 20,000 digits, waaay bigger even than millinillions
(millinillimillinillinillions?)

```python
>>> SHIFT = pow(2, 16)
>>> print(len(str(int('1'*(256+SHIFT),2))))
19806
```

Primes of this length aren’t suitable for using as the basis of a
Proof-Of-Work algorithm for a cryptocurrency because the computational work
of just checking the PoW of such a large prime may well act as a
denial-of-service attack on the chain.

---

## Shifts and mining

Below is a small Python routine that shows the corresponding prime lengths
for each of the shifts:

```python
>>> [len(str(int('1'*(256+SHIFT),2))) for SHIFT in range(15, 155, 10)]
[82, 85, 88, 91, 94, 97, 100, 103, 106, 109, 112, 115, 118, 121]
```

The example below is the result of a couple of limited tests of the Gapcoin cpuminer running on a Dell XPS 9569 i7 laptop at shifts of 32 and 64 with the default sieve-size and sieve-primes settings:

    --threads 1 --shift 32 --sieve-size 33554432 --sieve-primes 900000 -j 5 -e 

    [2021-03-19 14:21:32] pps: 219195 / 219631  tests/s 69867 / 70749  gaps/s 10378 / 10405
    [2021-03-19 14:21:37] pps: 216931 / 219515  tests/s 70140 / 70821  gaps/s 10278 / 10400
    [2021-03-19 14:21:42] pps: 220776 / 214989  tests/s 71526 / 69464  gaps/s 10460 / 10185
    [2021-03-19 14:21:47] pps: 215538 / 215627  tests/s 69858 / 69744  gaps/s 10213 / 10216
    [2021-03-19 14:21:52] pps: 221439 / 215644  tests/s 71773 / 69772  gaps/s 10493 / 10217
    [2021-03-19 14:21:57] pps: 217258 / 215948  tests/s 69879 / 69817  gaps/s 10289 / 10231
    [2021-03-19 14:22:02] pps: 218976 / 216395  tests/s 70417 / 69922  gaps/s 10373 / 10252
    [2021-03-19 14:22:07] pps: 218754 / 216557  tests/s 71559 / 69962  gaps/s 10369 / 10260
    [2021-03-19 14:22:12] pps: 221418 / 216953  tests/s 70514 / 70076  gaps/s 10482 / 10278
    [2021-03-19 14:22:17] pps: 224622 / 217301  tests/s 72134 / 70189  gaps/s 10639 / 10295
    [2021-03-19 14:22:22] pps: 220063 / 217468  tests/s 70087 / 70237  gaps/s 10418 / 10303
    [2021-03-19 14:22:27] pps: 219848 / 217685  tests/s 71645 / 70293  gaps/s 10420 / 10313
    [2021-03-19 14:22:32] pps: 219698 / 217660  tests/s 71050 / 70293  gaps/s 10408 / 10312
    [2021-03-19 14:22:37] pps: 213912 / 217468  tests/s 68960 / 70231  gaps/s 10130 / 10303

    --threads 1 --shift 64 --sieve-size 33554432 --sieve-primes 900000 -j 5 -e 

    [2021-03-19 14:20:03] pps: 166291 / 169551  tests/s 60031 / 60985  gaps/s 7879 / 8032
    [2021-03-19 14:20:08] pps: 165653 / 170272  tests/s 59199 / 60846  gaps/s 7846 / 8065
    [2021-03-19 14:20:13] pps: 168338 / 166193  tests/s 60731 / 59428  gaps/s 7977 / 7873
    [2021-03-19 14:20:18] pps: 172167 / 168326  tests/s 61802 / 60242  gaps/s 8157 / 7975
    [2021-03-19 14:20:23] pps: 177640 / 168989  tests/s 63981 / 60495  gaps/s 8422 / 8006
    [2021-03-19 14:20:28] pps: 170073 / 169990  tests/s 60453 / 60750  gaps/s 8057 / 8054
    [2021-03-19 14:20:33] pps: 168925 / 170474  tests/s 60395 / 60966  gaps/s 8004 / 8077
    [2021-03-19 14:20:38] pps: 172555 / 168662  tests/s 61492 / 60348  gaps/s 8173 / 7991
    [2021-03-19 14:20:43] pps: 179819 / 169214  tests/s 63995 / 60563  gaps/s 8519 / 8018
    [2021-03-19 14:20:48] pps: 181478 / 169949  tests/s 64944 / 60849  gaps/s 8599 / 8053
    [2021-03-19 14:20:53] pps: 178819 / 170347  tests/s 64278 / 60963  gaps/s 8475 / 8072
    [2021-03-19 14:20:58] pps: 177222 / 170397  tests/s 62913 / 60981  gaps/s 8393 / 8074
    [2021-03-19 14:21:03] pps: 170860 / 170240  tests/s 62286 / 60969  gaps/s 8103 / 8067


¹ Wikpedia [Names of large numbers](https://en.wikipedia.org/wiki/Names_of_large_numbers)

² Stewart, Ian (2017). [Infinity: A Very Short Introduction](https://books.google.com/books?id=iewwDgAAQBAJ) (illustrated ed.). Oxford University Press. p. 20. [Extract of Page 20](https://books.google.com/books?id=iewwDgAAQBAJ&pg=PA20)
