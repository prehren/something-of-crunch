---
title: "Most Cited Authors on the WoS: Broad vs. Narrow Influence"
date: 2024-11-19
---

Not all authors are equally influential in all areas of philosophy (deep insight, I know). I thought I’d use the WoS citation data I collected (used [here](https://prehren.github.io/something-of-crunch/2024/11/13/top-wos-authors.html) to generate a ranking of the most cited authors in philosophy) to investigate this a little more concretely and quantitatively for some of philosophy’s most influential figures. To do so, I assigned journals to the five main sub-field clusters listed on PhilPapers (History of Western Philosophy = HoWP; LEM&M; Philosophy of Science, Logic and Mathematics = SL&M; Philosophical Traditions; Value Theory). A journal counts as a specialty journal in one of these clusters if more than half of the articles (for which there was at least one sub-field cluster available on PhilPapers) published in that journal since 1975 fell into that sub-field cluster. For each author, I then calculated the average proportion (averaged across five-year bins; see here) of citations received in each journal, ranked authors based on these proportions for each journal, and then calculated the author’s median rank for each of the five sub-field clusters.

(Throughout this post, I’m assuming that these rankings are a useful measure of influence: the higher relative to other authors the proportion of citations received by an author, the more influential the author’s work. This is one of the standard assumptions of citation analysis.)

Figure 1 shows the results for the first top 100 ranked authors. (To generate the heat map, I log-transformed the median ranks to alleviate these data’s right skew and make color differences towards the lower end of the data more noticeable. The numbers superimposed on each tile show the _untransformed_ median ranks).

![Figure 1. Median rank of the top 100 authors by journal sub-field cluster.]({{site.url}}/something-of-crunch/assets/images/2024-11-19/fig1NEW.png){: width="100%"}
<p style="text-align:center; font-size: 0.85em; padding-right: 30px; padding-left: 30px;">Figure 1. Median rank of the top 100 authors by journal sub-field cluster.</p>
<br>

Let’s start with Heidegger, the overall #1. Heidegger’s median rank for the Philosophical Traditions sub-field cluster (made up of the areas African/Africana Philosophy; Asian Philosophy; Continental Philosophy; European Philosophy; and Philosophy of the Americas) is 6.5, _by far_ the highest out of all authors. (Consider what this means for a moment: If you pick a random Philosophical Traditions journal, then Heidegger will be ranked seventh or higher in that journal at least 50% of the time. That’s insane.) In contrast, Heidegger seems to have been rather less influential (though still influential, of course, which is to be expected given he is the overall #1) in other sub-field clusters. Heidegger’s next highest median rank (HoWP) is more than four times lower than his rank for Philosophical Traditions; for SL&M and LEM&M, Heidegger does not even crack the top 200.

By the same standard (highest median rank is at least four times lower than the next highest median rank), other authors in the top 100 whose influence in one sub-field cluster (far) outstrips their influence in other sub-field clusters are David Lewis (LEM&M); John Rawls, Ronald Dworkin, Peter Singer and Amartya Sen (Value Theory); and Thomas Kuhn (SL&M). If we relax the standard a bit (highest median rank is at least three times lower than the next highest median rank), then this adds Jacques Derrida, Maurice Merleau-Ponty, Paul Ricoeur and Emmanuel Levinas (Philosophical Traditions); Timothy Williamson and Fred Dretske (LEM&M); and Robert Nozick (Value Theory) to the list.

Compare this to a figure like Kant (the overall #2). The difference between Kant’s highest median rank (9 for HoWP) and the next highest median rank (11 for Value Theory) is ~22%, much less pronounced than what we found for Heidegger, Lewis and Rawls et al.

So far, I have been discussing authors whose influence in _one_ sub-field cluster outstrips their influence in _all_ other sub-field clusters. However, an author might also have been (much) more influential in two or more sub-field clusters than in one or more of the other sub-field clusters. Conversely, even an author who’s been (much) more influential in one sub-field cluster than in the others might still have had a similar amount of influence in these other clusters. What would be useful, then, is to also have a look at the spread of the median ranks for different authors. I therefore calculated for each author in the top 100 the range [max(rank)-min(rank)] of their median ranks. Figure 2 shows the results.

![Figure 2. Range of median ranks for top 100 authors.]({{site.url}}/something-of-crunch/assets/images/2024-11-19/fig2NEW.png){: width="90%"}
<p style="text-align:center; font-size: 0.85em; padding-right: 30px; padding-left: 30px;">Figure 2. Range of median ranks for top 100 authors.</p>
<br>

Two quick observations. At the low end of the y-axis, Kant and Wittgenstein stand out: Both have been very influential (#2 and #10 overall, respectively), and the amount of influence they’ve had during the last 50 years seems to have been roughly similar across philosophy’s five major sub-field clusters. I think I’ve once read somewhere that Kant was unique among influential figures in the history of philosophy for the breadth of his influence. These results would seem to suggest otherwise.

Second, there is something of a cluster of authors towards the high end of the y-axis, consisting of Søren Kierkegaard, Jean-Jacques Rousseau, Vladimir Lenin (yes, Lenin is in the top 100), Ernst Cassirer, Jacques Lacan, Giorgio Agamben, Walter Benjamin, Alain Badiou, Jacques Ranciere and Axel Honneth. What I find curious about this cluster is that everyone in it (except perhaps for Lenin) is from Continental Europe. Indeed, this looks to be true more generally: The median rank ranges of authors from Continental Europe tend to be larger than for authors from elsewhere (mostly the UK and North America).

I must admit I’m not quite sure what’s going on here. An author’s region of birth correlates with the sub-field cluster in which the author has been most influential (i.e., where their median rank is highest). Figure 3 shows that for authors from Continental Europe, the most influential sub-field cluster tends to be Philosophical Traditions, while for authors from the UK and North America, the most influential sub-field cluster tends to be SL&M or LEM&M. (Value Theory and HoWP seem to be somewhere in between.) If authors who are most influential in Philosophical Traditions tend to be less influential in SL&M and LEM&M (a reasonable assumption; see Figure 4), then it would make sense that the ranges associated with these author’s median ranks will tend to be quite large. However, this only explains the clustering we see in Figure 3 if the reverse is not true–that is, if authors who are most influential in LEM&M and/or SL&M are _not_ generally much less influential in Philosophical Traditions. This strikes me as implausible (this might just reflect my own ignorance, though), but I’m not sure how else to explain these results.

![Figure 3. Range of median ranks for top 100 authors with colors indicating each author's most influential sub-field cluster(s).]({{site.url}}/something-of-crunch/assets/images/2024-11-19/fig3NEW.png){: width="90%"}
<p style="text-align:center; font-size: 0.85em; padding-right: 30px; padding-left: 30px;">Figure 3. Range of median ranks for top 100 authors with colors indicating each author's most influential sub-field cluster(s).</p>
<br>

Does influence in one sub-field cluster predict influence in another? Yes. Figure 4 shows pair-wise correlations between median ranks in different sub-field clusters [only statistically significant correlations (_p_ < 0.05) are shown]. Authors who are ranked highly in LEM&M also tend to rank highly in in SL&M (and vice versa); authors who tend to rank highly in the HoWP also tend to rank highly in Philosophical Traditions (and vice versa). Both are strong correlations: the correlation coefficients hover around 0.7. No surprises there. Furthermore, influence in Value Theory is associated with influence in HoWP and Philosophical Traditions. The weakest significant and the only negative correlation is between Philosophical Traditions and LEM&M: more influence in Philosophical Traditions predcits less influence in the LEM&M-ing fields (and vice versa). To be honest, I would have expected this last correlation to be stronger, but what do I know.

![Figure 4. Pair-wise correlations between median ranks in different sub-field clusters.]({{site.url}}/something-of-crunch/assets/images/2024-11-19/fig4NEW.png){: width="50%"}
<p style="text-align:center; font-size: 0.85em; padding-right: 30px; padding-left: 30px;">Figure 4. Pair-wise correlations between median ranks in different sub-field clusters.</p>
<br>

To end, this is what the overall top 100 (102 because of ties) looks like if I also cluster by sub-field cluster (i.e., instead of averaging the proportions of citations received by each author in each journal right away, I first calculate the mean of these proportions for each sub-field cluster individually and only then average the resulting averages):

1\.&nbsp;&nbsp;&nbsp;&nbsp;I Kant (0.592%)\
2\.&nbsp;&nbsp;&nbsp;&nbsp;M Heidegger (0.556%)\
3\.&nbsp;&nbsp;&nbsp;&nbsp;J Derrida (0.36%)\
4\.&nbsp;&nbsp;&nbsp;&nbsp;E Husserl (0.351%)\
5\.&nbsp;&nbsp;&nbsp;&nbsp;Aristotle (0.295%)\
6\.&nbsp;&nbsp;&nbsp;&nbsp;M Foucault (0.265%)\
7\.&nbsp;&nbsp;&nbsp;&nbsp;D Lewis (0.264%)\
8\.&nbsp;&nbsp;&nbsp;&nbsp;GWF Hegel (0.252%)\
9\.&nbsp;&nbsp;&nbsp;&nbsp;K Marx (0.249%)\
10\.&nbsp;&nbsp;&nbsp;&nbsp;G Deleuze (0.237%)\
11\.&nbsp;&nbsp;&nbsp;&nbsp;J Rawls (0.206%)\
12\.&nbsp;&nbsp;&nbsp;&nbsp;D Hume (0.196%)\
13\.&nbsp;&nbsp;&nbsp;&nbsp;F Nietzsche (0.192%)\
14\.&nbsp;&nbsp;&nbsp;&nbsp;Plato (0.183%)\
15\.&nbsp;&nbsp;&nbsp;&nbsp;J Habermas (0.181%)\
16\.&nbsp;&nbsp;&nbsp;&nbsp;JP Sartre (0.177%)\
17\.&nbsp;&nbsp;&nbsp;&nbsp;W Quine (0.165%)\
18\.&nbsp;&nbsp;&nbsp;&nbsp;B Russell (0.154%)\
18\.&nbsp;&nbsp;&nbsp;&nbsp;L Wittgenstein (0.154%)\
20\.&nbsp;&nbsp;&nbsp;&nbsp;M Merleau Ponty (0.151%)\
21\.&nbsp;&nbsp;&nbsp;&nbsp;P Ricoeur (0.148%)\
22\.&nbsp;&nbsp;&nbsp;&nbsp;J Dewey (0.142%)\
23\.&nbsp;&nbsp;&nbsp;&nbsp;E Levinas (0.141%)\
24\.&nbsp;&nbsp;&nbsp;&nbsp;J Piaget (0.138%)\
25\.&nbsp;&nbsp;&nbsp;&nbsp;H Arendt (0.131%)\
26\.&nbsp;&nbsp;&nbsp;&nbsp;D Davidson (0.127%)\
26\.&nbsp;&nbsp;&nbsp;&nbsp;R Descartes (0.127%)\
28\.&nbsp;&nbsp;&nbsp;&nbsp;T Hobbes (0.126%)\
29\.&nbsp;&nbsp;&nbsp;&nbsp;H Putnam (0.122%)\
29\.&nbsp;&nbsp;&nbsp;&nbsp;GW Leibniz (0.122%)\
31\.&nbsp;&nbsp;&nbsp;&nbsp;T Aquinas (0.112%)\
32\.&nbsp;&nbsp;&nbsp;&nbsp;K Popper (0.107%)\
33\.&nbsp;&nbsp;&nbsp;&nbsp;S Kripke (0.104%)\
33\.&nbsp;&nbsp;&nbsp;&nbsp;G Frege (0.104%)\
35\.&nbsp;&nbsp;&nbsp;&nbsp;T Adorno (0.099%)\
36\.&nbsp;&nbsp;&nbsp;&nbsp;T Williamson (0.097%)\
37\.&nbsp;&nbsp;&nbsp;&nbsp;J Searle (0.093%)\
37\.&nbsp;&nbsp;&nbsp;&nbsp;M Nussbaum (0.093%)\
37\.&nbsp;&nbsp;&nbsp;&nbsp;R Rorty (0.093%)\
40\.&nbsp;&nbsp;&nbsp;&nbsp;JS Mill (0.092%)\
40\.&nbsp;&nbsp;&nbsp;&nbsp;HG Gadamer (0.092%)\
42\.&nbsp;&nbsp;&nbsp;&nbsp;W James (0.091%)\
43\.&nbsp;&nbsp;&nbsp;&nbsp;B Williams (0.09%)\
44\.&nbsp;&nbsp;&nbsp;&nbsp;T Nagel (0.089%)\
44\.&nbsp;&nbsp;&nbsp;&nbsp;C Peirce (0.089%)\
46\.&nbsp;&nbsp;&nbsp;&nbsp;A Goldman (0.088%)\
47\.&nbsp;&nbsp;&nbsp;&nbsp;J Locke (0.087%)\
48\.&nbsp;&nbsp;&nbsp;&nbsp;K Fine (0.085%)\
49\.&nbsp;&nbsp;&nbsp;&nbsp;R Carnap (0.082%)\
49\.&nbsp;&nbsp;&nbsp;&nbsp;J Mc Dowell (0.082%)\
49\.&nbsp;&nbsp;&nbsp;&nbsp;A Rand (0.082%)\
52\.&nbsp;&nbsp;&nbsp;&nbsp;T Kuhn (0.081%)\
53\.&nbsp;&nbsp;&nbsp;&nbsp;J Fodor (0.08%)\
54\.&nbsp;&nbsp;&nbsp;&nbsp;S Kierkegaard (0.079%)\
54\.&nbsp;&nbsp;&nbsp;&nbsp;D Chalmers (0.079%)\
56\.&nbsp;&nbsp;&nbsp;&nbsp;A Plantinga (0.076%)\
56\.&nbsp;&nbsp;&nbsp;&nbsp;S Freud (0.076%)\
58\.&nbsp;&nbsp;&nbsp;&nbsp;W Benjamin (0.075%)\
59\.&nbsp;&nbsp;&nbsp;&nbsp;V Lenin (0.074%)\
60\.&nbsp;&nbsp;&nbsp;&nbsp;C Wright (0.069%)\
60\.&nbsp;&nbsp;&nbsp;&nbsp;B Van Fraassen (0.069%)\
60\.&nbsp;&nbsp;&nbsp;&nbsp;R Nozick (0.069%)\
60\.&nbsp;&nbsp;&nbsp;&nbsp;G Agamben (0.069%)\
64\.&nbsp;&nbsp;&nbsp;&nbsp;M Dummett (0.068%)\
64\.&nbsp;&nbsp;&nbsp;&nbsp;C Taylor (0.068%)\
64\.&nbsp;&nbsp;&nbsp;&nbsp;G Priest (0.068%)\
67\.&nbsp;&nbsp;&nbsp;&nbsp;D Dennett (0.067%)\
67\.&nbsp;&nbsp;&nbsp;&nbsp;G Harman (0.067%)\
67\.&nbsp;&nbsp;&nbsp;&nbsp;I Hacking (0.067%)\
67\.&nbsp;&nbsp;&nbsp;&nbsp;P Strawson (0.067%)\
71\.&nbsp;&nbsp;&nbsp;&nbsp;P Guyer (0.065%)\
72\.&nbsp;&nbsp;&nbsp;&nbsp;D Pritchard (0.064%)\
72\.&nbsp;&nbsp;&nbsp;&nbsp;D Armstrong (0.064%)\
72\.&nbsp;&nbsp;&nbsp;&nbsp;A Wood (0.064%)\
75\.&nbsp;&nbsp;&nbsp;&nbsp;C Korsgaard (0.062%)\
75\.&nbsp;&nbsp;&nbsp;&nbsp;P Kitcher (0.062%)\
77\.&nbsp;&nbsp;&nbsp;&nbsp;R Dworkin (0.061%)\
78\.&nbsp;&nbsp;&nbsp;&nbsp;D Parfit (0.06%)\
78\.&nbsp;&nbsp;&nbsp;&nbsp;P Singer (0.06%)\
78\.&nbsp;&nbsp;&nbsp;&nbsp;P Van Inwagen (0.06%)\
81\.&nbsp;&nbsp;&nbsp;&nbsp;A Einstein (0.059%)\
81\.&nbsp;&nbsp;&nbsp;&nbsp;D Walton (0.059%)\
83\.&nbsp;&nbsp;&nbsp;&nbsp;A Sen (0.058%)\
83\.&nbsp;&nbsp;&nbsp;&nbsp;N Goodman (0.058%)\
85\.&nbsp;&nbsp;&nbsp;&nbsp;R Stalnaker (0.057%)\
85\.&nbsp;&nbsp;&nbsp;&nbsp;T Scanlon (0.057%)\
85\.&nbsp;&nbsp;&nbsp;&nbsp;J Butler (0.057%)\
88\.&nbsp;&nbsp;&nbsp;&nbsp;E Sosa (0.056%)\
88\.&nbsp;&nbsp;&nbsp;&nbsp;J Kim (0.056%)\
88\.&nbsp;&nbsp;&nbsp;&nbsp;JJ Rousseau (0.056%)\
88\.&nbsp;&nbsp;&nbsp;&nbsp;J Ranciere (0.056%)\
92\.&nbsp;&nbsp;&nbsp;&nbsp;GE Moore (0.055%)\
93\.&nbsp;&nbsp;&nbsp;&nbsp;M Friedman (0.054%)\
93\.&nbsp;&nbsp;&nbsp;&nbsp;F Dretske (0.054%)\
93\.&nbsp;&nbsp;&nbsp;&nbsp;H Frankfurt (0.054%)\
96\.&nbsp;&nbsp;&nbsp;&nbsp;T Burge (0.053%)\
96\.&nbsp;&nbsp;&nbsp;&nbsp;J Hintikka (0.053%)\
98\.&nbsp;&nbsp;&nbsp;&nbsp;F Jackson (0.052%)\
99\.&nbsp;&nbsp;&nbsp;&nbsp;J Raz (0.051%)\
99\.&nbsp;&nbsp;&nbsp;&nbsp;M Weber (0.051%)\
99\.&nbsp;&nbsp;&nbsp;&nbsp;E Cassirer (0.051%)\
102\.&nbsp;&nbsp;&nbsp;&nbsp;N Chomsky (0.05%)\
102\.&nbsp;&nbsp;&nbsp;&nbsp;R Swinburne (0.05%)\
102\.&nbsp;&nbsp;&nbsp;&nbsp;H Bergson (0.05%)\
102\.&nbsp;&nbsp;&nbsp;&nbsp;A Mac Intyre (0.05%)\
102\.&nbsp;&nbsp;&nbsp;&nbsp;JL Nancy (0.05%)\
102\.&nbsp;&nbsp;&nbsp;&nbsp;C Hempel (0.05%)

On the whole, this top 100 is quite similar to [the original top 100](https://prehren.github.io/something-of-crunch/2024/11/13/top-wos-authors.html). A few differences I noticed are that Kant is now #1; David Lewis moved up considerably (from #12 to #7); and Wittgenstein and Nietzsche are out of the top 10. However, given that all of these changes are due to rather small changes in the underlying mean percentages, I don't think these differences between the two lists are all that meaningful.
