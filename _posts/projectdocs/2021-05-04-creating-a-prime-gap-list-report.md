---
layout: post
author: Graham Higgins
title:  Creating a prime gap list report
description: How to add a prime gap list submission report to the community web site
category: projectdocs
date: 2021-05-04
tags: content
---

You will need to have read the [“Contributing to the community web site” post](/projectdocs/2021/05/03/care-and-maintenance/), have Jekyll, Bundler and git installed and a local clone of a fork of the Gapcoin Project community web site repository.

Follow the process described in the post describing how to [submit Gapcoin improved merits to the Prime Gap List](/gapcoin/2021/05/01/checkprimegaplist-rpc-api-command/).

Follow the top-of-page link `prime-gap-list` to the Prime Gap List’s Github repository where the latest commit should be the Gapcoin records just processed.

![Screenshot of prime gap list commits](/img/blog/prime-gap-records-list-commits-0.png)

Follow the link to the commit details.

![Screenshot of prime gap list commit](/img/blog/prime-gap-records-list-commits-1.png)

Create a new post by copying the last `primegaplist` post into into a new post, filename format `YYYY-MM-DD-N-updates.md` where N is 0 if there are no existing posts for that day or N is one more than the N of the last update post for that day.

{% highlight liquid %}
{% raw  %}
---
layout: post
author: Gapcoin
title:  Improved record 22682 merit=25.6035 found by Gapcoin
description: update to Prime Gap List
date: 2021-04-30
category: primegaplist
tags: primegap
---

Gaps discovered or merits improved: April 29-30 2021 submitted to and accepted by the Prime Gap List

[Improved record 22682 merit=25.6035 found by Gapcoin]
(https://github.com/primegap-list-project/prime-gap-list/commit/98cf8bfe094ad6ddb2e61e45115b5b941f3d9f5a) 
committed via prime-gardner¹ on Apr 29th, 2021

```
Improved record 22682 merit=25.6035 found by Gapcoin
```

¹ *“prime-gardner” is the reference id for Seth Troisi’s ultra-cool
[online prime gap submissions, checking and commit service](https://primegaps.cloudygo.com/)*
{% endraw %}
{% endhighlight %}

Preserve the existing content format, replace the old data with the new data - change the post title to the commit comment, update the date, change “April 29-30 2021” to whatever period was covered by the `checkprimegaplist` scan (see [previous posts](https://github.com/gapcoin-project/gapcoin-project.github.io/tree/master/_posts/primegaplist) for examples), then copy and paste from the commit data to change the body content to match the commit data.

Save the file. Commit the changes, push the commit, create PR. Job done.

---

