---
layout: post
author: Graham Higgins
title:  Updating the Freiexchange re-charted order book
description: Reference HOW-TO for the record
date: 2021-04-18
category: projectdocs
tags: maintenance
---

# How to easily create a new update for the Freiexchange recharted order book

## Step 1 - retrieve a fresh copy of the Freiexchange order book

Execute the following:

{% highlight bash %}
{% raw  %}
curl -X GET https://api.freiexchange.com/public/orderbook/GAP -o freiexchange-orderbook.json
{% endraw %}
{% endhighlight %}

This will result in the creation of a file called `freiexchange-orderbook.json` with the contents:

{% highlight json %}
{% raw  %}
{
    "BUY": [
        {
            "id": "762002",
            "coin": "GAP",
            "basecoin": "BTC",
            "price": "0.00000078",
            "amount": "48.12000000"
        },
        ...
    ],
    "SELL": [
        {
            "id": "763667",
            "coin": "gap",
            "basecoin": "BTC",
            "price": "0.00000079",
            "amount": "79.00000000"
        },
        ...
    ]
}
{% endraw %}
{% endhighlight %}

There'll be more. The contents shown above have been elided for brevity and presentation with `...`.

## Step 2 - process the received JSON data to CSV


Execute the following:


{% highlight bash %}
{% raw  %}
cat freiexchange-orderbook.json | \
grep -v 'coin\|id' | \
sed -r 's/\s+//g' | \
tr --delete '\n' | \
sed -r 's/],/],\n/g' | \
grep -v 'BUY' | \
sed -r 's/"SELL":\[//g' | \
sed -r 's/]}//g' | \
sed -r 's/^\{//g'  | \
sed -r 's/}$//g' | \
sed -r 's/},\{/\n/g' | \
sed -r 's/"price"://g' | \
sed -r 's/"amount"://g' | \
sed -r 's/"//g' | \
sed -r 's/$/\\n/g' | \
tr --delete '\n' | \
sed -r 's/^/"/g' | \
sed -r 's/$/"/g' | \
sed -r 's/\\n"$/"/' > freiexchange-orderbook.csv
{% endraw %}
{% endhighlight %}

This will result in the creation of a file called `freiexchange-orderbook.csv` with the contents:

{% highlight csv %}
{% raw  %}
"0.00000079,79.00000000\n0.00000080,245.57388877\n0.00000081,81.00000000\n0.00000082,82.00000000\n
...
0.70000020,5.00000000\n0.90000020,5.00000000\n1.00000000,5.00000000\n3.00000000,0.00325577"
{% endraw %}
{% endhighlight %}

(Again, there’ll be more than the content shown above which has also been elided with `...`)

## Step 3 - Create a new post 

Using the following template:

---

{% highlight liquid %}
{% raw  %}
---
layout: orderbook
title: Freiexchange order book, re-charted
description: Reasonable, significant, offers to sell on YYYY-MM-DD.
author: <Your name here>
date: YYYY-MM-DD
data: ""
btcprice: 000000
---

{% include orderbook.html %}
{% endraw %}
{% endhighlight %}

---

Copy and paste the contents of `freiexchange-orderbook.csv` into the `data:` field, overwriting the `""`. It should appear as a solid block of text and look like this:

{% highlight liquid %}
{% raw  %}
---
layout: orderbook
title: Freiexchange order book, re-charted
description: Reasonable, significant, offers to sell on YYYY-MM-DD.
author: <Your name here>
date: YYYY-MM-DD
data: "0.00000079,79.00000000\n0.00000080,245.57388877\n0.00000081,81.00000000\n0.00000082,82.00000000\n...
0.70000020,5.00000000\n0.90000020,5.00000000\n1.00000000,5.00000000\n3.00000000,0.00325577"
btcprice: 000000
---

{% include orderbook.html %}
{% endraw %}
{% endhighlight %}


Then, change the `YYYY-MM-DD` placeholders to the actual date of creation, change `<Your name here>` to something else and change the BTC price to the USD value at the time of downloading the orderbook (just the integer dollar value, without the decimal/cents).

Save the entry in the `_orderbook` folder as `YYYY-MM-DD-freiexchange-orderbook.md`

That’s it.


