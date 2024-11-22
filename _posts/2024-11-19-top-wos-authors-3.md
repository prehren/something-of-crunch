---
title: "Most Cited Authors on the WoS: Broad vs. Narrow Influence"
date: 2024-11-19
---

Not all authors are equally influential in all areas of philosophy (deep insight, I know). I thought I’d use the WoS citation data I collected (used [here](https://prehren.github.io/something-of-crunch/2024/11/13/top-wos-authors.html) to generate a ranking of the most cited authors in philosophy) to investigate this a little more concretely and quantitatively for some of philosophy’s most influential figures. To do so, I assigned journals to the five main sub-field clusters listed on PhilPapers (History of Western Philosophy = HoWP; LEM&M; Philosophy of Science, Logic and Mathematics = SL&M; Philosophical Traditions; Value Theory). A journal counts as a specialty journal in one of these clusters if more than half of the articles (for which there was at least one sub-field cluster available on PhilPapers) published in that journal since 1975 fell into that sub-field cluster. For each author, I then calculated the average proportion (averaged across five-year bins; see here) of citations received in each journal, ranked authors based on these proportions for each journal, and then calculated the author’s median rank for each of the five sub-field clusters.

(Throughout this post, I’m assuming that these rankings are a useful measure of influence: the higher relative to other authors the proportion of citations received by an author, the more influential the author’s work. This is one of the standard assumptions of citation analysis.)

Figure 1 shows the results for the first top 100 ranked authors. (To generate the heat map, I log-transformed the median ranks to alleviate these data’s right skew and make color differences towards the lower end of the data more noticeable. The numbers superimposed on each tile show the _untransformed_ median ranks).

![Figure 1. Median rank of the top 100 authors by journal sub-field cluster.]({{site.url}}/something-of-crunch/assets/images/2024-11-19/fig1.png){: width="100%"}
<p style="text-align:center; font-size: 0.85em; padding-right: 30px; padding-left: 30px;">Figure 1. Median rank of the top 100 authors by journal sub-field cluster.</p>
<br>

Let’s start with Heidegger, the overall #1. Heidegger’s median rank for the Philosophical Traditions sub-field cluster (made up of the areas African/Africana Philosophy; Asian Philosophy; Continental Philosophy; European Philosophy; and Philosophy of the Americas) is 6.5, _by far_ the highest out of all authors. (Consider what this means for a moment: If you pick a random Philosophical Traditions journal, then Heidegger will be ranked seventh or higher in that journal at least 50% of the time. That’s insane.) In contrast, Heidegger seems to have been rather less influential (though still influential, of course, which is to be expected given he is the overall #1) in other sub-field clusters. Heidegger’s next highest median rank (HoWP) is more than four times lower than his rank for Philosophical Traditions; for SL&M and LEM&M, Heidegger does not even crack the top 200.

By the same standard (highest median rank is at least four times lower than the next highest median rank), other authors in the top 100 whose influence in one sub-field cluster (far) outstrips their influence in other sub-field clusters are David Lewis (LEM&M); John Rawls, Ronald Dworkin, Peter Singer and Amartya Sen (Value Theory); and Thomas Kuhn (SL&M). If we relax the standard a bit (highest median rank is at least three times lower than the next highest median rank), then this adds Jacques Derrida, Maurice Merleau-Ponty and Paul Ricoeur (Philosophical Traditions); Timothy Williamson and Fred Dretske (LEM&M); and Robert Nozick (Value Theory) to the list.

Compare this to a figure like Kant (the overall #2). The difference between Kant’s highest median rank (9 for HoWP) and the next highest median rank (11 for Value Theory) is ~22%, much less pronounced than what we found for Heidegger, Lewis and Rawls et al.

So far, I have been discussing authors whose influence in _one_ sub-field cluster outstrips their influence in _all_ other sub-field clusters. However, an author might also have been (much) more influential in two or more sub-field clusters than in one or more of the other sub-field clusters. Conversely, even an author who’s been (much) more influential in one sub-field cluster than in the others might still have had a similar amount of influence in these other clusters. What would be useful, then, is to also have a look at the spread of the median ranks for different authors. I therefore calculated for each author in the top 100 the range [max(rank)-min(rank)] of their median ranks. Figure 2 shows the results.

![Figure 2. Range of median ranks for top 100 authors.]({{site.url}}/something-of-crunch/assets/images/2024-11-19/fig1.png){: width="100%"}
<p style="text-align:center; font-size: 0.85em; padding-right: 30px; padding-left: 30px;">Figure 2. Range of median ranks for top 100 authors.</p>
<br>






