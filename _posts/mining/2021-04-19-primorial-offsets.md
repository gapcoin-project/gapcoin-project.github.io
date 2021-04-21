---
layout: post
author: Graham Higgins
title: Primorial offsets 
description: Copied across from the Mersenne Forum
date: 2021-04-19
category: mining
tags: technical
---

##  [Primorial offsets](https://www.mersenneforum.org/showthread.php?t=23753) by robert44444uk, 2018-10-30, 12:24 

This thread will capture any work anyone is carrying out to generate large primes gaps using Chinese Remainder Theorem (CRT) offsets generated using ATH's prime interval software.

The thinking behind this is that, for any range of integers there are some ranges where there are relatively few members of the range without small prime factors. ATH's software looks, as a start point, to define a range of integers, (called an interval in the software) and then to look at possible modular values for the primes <math></math> in a primorial <math>p#</math> to determine those which generate low numbers of members with no factor <math><=p</math>.

Using CRT, those combinations of modular values can provide an integer, referred to as the offset, which if added or subtracted from the primorial, provides a starting point for an interval with these properties. If we multiply <math>A</math>, an integer, by the primorial, then add or subtract the offset, the properties of the interval demonstrate similar modular properties.

Hence, for any given primorial and chosen offset, it is possible to check many gaps by altering <math>A</math> alone.

The relative values of <math>p</math> that are the most efficient for any interval are yet to be determined. But if <math>p</math> is too small, then the chances of any <math>A</math> providing all members with composites (i.e. maximising the theoretical benefits of the interval) are very low. If <math>p</math> is too high, then the chances of meeting this criterion is quite high, but the absolute size of the members of the interval is also high, lessening the chance that the resulting prime gap is not a record.

To ensure decent coordination, mersenneforum members may reserve an interval size here. Interval sizes can be any value but for convenience sake, the intervals that may be reserved are 50 apart, starting at 1000.

Participating members should report any or all of three things:

1. results in aggregate coming from using the ATH software - for example the numbers of CRT offsets that provide the lowest numbers of composites for a given interval. For example, for the 2000 interval, carrying out a comprehensive test of all possible modular results for primes up to 37, there were 16 combinations providing solutions of 275, 166 providing 276, and 1806 at 277. Where a "solution" is the number of members of the interval with no factors smaller than or equal to 37

2. Any CRT offsets that are useful but which the member has no further interest in - typically this will be any offset that provides a solution within three of the best found. Three pieces of information are required - the interval, p, and the CRT solution.

3. Any records posted to Dr Nicely's site.

4. ATH output files can be posted if the member wants to release a range.

The latest version of ATH's software, written in c is to be found here:

[https://www.mersenneforum.org/showpo...&postcount=114](https://www.mersenneforum.org/showpost.php?p=498611&postcount=114)

A working piece of software written in perl, developed for another purpose by danaj, is to be found here:

[https://www.mersenneforum.org/showpo...&postcount=103](https://www.mersenneforum.org/showpost.php?p=498140&postcount=103)

### Reservations and results
```nohighlight
    A = Interval
    B = Reserved by
    C = Records sent to Dr Nicely

    A       B               C
            
    1000        
    1050        
    1100        
    1150        
    1200        
    1250        
    1300    robert44444uk   1
    1350        
    1400        
    1450        
    1500        
    1550        
    1600        
    1650    robert44444uk   
    1700        
    1750        
    1800        
    1850        
    1900        
    1950        
    2000    robert44444uk   
    2050        
    2100        
    2150        
    2200    robert44444uk   47
    2250        
    2300        
    2350        
    2400        
    2450        
    2500        
    2550        
    2600        
    2650        
    2700        
    2750        
    2800        
    2850        
    2900        
    2950        
    3000    robert44444uk   
    3050        
    3100        
    3150        
    3200        
    3250        
    3300        
    3350        
    3400        
    3450        
    3500        
    3550        
    3600        
    3650        
    3700        
    3750        
    3800        
    3850        
    3900        
    3950        
    4000    robert44444uk   
    4050        
    4100        
    4150        
    4200        
    4250        
    4300        
    4350        
    4400        
    4450        
    4500        
    4550        
    4600        
    4650        
    4700        
    4750        
    4800        
    4850        
    4900        
    4950        
    5000
```

---

#### 2018-10-31, 12:02  [robert44444uk](https://www.mersenneforum.org/showpost.php?p=499154&postcount=3)

I have run 2000 and 4000 up to 79# and 101# respectively. I had 16 useful offsets that provide 197 positions within the 2000 interval where there are no prime factors smaller than 79, and 165 offsets that provide 405 positions within the 4000 interval where there are no prime factors less than 101.

I realise now that 4000 is probably too large an interval for ATH software to handle - I would need to run up to 137# to be competitive with the records.

Reserving 3000

---

#### 2018-10-31, 16:50 [ATH](https://www.mersenneforum.org/showpost.php?p=499170&postcount=4)

I can [extend it to include higher primes than 101](/mining/2021/04/19/potential-crt-improvement/), but the problem is calculating CRT offset. It would exceed 128 bits so I would have to switch to GMP library to calculate it instead of the 128 bit variables I use now, and then you need to compile the GMP library first in order to compile the program

It should be no problem to compile GMP in MSYS2, I do it all the time, and you have all the needed packages installed, but I do not know if you feel it is worth it. The higher you go using only the best few solutions from the lower runs, the higher risk there is that you are no where near the real minimum. 

---

#### 2018-11-01, 08:02 [robert44444uk](https://www.mersenneforum.org/showpost.php?p=499230&postcount=5)

It would be worthwhile to do the GMP solution.

I agree that we are nowhere near the real minimum at higher primorials, but then again, I think a few tweaks to the program would allow for pretty decent offsets. For example if programmed to take results that are within 5 of the record at a given level, instead of 3, and then advanced those two primes at a time, then you could quickly get good results. To do that, a tweak would be required to eliminate from the results file those first few solutions that come out that are nowhere near the minimum. You could do that by calculating the theoretical expected result given an input file and only outputting those which are within 5. What do you think?

Took one offset from 2000 interval forward last night and 4 records this morning between 2600 and 2750 :)


If the CRT calculation is time intensive then maybe the program should only calculate it if the result is within 2-3 of the best solution as it is unlikely that people would look at solutions that are far way from the best.

I've been concentrating on two prime gap ranges (2000-3000 and 6000-8000) where it is clear there is relatively low hanging fruit in terms of records. It is surprising how weak the range 2000-3000 is. I think this partly due to Gapcoin's efforts, which appear as a very clear line starting at 5000 - clearly smaller gaps were not that interesting to them - and Spielaur, who has clearly invested a lot of computer resources in the 1500-2000 range but perhaps less after that.


![Prime gaps by merit](/img/blog/primorial-offet-prime-gaps.png)


There are some fairly big gaps in terms of merit coming from this study, these are from the last two weeks and have already been submitted, The format is the simplified version of that used on the Nicely site, i,e. gap, merit, number of decimal digits of the lower of two primes defining the gap, and the detail of that prime, # representing the primorial. The value following the + is the offset developed by ATH's program.

The last gap was the smallest record found.

    2982    32.39   40  3012136000*79#+290310270974475604429744889245-2178
    2368    32.26   32  39771103997*59#+171014232051617437041-1652
    8646    32.09   118 899511684*269#+5957374301812580490985358710617344145356905967130828134768836382571519478219821452087369852491775393604015-5912
    8392    31.23   117 418821175*269#+5896655172957128379466664980541054439832493567791706402422867847469770908884219241972694445732755415692205-2924
    8150    30.78   115 8497670*269#+5896655172957128379466664980541054439832493567791706402422867847469770908884219241972694445732755415692205-4438
    2800    30.01   41  10443985146*79#+2965490987166802298083559027821-1998
    3708    29.82   54  3537439094*109#+243154260282212682243913611242329809258287235-3046
    7838    29.34   117 86297041*269#+5957374301812580490985358710617344145356905967130828134768836382571519478219821452087369852491775393604015-2692
    7870    29.33   117 284758679*269#+7492355714324105806675448398670447890842962554279407545969581629829188193229173583157646315295447832339675-3506
    2178    29.32   33  94343930124*59#+1067076873163923483-832
    2732    29.22   41  12351800046*79#+2965490987166802298083559027821-1184
    7810    29.19   117 139673464*269#+5240614097214307182652892455738985324935115803017173229924268024043265087223577925588717365155009939172265-2912
    7650    29.12   115 1070393*269#+7492355714324105806675448398670447890842962554279407545969581629829188193229173583157646315295447832339675-4364
    3920    29.11   59  7708801521*127#+1111132328791289255885652218210449264035303164895-1378
    ….
    2012    27.10   33  90267121489*59#+1067076873163923483-1216

---

EOT