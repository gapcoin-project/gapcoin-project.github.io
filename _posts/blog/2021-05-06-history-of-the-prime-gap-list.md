---
layout: post
author: Graham Higgins
title: An informal history of the Prime Gap List
description: Origins and development of the computational search for first known occurrence prime gaps 
date: 2021-05-06
category: gapcoin
tags: post
---

## Introduction and background

The history of the prime gap list of today begins back in the last year of of the 20th Century when Dr. Thomas R. Nicely created a web site to curate some papers on first occurrence prime gaps that he submitted to the AMS (American Mathematical Society) and to make available an openly-accessible “electronic” version of the list of first known occurrence prime gaps.

<div class="ui raised padded container segment">
  <div class="ui two column very relaxed grid">
    <div class="column">
      <div class="ui tiny header">Dr. Thomas R. Nicely</div>
      <p>Tom Nicely began publishing lists of record prime gap data on his web site in May 1999 and maintained the lists until his death in a car accident on 11th. September 2019. Prior to his retirement, Dr. Nicely was professor of mathematics at the University of Lynchburg. The Internet Archive’s “Wayback Machine” has captured the Univerity‘s <a href="https://web.archive.org/web/20191121205013/https://www.lynchburg.edu/news/2019/09/remembering-dr-thomas-nicely-legendary-teacher-who-discovered-pentium-bug/">Remembering Dr. Thomas Nicely</a> page.</p>
    </div>
    <div class="column">
      <p>
        <img src="/img/blog/prime-gap-list-history-tom-nicely.jpg" height="240px" />
      </p>
    </div>
  </div>
</div>

The first paper is by Thomas R. Nicely and Bertil Nyman, “[First occurrence of a prime gap of 1000 or greater](https://web.archive.org/web/20000914090000/http://www.trnicely.net/gaps/gaps2.html)”, submitted 26 May 1999 to Math. Comp. Nicely’s calculations were performed during the period October, 1997, through February, 1999; Nyman’s between August, 1998, and May, 1999. The second paper is by Thomas R. Nicely, "[New maximal prime gaps and first occurrences](https://web.archive.org/web/20000914090000/http://www.trnicely.net/gaps/gaps.html)", Math. Comp. 68:227 (July, 1999), 1311-1315. [MR 99i:11004](https://www.ams.org/journals/mcom/1999-68-227/S0025-5718-99-01065-0/S0025-5718-99-01065-0.pdf). Calculations performed during the period August, 1995, through October, 1997.

### Description of the prime gap list

The following rubric, taken from [archive.org’s first capture](https://web.archive.org/web/20000914090000/http://www.trnicely.net/gaps/gaplist.html) and headlined “Last updated 3 September 2000” describes and qualifies the content of the list.

<div class="ui raised padded container segment">
  <ul style="font-size:85%">
    <li>The following table is believed to exhibit all first occurrence prime gaps conclusively established as of the date shown above.</li>
    <li>Gaps indicated in parentheses are first known occurrences likely to be, but not yet definitively established as first occurrences.</li>
    <li>Gaps indicated in square brackets are first known occurrences which are not believed to be first occurrences.</li>
    <li>Maximal gaps are marked with an asterisk (\*).</li>
    <li>All prime gaps in <math>0 < x < 1.2161 × 1016</math> have been scanned.</li>
    <li>The smallest gap whose first occurrence remains uncertain is the gap of 968.</li>
    <li>No gap exceeding 1132 has been established as a first occurrence.</li>
    <li>Nyman’s count of primes below 1016 exceeded the accepted value of <math>pi(1016)</math> by 809, a notable discrepancy. However, analysis indicates a probability of less than one in one million that this caused an error (specifically, an omission) in his compilation of prime gaps; this computation presumes a uniform distribution of false primes, and the probability of error is otherwise somewhat greater. Nicely has independently checked all gaps occurring between <math>7.2 × 1013</math> and <math>2.75 × 1015</math>.</li>
    <li>The listed discoverers and dates reflect the most accurate values known for the actual date of discovery; if this is not known, the date of publication or the date of the preprint is shown; if this is not known, an estimate is given. Some or all of the gaps occurring below 105 were almost certainly known prior to the indicated discovery, and the correct attribution of some of the other gaps below 108 is in doubt.</li>
    <li>The convention is followed here that the size <math>G</math> of a gap is the difference of its two bounding primes; consequently a gap <math>G</math> contains <math>(G  - 1)</math> consecutive composite integers (some authorities take <math>(G  - 1)</math> itself as the size of the gap).</li>
    <li>Note that the term *first occurrence prime gap* (of measure <math>G</math>) refers to that interval <math>p <= x <= p+G</math> for which (1) <math>p</math> and <math>p+G</math> are primes, (2) <math>p+t</math> is composite for each integer <math>t=1,...,G-1</math>, and (3) no smaller positive prime <math>p</math> possesses these properties. The entity might be more accurately described as the earliest or smallest occurrence of the gap <math>G</math>, but the terminology first occurrence prime gap is well established in the literature.</li>
    <li>Notification of any errors or omissions will be appreciated.</li>
  </ul>
</div>


### Rationale for a list of first occurrence prime gaps

Nicely and Nyman’s work was conducted in the context of general interest by number theorists in attempting to formalise the distribution of prime numbers. As Dr. Nicely observes: “The study of the distribution of the prime numbers among the positive integers occupies a central place in number theory.”

<div class="ui raised padded container segment" >
  <p>The number of primes up to <math>x</math>, denoted by <math>π(x)</math>, is roughly <math>x/log(x)</math> for large values of <math>x</math>; this is the celebrated <a href="https://en.wikipedia.org/wiki/Prime_number_theorem" target="_blank">Prime Number Theorem</a>. Therefore, if we randomly choose an integer near <math>x</math>, then it has about a 1 in <math>log(x)</math> chance of being prime.</p>
  <p>In other words, as we look at primes around size <math>x</math>, the average gap between consecutive primes is about <math>log(x)</math>. As <math>x</math> increases, the primes get sparser and the gap between consecutive primes tends to increase.</p>
  <p>Here are some natural questions about these gaps between prime numbers.</p>
  <p>Do the gaps always remain roughly about size <math>log(x)</math> or do we sometimes get unexpectedly large gaps and sometimes surprisingly small gaps?</p>
  <p>Can we say something about the statistical distribution of these gaps? That is, can we quantify how often the gap is between, say, <math>α log(x)</math> and <math>β log(x)</math>, given <math>0 ≤ α < β</math>?</p>
  <p>Except for the primes 2 and 3, clearly the gap between consecutive primes must be even. Does every even number occur infinitely often as a gap between consecutive primes? For example, the twin prime conjecture says that the gap 2 occurs infinitely. How frequently should we expect the occurrence of twin primes?</p>
  <p style="font-style:italic;font-size:75%">From the introduction of Kannan Soundararajan’s “Small gaps between prime numbers: the work of Goldston-Pintz-Yıldırım” <a href="https://arxiv.org/abs/math/0605696" target="_blank">Bull. Am. Math. Soc. New Series. 44 (1): 1–18</a></p>
</div>

### Context for construction of a list of first occurrence prime gaps

Dr. Nicely’s list of references provides some more details about the context - “*No general method more sophisticated than an exhaustive search is known for the determination of first occurrences and maximal prime gaps*. As in the present study, this is most efficiently done by sieving successive blocks of positive integers for primes, recording the successive differences, and thus determining directly the first occurrences and maximal gaps.”

#### Dr Tom Nicely’s table of first occurrence prime gaps

The first couple of dozen entries, as published in August 2000:

<div class="ui raised padded container segment">
  <p style="text-align:center"><img alt="Nicely’s prime gap list" src="/img/blog/prime-gap-list-history-list.png" width="75%"/></p>
</div>

And some comments and observations on the above content ...

#### Hand-generated tables

And while both Nyman’s and Nicely’s calculations were performed on Pentium series machines, there’s a *long* history, dating back at least as far as Glaisher’s dedicated efforts by hand, reported in 1877:

<div class="ui raised padded container segment">
  <div class="ui tiny header">“... by counting the number of dashes ...”</div>
  <p style="text-align:center"><a href="https://books.google.co.uk/books?id=5JY_AQAAIAAJ&pg=PA102&focus=viewport" target="_blank"><img alt="Glaisher" src="/img/blog/prime-gap-list-history-glaisher.png" width="80%" /></a><br/>
  J. W. L. Glaisher, "<a title="Glaisher PDF image on Google books" href="https://books.google.co.uk/books?id=5JY_AQAAIAAJ&pg=PA102&focus=viewport" target="_blank">On long successions of composite numbers</a>" Messenger of Mathematics 7 (1877), 102-106, 171-176</p>
</div>

And in 1934 A. E. Western provided a hand-calculated table of gaps between successive primes in [A. E. Western](https://londmathsoc.onlinelibrary.wiley.com/doi/epdf/10.1112/jlms/s1-9.4.276), "Note on the magnitude of the difference between successive primes", London Math. Soc, v.9, 1934, p.276-278 (unfortunately, Western’s data is inaccessible behind a John Wiley & Sons, Inc paywall).

#### The early digital computing era

Dr. Nicely notes that the technique of exhaustive search “has been used by Shanks, Lander and Parkin, Brent, and Young and Potler.”

Both Glaisher’s and Western’s hand-produced tables were referenced by Shanks but by 1964, the long hours of searching through primes had been devolved to the digital computer and Dr Nicely’s references echo the developments in processing over the decades:

<div class="ui raised padded container segment">
  <div class="ui two column doubling stackable grid container">
    <div class="column">
      <div class="ui tiny header">“... a rough "ball-park" estimate of where one would first find a run of a million or  more consecutive composite integers. ...”</div> 
      <p>Daniel Shanks, "<a href="https://www.ams.org/journals/mcom/1964-18-088/S0025-5718-1964-0167472-8/S0025-5718-1964-0167472-8.pdf" title="Shanks PDF, AMS">On maximal gaps between successive primes</a>" Math. Comp. 18 (1964) 646-651. MR 29:4745.</p>
      <p>In 1964, Daniel Shanks was working at the US Navy’s <a href="https://en.wikipedia.org/wiki/David_Taylor_Model_Basin" target="_blank">David Taylor Model Basin</a> (test facilities for ship design) where they had one of two <a href="https://en.wikipedia.org/wiki/UNIVAC_LARC" target="_blank">UNIVAC LARCs</a> produced. Shanks summarised the available results: “Empirically, the exact facts are known out to <math>g = 209</math> thanks to an often-quoted but still not published study of D. H. Lehmer concerning the distribution of primes out to <math>37•10<sup>6</sup></math>. Previously, less complete tables were given by Western and by Glaisher.”</p>
    </div>
    <div class="column">
      <p style="text-align:center"><a title="Public domain image via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:UNIVAC_LARC-BRL61-0959.jpg"><img width="80%" alt="UNIVAC_LARC-BRL61-0959" src="https://upload.wikimedia.org/wikipedia/commons/e/e5/UNIVAC_LARC-BRL61-0959.jpg" /></a></p>
    </div>
  </div>
</div>

<div class="ui raised padded container segment">
  <div class="ui two column doubling stackable grid container">
    <div class="column">
      <p style="text-align:center"><a title="National Institute of Standards and Technology, Public domain, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:SWAC_001.jpg"><img width="80%" alt="SWAC 001" src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a8/SWAC_001.jpg/512px-SWAC_001.jpg"></a></p>
    </div>
    <div class="column">
      <div class="ui tiny header">“... an often-quoted but still not published study  ...”</div>
      <p><a href="https://en.wikipedia.org/wiki/D._H._Lehmer" title="D.H.Lehmer" target="_blanK">D. H. Lehmer</a>, "Tables concerning the  distribution of primes up to 37 millions" 1957, <em>mimeographed</em> copy deposited in the UMT File and  <a href="https://www.ams.org/journals/mcom/1959-13-065/S0025-5718-59-99266-X/S0025-5718-59-99266-X.pdf" target="_blank">reviewed</a> (by J. L. Selfridge of IBM Research, Yorktown Heights NY) in MTAC, v.13, 1959, p.56-57</p>
      <p>The tables may well have have been produced in association with <a href="http://www.bitsavers.org/pdf/nbs/swac/SWAC_Oct53.pdf" target="_blank">a study of the primality of Mersenne numbers</a> performed on <a href="https://en.wikipedia.org/wiki/SWAC_(computer)" target="_blank">SWAC</a>, a parallel computer using a Williams tube memory and the fastest computer in existence at the time.</p>
    </div>
  </div>
</div>


<hr style="margin: 2em 4em 1em 4em; color: #eee"/>

Several references to foundational work are unavailable for casual inspection, such as D. H. Lehmer’s list, Kenneth I. Appel and J. Barkley Rosser’s “Table for Estimating Functions of Primes” and F. J. Gruenberger and G. Armerding’s, "Statistics on the first six million prime numbers".

Fortunately, in his paper, Shanks provides the first accessible version of the prime gap list - “From these results (slightly reinterpreted) we have given in Table 1 a list of maximal gaps up to <math>g=219</math>.”

<div class="ui raised padded container segment">
  <p style="text-align:center"><img alt="Shanks’ prime gap list" src="/img/blog/prime-gap-list-history-shanks.png" width="70%"/></p>
</div>

#### The supercomputer era

<div class="ui raised padded container segment">
  <div class="ui two column doubling stackable grid container">
    <div class="column">
      <div class="ui tiny header">“... a sieve technique for generating and examining gaps in primes  ...”</div>
      <p>L. J. Lander and T. R. Parkin, "<a href="" title="Lander and Parkin" target="_blank">On First Appearance of Prime Differences</a>", Math. Comp. 21 (1967) 483-488. MR 37:6237.</p>
      <p>“A  program for the CDC 6600 was written to implement a sieve technique for generating and examining gaps in primes. ... Table I for <math>1.46 x 10<sup>9</sup> <  P  <  1.096 x 10<sup>10</sup></math> presents the results obtained from this program.”</p>
      <p>Generally considered to be the first successful supercomputer, the CDC 6600 was the world's fastest computer from 1964 to 1969.</p>
    </div>
    <div class="column">
      <p style="text-align:center"><a title="Jitze Couperus, CC BY 2.0 &lt;https://creativecommons.org/licenses/by/2.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:CDC_6600.jc.jpg"><img width="512" alt="CDC 6600.jc" src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c4/CDC_6600.jc.jpg/512px-CDC_6600.jc.jpg"></a></p>
    </div>
  </div>
</div>

<hr style="margin: 2em 4em 1em 4em; color: #eee" />

Lander and Parkin‘s table of gaps in primes is clearly closer in format to Nicely’s table: 

<div class="ui raised padded container segment">
  <p>L. J. Lander and T. R. Parkin report: “In private correspondence Daniel Shanks suggested the possibility of extending Table I in [2] over the  new differences found. Accordingly, Table I shows <math>log P<sub>b</sub>/(D — l)<sup>1/2</sup></math>, with each maximal gap <math>D</math> marked with an asterisk. Maximal gaps, according to Shanks, are those larger than any preceding gap in the sequence of primes.”</p>
  <p style="text-align:center"><img alt="Lander and Parkin’s prime gap list" src="/img/blog/prime-gap-list-history-lander-and-parkin.png" width="70%"/></p>
</div>

<div class="ui raised padded container segment">
  <div class="ui two column doubling stackable grid container">
    <div class="column">
      <div class="ui tiny header">“... scanned for large gaps by an algorithm ...”</div>
      <p>Richard P. Brent, "<a href="https://www.ams.org/journals/mcom/1973-27-124/S0025-5718-1973-0330021-0/S0025-5718-1973-0330021-0.pdf" title="Brent AMS PDF" target="_blank">The first occurrence of large gaps between successive primes</a>" Math. Comp. 27:124 (1973) 959-963, MR 48#8360.</p>
      <p>“The computations were performed on an IBM 360/91 computer at the IBM T. J. Watson Research Center. ... efficiently scanned for large gaps by an algorithm”</p>
      <p>The <a href="https://en.wikipedia.org/wiki/IBM_System/360_Model_91" target="_blank">IBM System 360 Model 91</a> was the world's biggest, fastest, and most powerful computer in the mid-to-late 1960s, designed to handle high-speed data processing for scientific applications.</p>
    </div>
    <div class="column">
      <p><a title="MBlairMartin, CC BY-SA 4.0 &lt;https://creativecommons.org/licenses/by-sa/4.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:IBM_Model_91_Front_Panel.jpg"><img width="512" alt="IBM Model 91 Front Panel" src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/df/IBM_Model_91_Front_Panel.jpg/512px-IBM_Model_91_Front_Panel.jpg"></a></p>
    </div>
  </div>
</div>


<div class="ui raised padded container segment">
  <div class="ui two column doubling stackable grid container">
    <div class="column">
      <div class="ui tiny header">“... programs written on a CRAY-2 supercomputer ...”</div>
      <p>Jeff Young and Aaron Potler “<a href="https://www.ams.org/journals/mcom/1989-52-185/S0025-5718-1989-0947470-1/S0025-5718-1989-0947470-1.pdf" title="Young and Potler AMS PDF" target="_blank">First occurrence prime gaps</a>” Math. Comp. 52:185 (1989) 221-224. MR 89f:11019.</p>
      <p>“An ongoing search for first occurrence prime gaps is being carried out which extends all previous work done on this subject. To date this search has found all such gaps for primes up to <math>7.263 x 10<sup>13</sup></math>. First occurrence prime gaps had previously been known for primes less than 4.444 x 10<sup>12</sup>. Computer programs were written ... on a CRAY-2 supercomputer.”</p>
      <p>The <a href="https://en.wikipedia.org/wiki/Cray-2" title="CRAY-2" target="_blank">Cray-2</a> supercomputer was the fastest machine in the world when it was released.</p>
    </div>
    <div class="column">
      <p><a title="Rama, CC BY-SA 3.0 FR &lt;https://creativecommons.org/licenses/by-sa/3.0/fr/deed.en&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:Cray-2-IMG_0515.jpg"><img width="512" alt="Cray-2-IMG 0515" src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/78/Cray-2-IMG_0515.jpg/512px-Cray-2-IMG_0515.jpg"></a></p>
    </div>
  </div>
</div>

<hr style="margin: 2em 4em 1em 4em; color: #eee" />

Young and Potler‘s table of gaps in primes is even closer in format to Nicely’s table: 

<div class="ui raised padded container segment">
  <p>“The following table lists all the first occurrence prime gaps found. This table agrees with all previously published results (Brent and Lander &amp; Parkin). The maximal first occurrence prime gaps are marked with an asterisk (*).”</p>
  <p style="text-align:center"><img alt="Young and Potler‘s table of gaps in primes" src="/img/blog/prime-gap-list-history-young-and-potler.png" width="70%"/></p>
</div>

#### The microcomputer era


##### 1999

Young and Potler’s 1989 work was the last extension to the list of prime gaps for a decade.

Thomas R. Nicely and Bertil Lyman continued the work in the mid-1990s, distributing the search across a number of Pentium II PCs and on 26 May 1999 they submitted a(n unaccepted) report on progress to Math. Comp. --- Thomas R. Nicely and Bertil Nyman, "First occurrence of a prime gap of 1000 or greater".

Nicely successfully submitted a second paper in July of the same year, observing: “Calculations performed during the period August, 1995, through October, 1997”.


<div class="ui raised padded container segment">
  <div class="ui two column doubling stackable grid container">
    <div class="column">
      <div class="ui tiny header">“... The number of systems (most of them Pentiums) ...”</div>
      <p>Thomas R. Nicely “<a href="https://www.ams.org/journals/mcom/1999-68-227/S0025-5718-99-01065-0/S0025-5718-99-01065-0.pdf" title="Thomas R. Nicely AMS PDF" target="_blank">New maximal prime gaps and first occurrences</a>” Math. Comp. 68:227 (July, 1999), 1311-1315. MR 99i:11004.</p>
      <p>“The search for prime gaps is being carried out as part of a larger program ... All computations are being executed during slack hours on personal computers belonging to the author or assigned to the Department of Mathematics at Lynchburg College. The number of systems (most of them Pentiums) in use has averaged about fifteen since the present program began in 1993. ... Typical throughput is about 10<sup>11</sup> integers per day on a 60 MHz Pentium.”</p>
    </div>
    <div class="column">
      <p><img width="512" alt="Gateway 2000 Pentium II" src="/img/blog/prime-gap-list-history-pentium-ii.png" /></p>
    </div>
  </div>
</div>

“The search for first occurrences of prime gaps, and maximal prime gaps, is extended to 10<sup>15</sup>. New maximal prime gaps of 806 and 906 are found, and sixty-two new first occurrences are found for gaps varying in size from 676 to 906.”

“Thus all first occurrences of gaps through 674, as well as scattered first occurrences for gaps through 778, were tabulated, and all maximal prime gaps through 778 were located. In addition, Young and Potler continued their calculations to an unpublished higher level; Ribenboim [13, p. 142] credits them with the discovery of an additional maximal prime gap of 804 following the prime 90874329411493, and this was privately confirmed by Young.”


#### First online publication of a comprehensive table of first known occurrence prime gaps

In May 1999, Nicely published the complete list of first known occurrence prime gaps along with the discoverer, the year of discovery, the merit of the gap, the number of digits in the starting prime and the starting prime itself as a plaintext list in HTML. Maximal gaps were denoted with an asterisk and the status of the bounding primes (confirmed or probable). 

The prime gap list as published by Nicely in May 1999 runs to just over 500 entries. Dr. Nicely collated all of the previously-published prime gap lists (including Glaisher’s list from 1887, Western’s list from 1934, Lehmer from 1957, Appel and Rosser from 1961, Lander and Parkin from 1967, Brent from 1973 and Young and Potler from 1989) as well as the additional discoveries made by Nicely and Lyman.

<div class="ui raised padded container segment">
  <p style="text-align:center"><a href="/img/blog/prime-gap-list-history-gaplist-1999-08-20.jpg" title="Full image"><img alt="Nicely‘s table of first occurrence prime gaps" src="/img/blog/prime-gap-list-history-gaplist-1999-08-20.png" /></a></p>
</div>

##### 1999-2019 the era of collaboration

For the first couple of years after the initial publication of the electronic version of the first known prime gap list, there were only few changes to Bertil Nyman’s entries and one submission in mid-2001 from Gilles Blanchette in Montreal.

However, by February 2002, Dr Nicely had collated a large number of additions from different sources, a 1992 submission to the Letters of Journal of Recreational Mathematics by D. Baugh and F. O'Hara but mainly from a small handful of contributors: [Harvey Dubner](https://en.wikipedia.org/wiki/Harvey_Dubner) who had been in contact with Nicely since 1996, [Kenneth Conrow](https://www.friendsjournal.org/kenneth-conrow/) of Kansas State University and a number of others working privately - Jim Fougeron, Kjell-Olav Grøndalen, Nuutti Kuosa and Luis Rodriguez.

Dubner and Conrow (mainly Dubner) added over 2000 entries to the the list, rendering it unwieldy as a single publication and Nicely created a second list [“First known occurrence prime gaps (exceeding 1132)”](https://web.archive.org/web/20020201204448/http://www.trnicely.net/gaps/gaplist2.html).

By early 2003, the list of first known occurrence prime gaps had been split into five parts; the number of entries had grown to 5550 (with Dubner and Nicely contributing the majority, supported by contributions in the > 9999 range by R.Athale and J.L.G. Pardo) with the largest gap discovered 233822, following a prime of 5878 digits in length.

Additional work and contributions continued, by August of 2003 Jens Kruse Andersen has contributed over 1500 records of gaps > 11999 and the the number of separate sub-lists had grown to eight. Later that year, Hans Rosenthal joined Andersen in making significant contributions to the upper reaches and the number of sub-lists was extended to ten to cover gaps exceeding 19999.

By the middle of the following year, there were fifteen sub-lists, extending to “1000000 to 999999998” with a couple dozen contributors now emailing submissions to Nicely for inclusion in the list.

Eventually, the number of sub-lists grew to twenty-one and in early 2016 Dr. Nicely collated them all into a single file: “The complete, untruncated listing of all presently known first occurrence and first known occurrence prime gaps is available as [allgaps.dat](https://web.archive.org/web/20160303183217/http://www.trnicely.net/gaps/allgaps.dat) (9 MB), a Win/DOS text file describing one gap per line, in the standard format.”

At this stage, the table of first known prime occurrence prime gaps had 84,629 entries and the largest gap discovered was 4680156, following the prime number <math>230077#/2229464046810 - 3131794</math> (99750 digits in length), discovered by Martin Raab in 2016.

##### Gapcoin contributions

The first contribution from the Gapcoin network (as recorded by archive.org) appears in the list of first known occurrence prime gaps 4000-5998 for [April 2015](https://web.archive.org/web/20150404184348/http://www.trnicely.net/gaps/g4k.html) which include 519 entries credited to Gapcoin.

It’s doubtful that any of these entries filled any gaps in new first known occurrences and far more likely they were improvements in merit of existing first known occurrences, such as that for the gap 4622.

The merit of the 2015 Gapcoin discovery was 24.24 whereas the existing entry, discovered by Helmut Spielauer in 2014, was of merit 24.03:

<p><pre style="font-size:70%"><code class="diff">+  4622  C?C Gapcoin  2014  24.24    83  64051350512724708215555131043627811252980984635815736414841611370833453628776789829
-  4622  C?C Spielaur 2012  24.03    84  334636025237567784523020021022819575015790229177281468713072013451084022710943448127</code></pre></p>

Spielaur’s 2014 entry is an improved merit over Torbjörn Alm‘s 2004 discovery

<p><pre style="font-size:70%"><code class="diff">+  4622  C?C Spielaur 2012  24.03    84  334636025237567784523020021022819575015790229177281468713072013451084022710943448127
-  4622  C?C TorAlmJA 2004  20.69    98  10298668143351087376700838989365136734283548190197588211113508946614970440606700979807555048843691</code></pre></p>

And that itself is an improvement in merit over H. Dubner’s 2002 discovery:

<p><pre style="font-size:60%"><code class="diff">+  4622  C?C TorAlmJA 2004  20.69    98  10298668143351087376700838989365136734283548190197588211113508946614970440606700979807555048843691
-  4622  C?C H.Dubner 2002  15.95   126  680941728113890909988182383034816373412341103196700637318249591357089162624656291902634885080827820797742072433863223714372631</code></pre></p>

##### 2019 end of an era

On Wednesday, September 11, 2019, Dr. Thomas R. Nicely died as a result of injuries sustained in a car accident. In the last update of August 2019, Dr. Nicely offered the following summary of the list of known first occurrence prime gaps: 

<div class="ui raised padded container segment">
  <p>“All prime gaps in <math>0 < x < 2<sup>64</sup></math> have now been analyzed, where 2<sup>64</sup> = 18446744073709551616, the smallest positive integer requiring more than 64 bits in its binary representation (i.e., not representable in C as a <code>uint64_t</code>).</p>

  <p>The final push from 18446744000000000000 to <math>2<sup>64</sup></math> was carried out by the combined efforts of PGS members Jerry LaGrou, Dana Jacobsen, Robert Smith, and Robert Gerbicz. No gap exceeding 898 was found in this interval.</p>

  <p>Calculations beyond 2<sup>64</sup> will be hindered by the fact that their binary representations require more than 64 bits, exceeding the capacity of the hardware registers in most present-day numeric processor FPUs (supercomputers excepted) and forcing the computations into software. This can be expected to reduce speed and throughput by one or two orders of magnitude.</p>

  <p>The upper bound of exhaustive analysis of gaps has been extended successively, as follows. For the most recent results, see the Prime Gap Searches project at the Mersenne Forum (see PGS in the Bibliography for a list of the participants). Most of the calculations beyond 16000e15 were carried out by Thomas Ritschel.”</p>

</div>

The last prime gap list published by Nicely ran to 96,476 entries with the largest gap being 6582144 following the prime number <math>499973#/30030 - 4509212</math> (216841 digits in length), this time discovered by Martin Raab in 2017.


## 2020 beginning of a new era of community curation

Since 2013, members of the Mersenne Forum’s Prime Gap Search Group (PGS) had been communicating and collaborating with Dr. Nicely in checking and validating submissions to the prime gap list, so it was natural that the PGS would concern itself with the preservation of Dr. Nicely’s work and its contribution to number theory.

<div class="ui raised padded container segment">
  <div class="ui two column doubling stackable grid container">
    <div class="column">
      <div class="ui tiny header">“... continue the prime gap saving ...”</div>
      <p>“Robert G is right to say this needs to be automated. All that is needed is a simple upload mechanism and checking program with a web page showing the record gaps and a download facility for reports. All we need is a person to create the script.” <i>Rob Smith, in <a href="https://www.mersenneforum.org/showpost.php?p=529530&postcount=115" target="_blank">a post to the Mersenne Forum Prime Gap Search Group</a>.</i></p>
    </div>
    <div class="column">
      <p><img width="512" alt="Prime gap list Github repository" src="/img/blog/prime-gap-list-history-pgs-01.png" /></p>
    </div>
  </div>
</div>

#### A Github repository curating the list of first known occurrence prime gaps

The result of the exercise was the creation of a [Github repository](https://github.com/primegap-list-project) which preserved the successive publications of Dr. Nicely’s `allgaps.dat` list as successive commits to the repository, transcribed as SQL insert statements, creating [a downloadable SQLite3-compatible database](https://raw.githubusercontent.com/primegap-list-project/prime-gap-list/server/allgaps.sql) for convenient analysis. 

<div class="ui raised padded container segment">
  <p style="text-align:center"><img alt="Screenshot of the prime gap list Github repository" src="/img/blog/prime-gap-list-history-github-repository.png" width="100%"/></p>
</div>

One contextually-valuable aspect of open source repository technology is that successive changes to the content are made clearly visible, in this instance preserving the credit for previous contributions which would otherwise be lost with a continually-updated list:

<div class="ui raised padded container segment">
  <p style="text-align:center"><img alt="Screenshot of the prime gap list Github repository" src="/img/blog/prime-gap-list-history-allgaps-sql-2019-01-15.png" width="100%"/></p>
</div>



The preservation of [the earlier HTML pages](https://web.archive.org/web/20000820091337/http://www.trnicely.net/index.html) is devolved to archive.org

#### An automated checking and submission service

Subsquently, Seth Troisi of the PGS created an online service for the submission, automatic checking and recording of (those successful) candidate entries to the list of first known occurrence prime gaps

<div class="ui raised padded container segment">
  <div class="ui two column doubling stackable grid container">
    <div class="column">
      <div class="ui tiny header">“... verify records and automatically upload them ...”</div>
      <p>“I made a new website to verify records and automatically upload them to github. The first page performs some validity checks (merit &gt; existing, prime &lt; 10,000 digits) After you upload you'll see "1 Queued ... &lt;data&gt;" If you click the Watch Queue you can see it testing (if it's a larger record) and the results of previous tests. I only do PRP test for the endpoints. After the record is verified it’s immediately uploaded to the prime-gap-list github”<i>Seth Troisi, in <a href="https://www.mersenneforum.org/showpost.php?p=538934&postcount=5" target="_blank">a post to the Mersenne Forum Prime Gap Search Group</a></i></p>
    </div>
    <div class="column">
      <p><img width="512" alt="Screenshot of Seth Troisi’s online submission checking form" src="/img/blog/prime-gap-records-submission-service.png" /></p>
    </div>
  </div>
</div>

#### Still going strong

The current extent of the prime gap list is 101894 entries and the majority of the activity is concerned with improving merits but Martin Raab is still contributing extremely large gaps and has recently announced that he is working on a couple of 3M+ gaps.

<div class="ui raised padded container segment">
  <p style="text-align:center"><img alt="prime gap list as SQL inserts" src="/img/blog/prime-gap-list-history-pgs-april-may-2021.png" width="100%"/></p>
</div>

<div class="ui raised padded container segment">
  <p style="text-align:center"><img alt="prime gap list as SQL inserts" src="/img/blog/prime-gap-list-history-allgaps-sql-2021-04-15.png" width="100%"/></p>
</div>

I’d like to believe that the current community curation of the table of first known occurrence prime gaps both reflects and meets the standards set and maintained for so many years by generations of contributors and particularly by Dr. Thomas Ray Nicely. Ave, Tom.

---
