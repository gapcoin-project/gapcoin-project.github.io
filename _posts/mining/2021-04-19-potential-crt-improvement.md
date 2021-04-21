---
layout: post
author: Graham Higgins
title: Potential CRT improvement 
description: Copied across from the Mersenne Forum
date: 2021-04-19
category: mining
tags: technical
---

##  [CRT offsets](https://www.mersenneforum.org/showthread.php?t=26660) by henryzz, 2021-04-01


In the past using CRT offsets has been considered as an alternative to using a divisor to reduce the density of candidates after sieving. This had some success with small primorials but struggled with larger primorials due to good CRT offsets being difficult to find. We used a program written by ATH last updated [https://www.mersenneforum.org/showpo...&postcount=117](https://www.mersenneforum.org/showpost.php?p=499324&postcount=117).

> Here is a version using GMP library to calculate CRT offsets, so it can go beyond maxprime 101: [primeinterval.c](http://hoegge.dk/mersenne/primeinterval.c)
> 
> No real maximum now, but it gets messy. I tested at the 1700 interval and already at maxprime=73 there are 11.5K solutions with minimum+2 and it finds more and more solutions if you continue to run min, min+1 and min+2 to higher values.
> What is the best maxprime for 1700 interval? Then I can provide some CRT offsets, I did a full run to maxp=37 and ran the best solutions higher, but I'm not going to use them for any prime gap search.
> 
> I do not think we want to save min+3 and min+4 solutions like you suggested. I tested at 1700 maxp=29 and 1250 maxp=31 and there were 4.5K / 11K min+3 solutions and 25K / 111K min+4 solutions and running all those would take a very long time, and that would just give too many solutions at higher maxprimes.

> I changed the way it resumes from earlier file. Instead of running it 2-3 times with the min value, min+1, min+2, you just run it once with the minimum value: (example 1700 maxp 37 minimum 231 running it to maxp=59):
> 
>     primeinterval.exe 59 primeinterval1700-37.txt 231
> 
> It will test all the 231 solutions first and then continue automatically with the 232 solutions and 233 solutions and you can stop it at any time with CTRL+C if it takes too long, and use the best it found so far in the primeinterval1700-59.txt file. 
> 
> ---
> 
> It will add CRT value now to the results file `primeinterval<interval>-<maxprime>.txt`.
> 
> It is the middle of the interval, so subtract "interval/2" to get the start of the interval.
> 
> To get CRT values from old results for example `primeinterval1450-31.txt` run:
> 
>     primeinterval.exe primeinterval1450-31.txt 204
> 
> to get CRT values for solutions with value 204, writing them to screen and also to the file `primeinterval1450-31CRT.txt`


For small primorials this did an exhaustive search but for larger primorials this was impossible and it used a combination of random selection and exhaustive search on the largest primes.

I have written a program that uses an alternative approach. It starts with zero offsets for all primes and then iterates through the primes trying all the possible offsets for each prime. My program will also iterate through pairs of primes optimising offsets. Iterating through sets of 3 or 4 primes at once is implemented but is impractical currently for primorials large enough for them to be useful.

An example CRT offset:

For 7993# the divisor of 13# or 17# are optimal with 6880 and 6878 candidates remaining after sieving to 7993 for a gap of 220k centred on 7993#/13# or 7993#/17#.

The following CRT offset has only 6776 candidates remaining for a gap of 220k centred at 7993# + c after sieving to 7993. This is ~98.5% of the candidates. I have also included the list of offsets for each prime.


```nohighlight
CRT: 3950072742283514595531834808142103045614620069560430020442846071927042936047429482112297325719444502473532707
329370573730389324553174683365279370939507211600445225516048250440397555332652881212433758244573874632676622001299
043007346375481866767053528956773335210722626827980817254288784361328276569640150893464777679758438443836450023126
223413167599953238852368544020790788128038698460081668970966536437188500602983515747931210829499949995163414365872
550504141466544554868498541094794244286967441790869062837847215193490813862210526464236222617483086945537658254496
518907592528959689912802974657880807146320230082111595157606504891636729985923155991322594409558170848037106441763
356495841615106250877084379744468415937527667197208395181787945582380304049749373234086464220069721844696740257126
846249450812403711655288890819826074189449129823964539181611268671517946826307219645774740902104477000109254945787
250148567908062658732581671542847010037127369042736532045735868329765522736987975728529500105476917333877905561163
306339695143127171882574055298946675703306822220902193964461667868000886407778371208321219701982444367369126150989
118045956087854161587616527093211070134986376404726847543899845684600581816850639582421294255713362527081945682857
178163727393966596712480985254084268815400050836739586055765736219771150377292549034737395799265016197504864123991
407121810491806175276415468475142334735338081474671449841316560959527619990129796175719983525753499951524070379416
931393986094364582794333672431311224294195386331889768896358353366880079287863998369555682223788568089760838012105
975493888114332296340918498885741688962151775485539422049044019128656066875558631228133577445909403415870781857107
084561538632221879524832376124468083784304364634028390964681016659353768873121488550122740647585145149158231537988
283016139334404043813416620514989239861296172211655647750201530872123788896448832323787301331739144270792949990005
151115354611203910858527326240819080485201229870040745355923313047300382214325961153809145438468797375316882413761
628694238959560465820869175782392389584470076209895323333983322619077933830375009104667891053466685987883399232973
253777072778067539399378253802505947721712688573479524459854500306853050715018176049899280718284425949873718750995
034458461066060493227297840268521538841029543168317451414778606516450162579940019386233659637239418353370196456251
355501905600363683262354532100171517522568173835273584598702915300470916595896991295865845001005495580338387506519
527616071437683100429187322759424754893244639940761295778534389420804463752007619739031657780502867771110528611347
556520834529086971336564548361343455366734776128548790200452898288554752535737191034701269019462947140078336180659
617610441901915472809069139731936221946653010602964323102060328193726674870533679499264775691375026536872234833367
102406133661012523977365000159714957560801881263391093376427255287606162762372805508144422318415809117430498455503
228035570246491145034629219784014710749831265886995739513614082074226364140225635967795682106658187963769455760675
045230946867224910204556424564899160165613889526824058468522485745820230867288175600167470938609791723835328741292
518009279190501568569412847041761805801219469666570751875554632795304773866313721356436701823107785793246129039879
269547453341199498592235857307648101018568787074871118244783486567418313248725104435569059363765296921930607451327
80669

Score: 6776 for 1 2 4 3 9 12 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 3362 0 0 0 0
0 0 0 0 2893 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 5270 0 0 0 4439 1541 0 0 0
0 0 0 0 0 2872 0 0 0 0 0 0 0 3520 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
5939 0 0 0 0 0 0 0 0 0 0 4981 4388 0 371 0 0 0 0 4634 0 0 0 6209 0 0 378 0 0 0 2646 1350 0 0 0 0 5471 0 0 0 0 836
1170 0 4683 0 0 0 0 0 0 3456 530 954 0 4405 0 0 3325 0 0 0 0 0 0 690 0 0 0 0 0 0 0 450 2594 0 0 0 0 910 3955 5094 0
0 0 0 0 0 6479 0 0 0 0 0 0 0 0 0 0 0 4493 1832 0 0 4368 0 0 4977 0 4057 0 3682 2514 0 0 0 0 0 0 0 0 0 0 0 0 1851 0
0 6194 5711 0 316 6248 1476 3693 0 0 6250 0 0 0 0 0 0 7204 0 0 0 0 0 0 0 0 0 0 5252 0 3548 0 7488 0 0 0 0 0 0 0 0
2338 0 0 1744 0 0 0 0 0 0 599 0 2106 359 0 6714 0 0 0 0 0 0 0 0 2330 0 0 5040 2711 0 0 0 6 0 5315 0 0 0 6623 4980
6269 6750 4105 6794 4337 0 0 5760 6086
```

This <math>~1.5%</math> reduction in the number of candidates doesn't seem like much but it doesn't tell the full story. On average around 1 in 160 numbers are prime after sieving at this size. To test the same range now <math>160^0.985=~148</math> tests are needed. This is a reduction of <math>~7.5%</math> which is a lot more significant. Edit: Not convinced this is correct. I think it would be more like <math>160*0.985</math>.

I am pretty certain that I am only scratching the surface here with the CRT offsets and far better should be possible.

Unfortunately, my program is a bit of a mess and would need quite a bit of tidying up in order for me to post it. Eventually, I will tidy it up although I am quite busy with my PhD. If anyone wants any CRT offsets I can run some searches for people.

If anyone has any suggestions on how to improve these CRT offsets I would appreciate the ideas. I am considering posting this as a puzzle in the puzzles section of the forum as that will hit a wider/different audience. 

---

I thought it might be useful for me to share my algorithms for optimizing the offsets for one or two primes. Any improvements or questions would be appreciated.

#### Algorithm for optimizing one prime at once:

1. Calculate current score
2. Choose a prime <math>p</math> to investigate
3. Generate the sieve array ignoring the prime <math>p</math>
4. Loop through sieve array. If the element is set then increment the value for <math>x % p</math> to count how many times that modulus occurs. As we are iterating subtraction can be used rather than division to maintain speed.
5. Choose the modulus with the maximum number of occurrences.
6. Return to step 2 and choose the next prime

#### Algorithm for optimizing two primes at once:

1. Calculate current score
2. Choose a prime <math>p</math> to investigate
3. Choose a candidate offset for the prime <math>p</math>
4. Calculate a score with the offset chosen in step 3. Record the difference between this and the best score. This difference is the improvement needed by the second prime.
5. Choose a prime <math>q > p</math> to investigate
6. Generate the sieve array ignoring the prime <math>q</math>
7. Loop through sieve array. If the element is set then increment the value for <math>x % q</math> to count how many times that modulus occurs. As we are iterating subtraction can be used rather than division to maintain speed.
8. Check if the modulus with the maximum number of occurrences improves the score enough to correct for the offset chosen in step 3 (that was probably worse than the best). If so keep it.
9. Return to step 5 and choose the next prime unless all have been tried
10. Return to step 3 and choose the next offset unless all offsets have been tried
11. Return to step 2 and choose the next prime 


---

#### 2021-04-02, 15:22 [henryzz](https://www.mersenneforum.org/showpost.php?p=574998&postcount=4)

I have discovered that my code for optimizing two primes at once never ran in that example.

A new solution with a score of 6751 which is a 1.85% reduction:



```nohighlight
CRT: 8469576951389608151420874612615248616679698628057854437509053972612955366555320894561872624382237635079885558
563870534052217477436104252867174000041944156922912561766571997613006274021838826098197325662350934223350741723829
453060156074421445837208255551556476810588934325648951128820567850687481042537296586478777428454819368501658137716
248939703709052207615032122029068361490990563292657505826840688262675440573949681785688562184745930464202386467618
022726533740660243190799332773437399842946158833982674676425510200684032568143951671293691370321799819336716700358
907545429943530422898407791341511921681314446274773327602900320481956968946843797282682574932894684966040924977143
304891767716524218522224936463951014999066477878268171275264707709149431832902561928496148592689848474046162851289
479187235111656666213839360392289731861241239720808886029056558521388726512874800370512496880793187880924543820118
420840145398615041449704391530784132285244099094179856336900303772721468723679779063627069841459985611913686007421
021243652404760798171849403655737475138373549743888443864575288425141105161547963150705121654884290994510253244670
208557545985000235032372142518137921512941385589556622276085201236169381606533374179244088628404687835948161844272
649862634525800077115357854869915899243762608571034327460038871807559461325957221993127284885145386256067988154853
447758014361607999698831259504448329042743089130220831200489088887537838750681387087767022701182626524696926458762
623129955177683776233366828778342669184487734636570942685311644027753361053450100749345467048948865209261963820137
122554115571221339740099583465185411253888270073588498091981787259244906051673644422452596024426500938487129453252
645374507942343995126219107225573379784056315868057346232635860997414098016376029573942170734698751505396133782438
672809906699219815739263597462525293228996396324160649240961334834847630260552990397264236203563967578703243898637
175343089911074500785618183264451868946154512867798070635093405106622945892148665297395754589653740283735911128979
800063785478611407363085180586031749390310708165010716505502352043889672055641034853846639815491476733852947674830
142758738340739713317166255073384485662593989473604750482708526620508676929131092773723611139952568902506370068713
560887716229793234977719976539390718331237488896298963758648587199452808298507103139928999916636620120946467017007
745896989025950050891299944364458128718199522075512823093943125147828933774814684579625127285057613564486948473575
018389753837523630779976784430768308097266761592607807793095521726619861464426048736379270150434607863399056390508
683087224846655375799136157533277970790907876341451083224572991331610888258518518910406592214153325486473654621570
104732800693060638149475785478579287985467321570059015938495293761530426109736573097235202893030745098214278835496
858156318531446429216802142654019627757560352495360637123367043006265244002462352550828844394477047298735623303654
397493154092689404708886131824996652784745146417777652008770799504658114793560731473454734217047847792687746815566
476473161282366702298904860480598385581466291458096839125454749809204220298893707965248295603648219182839069213492
098305733841698267716224826531076751266302888478535140828022311245755299925807313340739971476323322672142330110864
171788382566255008478431410933741077804609620498830400767753967830750382506079963878400826435518792682438473813491
299

Score: 6751 for 1 2 4 3 9 12 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 3362 0 1744 0
0 0 0 0 0 2893 0 0 0 0 0 0 0 0 0 0 0 1634 0 0 0 0 0 0 0 0 0 0 235 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 638 0 0 0 5017 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 5270 0 0 0 4581
1541 0 0 0 0 0 0 0 0 2872 0 0 0 0 0 0 0 3520 0 0 0 0 727 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 4407 0 0 0 0
0 1330 0 0 0 2258 0 5939 0 0 0 0 0 726 0 0 0 0 4981 4388 0 371 0 3057 3423 0 4634 6119 0 0 775 0 0 378 0 0 0 2646
1350 0 0 0 0 5471 0 1805 0 0 836 1170 0 4683 0 0 0 0 0 0 3456 530 954 0 4405 0 858 3325 0 0 0 3002 0 0 690 3601 0 0
6003 0 0 0 450 2594 0 0 0 0 910 3955 5094 0 0 0 0 2185 0 6479 0 0 0 4089 0 5661 0 0 0 0 0 4493 1832 0 0 1567 0 0
4977 0 4057 0 3682 2514 0 0 0 0 6370 0 0 0 0 0 2268 0 1851 216 0 6194 5711 0 316 6248 1476 3693 892 0 6250 0 0 0 0
0 3850 7204 0 5047 0 0 1512 3954 596 95 0 4028 5252 0 3548 0 7488 1459 0 0 0 0 0 0 392 2338 0 0 1744 6526 0 0 0
2903 0 599 2963 5057 359 0 6714 0 0 0 0 0 0 0 0 2330 0 0 5040 2711 4294 0 0 5880 29 5315 0 0 0 6623 4980 6269 6750
4105 2147 4337 4503 0 5760 6086
```

---

#### 2021-04-02, 23:22 [R. Gerbicz](https://www.mersenneforum.org/showpost.php?p=575032&postcount=8)

Improved solution with 6727 numbers survived the sieve:

```nohighlight
c=894101235464362219721356880526656966576862269828154398514501227439505880868173768034261872450219940738532
43350370299218133228354024172918920017036849608077012248962738493678518082207775942083484056118252504525593
80414780304298992207890252310184707262740254929665772228957303385302928849113042779776992222068138260839255
28607407799301583580289812608633646270306158259174036079292088947790819460085862530772370455045076770278964
55064908446002128034171196506275149100055425317067364671307834413677464783699720160433926631569221051354963
35803586093362596457302819362465946034566615707768885506741636348556338317963848280912807008109087520150940
38200535425967302545438000348218598245332367415689514556533807924323611251898728570083748171206589525074279
58679745769842925460680425818953365181704572871839345227075992459267527846337121030824136376187042569885692
10722274326791511120645239907644527154782679580127145474438852010305282801780239669395758845384660865748437
76408189417837812055471550930523625276363727449113222586477779002040574021717468505417530151198648354820236
80964418174198740762129115698241224871201018162888708859161829291335582800422806742011143504315799265919769
36796972973061932689468532280422396592709569899768089640401632537872256729847282950755895853767280127461793
10829710199392901875388666410598686890175601525712229638029608005550169463504405962647786956288427048281930
47072681159911223554064976126958734963918941014343234874571860440967965217479705830036468398553000091145695
93337886842295820593052610225987962345106787109786302291427379436270919430127693008256355164147448187965114
77636303583986805007029374735816223473972159595733842011861521954425026119396159574670408544104665751951696
38466967810245054449350597756765225312472479257248802349585758605649143048117010660389529528043320152670405
02580047791420943681273566400325721520558804009564809916717141574196738442163272919962879857747659497880489
94117868350791991047293406031640441655409535734211716075143902785171452558689018612296071330944599380563622
30472836083036407412903243588855198821949043332685655742371549224787113751287824584063421646663784894026618
24447357500867428897660316196663118206336842869737743596280344044015835082364888986468225053650464072381136
73259344652677158165745036109887829163563567646520223972380464316042166790790693114352428388364722769592005
87548920949652940569105391043407626452844371527887432843989465732723846724833710174768967828398434713986155
15395940131777906246113250802052973918333884274984854706688025066355226173065988746612492980982975266920198
54328905349621621861481661734112299946598507185699362243478831896469919744277949661645477466251371546539398
05397701997959806477659053240441074295059685929094294012427649322807468565340859426585731199399783646990002
53265977227198583807291511831086075684465472775470082731217759910993977117967348428927908074063329366309457
08209528554119434233296421185811055765457485357326882091683943278438330731574590639585492816854036436053779
65678942098231313147591095627163957087545559859910481329169248466752655290898181870158091900791146944729725
19592754724171842012565848796181631322938933743515659169520745670605295070062705804694794053303649377277137
03898012119701295575478573459984224904343045725473505704190646951312484991894044407080091394692206526715577
671509672870081507785250017047593209776248063781170242589849299138314228397347311816225505996337124551829;
t=1;forprime(p=2,7993,t*=p)   
sum(i=-110000,110000,gcd(c+i,t)==1)
%45 = 6727
```

---

#### 2021-04-03, 05:35 [CraigLo](https://www.mersenneforum.org/showpost.php?p=575048&postcount=9)

Nice work on the CRTs.

If you are looking for a gap of 220k then the first prime can range from -220k to 0 and the second prime can range from 0 to 220k. If you want to maximize your chance of finding a gap of 220k you probably want to run your CRT code for a gap size larger than 220k.

220k is roughly a merit of 28. I have a code that will calculate the probability of finding a gap greater than a given merit for a primorial and offset. I ran it for the 3 CRTs above and /7#, /11#, /13#, /17#.

```nohighlight
Merit     CRT_6776    CRT_6751    CRT_6727    7993#/7#    7993#/11#_1 7993#/11#_13 7993#/13#   7993#/17#
20        8.99E-04    9.10E-04    8.77E-04    1.00E-03    1.03E-03    9.97E-04     8.20E-04    6.18E-04
21        5.13E-04    5.19E-04    4.96E-04    5.35E-04    5.73E-04    5.56E-04     4.70E-04    3.56E-04
22        2.89E-04    2.92E-04    2.76E-04    2.80E-04    3.15E-04    3.05E-04     2.65E-04    2.03E-04
23        1.60E-04    1.61E-04    1.52E-04    1.44E-04    1.71E-04    1.65E-04     1.48E-04    1.14E-04
24        8.76E-05    8.80E-05    8.17E-05    7.28E-05    9.13E-05    8.80E-05     8.15E-05    6.35E-05
25        4.73E-05    4.74E-05    4.34E-05    3.63E-05    4.81E-05    4.64E-05     4.44E-05    3.51E-05
26        2.52E-05    2.52E-05    2.27E-05    1.79E-05    2.51E-05    2.41E-05     2.39E-05    1.92E-05
27        1.33E-05    1.32E-05    1.17E-05    8.66E-06    1.29E-05    1.24E-05     1.28E-05    1.04E-05
28        6.92E-06    6.83E-06    5.99E-06    4.15E-06    6.56E-06    6.30E-06     6.73E-06    5.56E-06
29        3.57E-06    3.49E-06    3.01E-06    1.96E-06    3.30E-06    3.17E-06     3.51E-06    2.96E-06
30        1.82E-06    1.76E-06    1.49E-06    9.17E-07    1.64E-06    1.57E-06     1.82E-06    1.56E-06
31        9.16E-07    8.82E-07    7.23E-07    4.25E-07    8.08E-07    7.75E-07     9.34E-07    8.17E-07
32        4.57E-07    4.36E-07    3.48E-07    1.94E-07    3.94E-07    3.78E-07     4.75E-07    4.24E-07
33        2.26E-07    2.13E-07    1.65E-07    8.80E-08    1.90E-07    1.83E-07     2.40E-07    2.19E-07
34        1.11E-07    1.04E-07    7.79E-08    3.95E-08    9.12E-08    8.75E-08     1.20E-07    1.12E-07
35        5.38E-08    4.97E-08    3.63E-08    1.76E-08    4.33E-08    4.15E-08     5.95E-08    5.68E-08
36        2.59E-08    2.37E-08    1.68E-08    7.76E-09    2.04E-08    1.96E-08     2.93E-08    2.87E-08
37        1.24E-08    1.12E-08    7.67E-09    3.40E-09    9.51E-09    9.13E-09     1.43E-08    1.44E-08
38        5.87E-09    5.23E-09    3.48E-09    1.47E-09    4.40E-09    4.22E-09     6.94E-09    7.13E-09
39        2.75E-09    2.43E-09    1.57E-09    6.34E-10    2.01E-09    1.94E-09     3.33E-09    3.51E-09
40        1.27E-09    1.11E-09    6.96E-10    2.69E-10    9.11E-10    8.76E-10     1.58E-09    1.70E-09
```

CRT_6776 is better than CRT_6751 for merits > 26. CRT_6727 is worse than the other 2 CRTs for all merits (it might be better for some cases below 20).

```
7993#/7# is best below 20
7993#/11# is best from 20-26
CRT_6776 is best from 26-30
7993#/13# is best from 30-37
7993#/17# is best above 37
```

The <math>/Q#</math> cases were computed with <math>A mod Q# = 1</math> but there is some variation among the offset chosen. For <math>/11#</math> I ran for offsets 1 and 13 which were one of the best and worst cases. The offset of 1 gives about a 4% improvement over 13. 

---

#### 2021-04-05, 13:51 [R. Gerbicz](https://www.mersenneforum.org/showpost.php?p=575238&postcount=11)

> henryzz
> That's a nice improvement. How did you find this?


For that record used only your 1st method with the following modification:
collect in array/vector those res values that occur maximal times as x%p and choose randomly(!) one res value from these. It gives some breath for the algorithm, but notice that you can stuck in a local min, so without several restarts you could be far from global min. I'd say the above result is not very far from optimal, but this is just my guess.

> henryzz
> I think this shows that it is necessary to pay attention to the target gap size with these searches.

Yeah, use it if you'd want to reach say merit=25, use a larger gap for merit=30. Ofcourse we don't know in advance what merits you will get in a search, but using this gap for merit=40 isn't that useful/optimal. 

---

#### 2021-04-05, 15:06 [CraigLo](https://www.mersenneforum.org/showpost.php?p=575246&postcount=12)

> henryzz
> I think this shows that it is necessary to pay attention to the target gap size with these searches.

Yes, but CRT_6727 is only 5th best of the 7 options at 220k and 15% worse than CRT_6776 even though it has the fewest remaining candidates so it is more complicated than just finding the minimum remaining candidates. I still think you would get better results for 220k if you ran the CRT code for a value greater than 220k. You could also try assigning a higher score to candidates near the center and a lower score to candidates farther from the center. 

---

#### 2021-04-05, 15:25 [henryzz](https://www.mersenneforum.org/showpost.php?p=575254&postcount=13)

> CraigLo
> Yes, but CRT_6727 is only 5th best of the 7 options at 220k and 15% worse than CRT_6776 even though it has the fewest remaining candidates so it is more complicated than just finding the minimum remaining candidates. I still think you would get better results for 220k if you ran the CRT code for a value greater than 220k. You could also try assigning a higher score to candidates near the center and a lower score to candidates farther from the center.

220k is nearly a record gap at this size(it was until recently). I would expect a lot of records in 120k-160k range. This size range would be better for maximising record gaps/day rather than the overall record. 

---

#### 2021-04-05, 16:55 [CraigLo](https://www.mersenneforum.org/showpost.php?p=575263&postcount=14)


> CraigLo
> This was a general comment that applies to gaps of any length. I only picked 220k because that was what you used. Finding offsets with fewer remaining candidates over some range does not necessarily lead to better odds of finding a gap of that size.

As far as I understand it optimising a range of x should provide better odds of finding a gap of size y with y < x. We just need to work out the correct ratio of x and y. 

---

#### 2021-04-06, 06:33 [CraigLo](https://www.mersenneforum.org/showpost.php?p=575301&postcount=16)


> henryzz
> As far as I understand it optimising a range of x should provide better odds of finding a gap of size y with y < x. We just need to work out the correct ratio of x and y.

I think that is correct. For a target gap size of G, all gaps >= G are going to contain some candidates < -G/2 or > G/2. You can't optimize the result while ignoring all of these.

Probably the best way to calculate this would be to scale the remaining candidates by the probability that they contribute to a gap of size G. Candidates near 0 would have a probability near 1. Candidates near +/- G/2 would have a probability near 0.5. Candidates near +/- G would have a probablility near 0. So run from -G to G and sum the probabilities for all remaining candidates and then minimize this.

I'm guessing you could get similar performance by doing what you suggested. Minimize the remaining candidates for some range > G which needs to be determined.


---

#### 2021-04-06, 12:39 [henryzz](https://www.mersenneforum.org/showpost.php?p=575319&postcount=17)


> R. Gerbicz
> For that record used only your 1st method with the following modification:
collect in array/vector those res values that occur maximal times as x%p and choose randomly(!) one res value from these. It gives some breath for the algorithm, but notice that you can stuck in a local min, so without several restarts you could be far from global min. I'd say the above result is not very far from optimal, but this is just my guess.

I think there are a few approaches to this.
I think you are suggesting randomly pick one that matches the res in question, randomize the others and then optimize everything using the previously defined methods.

Depending on how many primes hit the chosen res value it may be possible to do an exhaustive search for all of them(not certain but I think 10-15 would be possible). This would have the greatest chance of success I think.

I think an obvious optimization for this would be to recognize that there will be some very small primes that don't stand a chance of being changed. The sieve array could also be pre-populated with the sieve for all the other primes.

Local minima have the potential to be an issue. I need to try again with random starting points rather than just zeros. Selecting subsets that have more potential to improve to randomize seems like a decent way forward. Some form of simulated annealing might be sensible although I am not sure how to apply it in this case. 

---

#### 2021-04-06, 12:52 [henryzz](https://www.mersenneforum.org/showpost.php?p=575322&postcount=18)

@CraigLo How are you working out your probabilities? The obvious calculation is to sum the probabilities for each start point x < 0 that a gap >=xx merit starts there. However, these probabilities don't strike me as independent so summing them wouldn't be correct.

I assume that this calculation is always going to be too slow to optimize based on this. 

---

#### 2021-04-06, 16:06 [CraigLo](https://www.mersenneforum.org/showpost.php?p=575335&postcount=19)

> henryzz
> @CraigLo How are you working out your probabilities? The obvious calculation is to sum the probabilities for each start point x < 0 that a gap >=xx merit starts there. However, these probabilities don't strike me as independent so summing them wouldn't be correct.
> 
> I assume that this calculation is always going to be too slow to optimize based on this.

1. Calculate the probability that a gap >= G starts at the first point < 0.
2. Calculate the probability that a gap >= G starts at the second point < 0. A gap starting here will also include the first point so add this to the probability for the first point as well.
3. Calculate the probability that a gap >= G starts at the third point < 0. A gap starting here will also include the first and second points so add this to the probability for the first two as well.
4. Continue this for all points < 0.


When you are finished we have the probability that a point is included in a gap >= G. Every gap will include the first point. A gap will include a point at G/2 only about half the time so sieving a point at G/2 is only half as helpful as sieving a point at 0. A gap will only include a point at 3G/4 about 1/10th the time so sieving a point here is only 1/10th as helpful as sieving a point at 0.


The probabilities calculated above will change depending on the offset chosen but I think the changes will be small enough that they can be ignored. With this assumption the probabilities can be pre-computed and the optimization problem is similar to the one you are already doing.


You are currently subtracting 1 for each element sieved in the interval -G/2 to G/2 and 0 outside this region and minimizing the result.


I am suggesting we subtract the pre-computed probability for each element sieved over the interval -G to G and minimize this.


---

#### 2021-04-18, 11:08 [henryzz](https://www.mersenneforum.org/showpost.php?p=576109&postcount=20)

I have finally had time to code swapping based on probabilities of offsets being included in a gap. I have based it on the raw probabilities before accounting for offsets. I am unsure whether I need to change that although I am not sure how I would best do that as calculating the probabilities is not fast the way I am currently doing it.

This turned up the solution for a range of 220k and 440k::

```nohighlight
1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 8 0 16 32 3729
3789 0 128 4 3705 0 0 3837 0 0 0 3377 256 3879 64 3915 0 0 0 3687 0 0 0 0 0 512 0 2 0 4025 1024 0 0 0 3055
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 2048 0 0 0 0 0 0 0 0 0 0 0
2471 0 0 0 4096 0 0 495 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 2365 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1613 0 0 0 0 3942 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 1259 0 0 1277 5052 1493 0 5100 0 0 0 0 1273 0 0 1417 5004 1279 0 5364 1309 5112 5256 1547 1145 5244
1339 0 5460 5460 1589 5256 1477 0 0 5160 5460 0 1445 1355 1177 0 0 5556 0 5244 0 0 5400 0 0 5424 0 5544 0
0 0 0 0 0 0 0 0 0 0 0 1975 4920 0 0 0 0 0 4776 0 4884 2215 0 0 0 2047 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 4709 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 5423 0 0 5729 0 0
5095 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 3787 0 0 4104 0 0 0 0 0 0 0 0 0 0 0
```

I am a little concerned that this pushes the average gap size rather than the probability of a large gap. How does this perform for the stats in post #9? 

---

EOT