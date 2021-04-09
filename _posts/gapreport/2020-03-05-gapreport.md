---
layout: post
author: Seth Troisi
title: PGS news - new frontend to Prime Gap Search List web site
description: I made a new website to verify records and automatically upload them to github.
date: 2020-03-05
category: primegaplist
tags: news gapreport psg
---

New Frontend

*(coped from the Mersenne Forum’s Prime Gap Search group as pertinent to Gapcoin)*

##### 2020-03-05, 07:17 [Post to Mersenne Forum PSG: “New Frontend”](https://www.mersenneforum.org/showpost.php?p=538934&postcount=5)


I made a new website to verify records and automatically upload them to github.

[http://primegaps.cloudygo.com/](http://primegaps.cloudygo.com/)

([screenshots](https://imgur.com/a/2Ys7XJv))

I deleted [all gaps 10,000 to 11,000](https://github.com/sethtroisi/prime-gap-list/commit/71e0eb6d90554c9ed90c01d0fea3c89ce8023619) so they can be used to test the service.

The first page performs some validity checks (merit > existing, prime < 10,000 digits)

After you upload you’ll see: ![1 Queued](https://imgur.com/DpvPbv2 "`1 Queued ... <data>`")

<blockquote class="imgur-embed-pub" lang="en" data-id="DpvPbv2"><a href="//imgur.com/DpvPbv2"></a></blockquote><script async src="//s.imgur.com/min/embed.js" charset="utf-8"></script>

If you click the Watch Queue you can see it testing (if it’s a larger record) and the results of previous tests

After the record is verified it’s [immediately uploaded to the prime-gap-list github](https://github.com/sethtroisi/prime-gap-list/commit/20bb0b3f8db2f16703ab874513d7595f6d60ebf9) (or in this case my fork of it)

It’s fairly fragile right now (e.g. if worker: dead on the [status](http://primegaps.cloudygo.com/status) page it’s broken till I kick the machine again), but I’ll fix issues as they arise.

Chime in with what would be useful.

