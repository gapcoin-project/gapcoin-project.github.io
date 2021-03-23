---
layout: page
title: About Gapcoin
description: 
---

### What is Gapcoin?

“Gapcoin is a prime number based P2P cryptocurrency, which eliminates some sticking points of other scientific currencies like Primecoin or [Riecoin](https://riecoin.dev/). It's a (code, *not* chain) ‘fork’ of Satoshi Nakamoto’s Bitcoin, a decentralized payment system which is independent of banks, governments and other centralized regulators. With Gapcoin, you can send money around the globe in seconds. The big improvement in comparison to Bitcoin is that instead of burning electricity for its own sake, Gapcoin’s Proof of Work function actually does useful work by searching for large [prime gaps](https://en.wikipedia.org/wiki/Prime_gap).”


#### Fair launch

“Gapcoin was not designed to enrich the early adopters or the coin creators! Unlike Primecoin, the more people that mine Gapcoin, the more coins per block will be produced. (Coin supply will increase logarithmically with the difficulty, this means it will grow in the beginning, but later, it won't change that much.)

There wasn't any premine!

To avoid instamine, the reward of the first 1152 blocks (about 48 hours) increased quadratically to its absolute value: the current difficulty. The block reward was 1/1152^2 * blockheight^2 * difficulty for the first 1152 blocks.

The source code was made available before launch (excluding the PoW function), so that everyone could setup their own testing environment, compile the software, and check that everything works. Windows and Linux binaries were distributed in an encrypted container before launch, the password was revealed at launch on Tue Oct. 21 2014 - 18:00:00 UTC”

#### Specifications

- PoW: **custom, prime gaps**
- Block target time 2.5 minutes (fast confirmations like [Litecoin](https://litecoin.org) = **4x faster transaction confirmations** than Bitcoin!¹)
- Block reward proportional to the current difficulty
- Block reward halving every 420000 (about 2 years)
- Cap: about 10 - 30 million GAP
- Difficulty adjusts every block and increases [logarithmically](https://en.wikipedia.org/wiki/Logarithmic_spiral) (it will probably take years to get to 50)"

(¹ based on the 10 minute average block time (Bitcoin) vs 2.5 minute average block time (Gapcoin).)

The Gapcoin project is particularly interested in prime gaps that have a merit of greater than 20. For a given prime <math>p</math>, the average prime gap to the next consecutive prime is given by <math>ln(p)</math>, where <math>ln</math> is the natural logarithm. The merit of a gap <math>g</math> is given by <math>g/ln(p)</math>.

