---
layout: post
author: Graham Higgins
title: PSG news - state of play at end of 2020
description: Graph by Seth Troisi showing coverage and different contributions
date: 2020-12-13
category: primegaplist
tags: feature news gapreport psg
image: /img/blog/state-of-play-2020-12.png
---

Let's do some end of year celebration of progress

*(coped from the Mersenne Forum’s Prime Gap Search group as pertinent to Gapcoin)*

##### 2021-02-16, 10:50 [Post to Mersenne Forum PSG: “Let's do some end of year celebration of progress”](https://www.mersenneforum.org/showpost.php?p=571747&postcount=227)

Let's do some end of year celebration of progress.

I'll update these in late December

- [by year merit status](https://primegap-list-project.github.io/lists/merit-stats/)
- [prime gap animation](https://www.youtube.com/watch?v=CYbLUKsRNmM)

I calculated
- Number of updates this year >12,000!
- Largest merit this year (Seth's 38.0479)
- largest gap found this year (Martin's 1898630)
- Smallest update to a record ([#173](https://www.mersenneforum.org/showpost.php?p=559833&postcount=173), Gapcoin +0.00025 merit)
- Smallest gap updated this year (Rob Smith's 1906 merit 26.7)

I still need to find
- largest update to a record (Probably 122542 14.5 -> 28.1 merit)
- largest gap with an update
- Total merit improved this year

Any other fun statistics people would like me to calculate?

Humblebrag: I submitted 1340 records for 4441# and 930 for 2221# with an average merit of 20.8 and 24.37 respectively.


    $ sqlite3 gaps.db 'SELECT startprime FROM gaps' | 
    sed -n 's!^[^/]*[^0-9/]\([0-9]\+#\).*!\1!p' |
    sort | uniq -c | sort -nr |
    awk '$1 > 200 { ("sqlite3 gaps.db \"SELECT discoverer, count(*),round(max(merit),2),round(avg(merit),2) \
    FROM gaps WHERE startprime like \\\"%" $2 "%\\\" GROUP BY 1 ORDER BY 2 DESC LIMIT 1\"") |
    getline freq; print($0 "\t" freq); }'

    count primorial  Who|HowManyTheydid|MaxMerit|AvgMerit
       1391 4441#    S.Troisi|1340|28.98|20.82
       1002 2221#    S.Troisi|930|33.03|24.37
        962 9439#    Jacobsen|868|24.27|16.32
        923 6761#    Jacobsen|911|25.2|17.67
        786 49999#    Rosnthal|786|25.86|12.62
        736 4139#    Jacobsen|714|27.0|20.05
        579 9973#    Rosnthal|525|25.17|16.41
        535 10343#    Jacobsen|528|25.55|16.37
        400 6199#    DStevens|370|27.27|18.99
        376 6661#    S.Troisi|322|27.31|18.02
        371 5003#    Jacobsen|343|26.42|19.71
        351 9629#    RobSmith|269|26.52|16.87
        276 4409#    Rosnthal|229|27.07|19.95
        228 18481#    PierCami|226|19.12|12.15


Seth [subsequently noted](https://www.mersenneforum.org/showpost.php?p=567669&postcount=209):

I updated two tables on the lists site

"Top 20 gaps by merit" is now ["Top 20 largest gaps ordered by merit"](https://primegap-list-project.github.io/lists/top20-gaps-by-merit/)

"Top 20 overall merits" is now ["Top 20 overall merits [plus 50th,100th,200th,...,500th]"](https://primegap-list-project.github.io/lists/top20-overall-merits/)

I also added a weighted average line to [the merit plot on cloudygo](https://primegaps.cloudygo.com/graphs?max=70000) and min_x, max_x input.

You can see where the focused efforts from gapcoin & S.Troisi have increased average merit in the neighborhood of 5000-6000 and 45000-52000

![Image: State of Play](https://www.mersenneforum.org/attachment.php?attachmentid=24068&d=1609272258)

