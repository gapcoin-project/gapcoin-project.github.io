---
layout: post
author: Graham Higgins
title: “checkprimegaplist” - extended client RPC/API call
description: How to submit Gapcoin improved merits to the Prime Gap List
date: 2021-05-01
category: gapcoin
tags: post
---

The [extended Gapcoin 0.16.3 client](https://github.com/gapcoin-project/gapcoin-core/tree/gapcoin-core-extended) has been augmented with an RPC/API call `checkprimegaplist`:

```nohighlight
    checkprimegaplist startheight endheight
     
    Returns a list of formatted record gaps or improved merits appropriate for copying and
    pasting into Seth Troisi’s online submission service at https://primegaps.cloudygo.com/.
     
    Arguments:
    1. startheight    (integer) First block number to check.
    2. endheight      (integer, default = chaintip) Last block number to check.
```

The client retrieves the latest version of the Prime Gaps List `allgaps.sql` from [the Prime Gap List repository](https://github.com/primegap-list-project/prime-gap-list) and uses it to check all the gaps in the Gapcoin blockchain since the given starting height against the current record to find any improved merits or (unlikely, these days) new first occurrence record gaps.

![Screenshot of results from checkprimegaplist](/img/blog/checkprimegaplist.png)

If any candidates are found, the data is output in a format compatible for copying and pasting directly into Seth Troisi’s [online submission/checking service](https://primegaps.cloudygo.com/):

![Screenshot of onine prime gap list submission service](/img/blog/prime-gap-records-submission-service.png)

Set the discoverer field to “`log`”, set a date and paste the output into the textarea:

![Screenshot of completed onine prime gap list submission service](/img/blog/prime-gap-records-submission-service-completed.png)

Click the “Add” button and the input will be checked against the current record (in essence, confirming the checks performed by the extended Gapcoin client).

![Screenshot of results of onine prime gap list submission service](/img/blog/prime-gap-records-submission-service-results.png)

To confirm a successful submission, follow the top-of-page link `prime-gap-list` to the Prime Gap List’s Github repository where the latest commit should be the Gapcoin records just processed.

![Screenshot of prime gap list commits](/img/blog/prime-gap-records-list-commits-0.png)

And then follow the link to the commit details.

![Screenshot of prime gap list commit](/img/blog/prime-gap-records-list-commits-1.png)

<div class="ui ignored info message" style="font-style:italic; font-size:85%"><i class="info icon"></i>If you feel up to it, you might care to create a new Prime Gap List report page on the community web site. If so, there is an extended <a href="/projectdocs/2021/05/04/creating-a-prime-gap-list-report/" target="_blank">HOW-TO post</a> covering exactly how to do that.</div>

---

