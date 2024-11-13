---
title: "Co-authorship in Philosophy: Now and Then"
date: 2023-12-20
---

In some disciplines (e.g., psychology; the natural sciences), papers commonly have more than one author. Not so much in philosophy. In 2021, 83.5% of philosophy articles were single-authored, 12.2% of philosophy were co-authored and only 4.3% had more than two authors (see [here](https://prehren.github.io/something-of-crunch/2023/12/11/generalist-journals.html) for a description of the data these numbers are based on).

I find this a little odd, given how often I’ve heard it stressed that bouncing one’s ideas of other (critical) philosophers and honestly engaging with their feedback and criticism is a crucial part of doing philosophy well. If so, then wouldn’t it often make sense to just write papers with other philosophers?

A while ago, someone at a workshop I was at suggested that philosophy has in fact become more collaborative in recent decades. Is this true? In Figure 1, I plot the proportions of philosophy articles with 1, 2, 3, 4 and 5 or more authors since 1975.

![Figure 1. Proportion of philosophy articles with 1, 2, 3, 4 and 5 or more authors since 1975.]({{site.url}}/something-of-crunch/assets/images/2023-20-12/figure1.png)
<p style="text-align:center; font-size: 0.85em; padding-right: 30px; padding-left: 30px;">Figure 1. Proportion of philosophy articles with 1, 2, 3, 4 and 5 or more authors since 1975.</p>
<br>

I also calculated the journal average number of authors for articles published since 1975. Figure 2 shows the results, along with the range (that is, the range of values for the mean number of authors in all journals per year), standard deviation and 95% confidence intervals.

![Figure 2. Journal average number of authors since 1975.]({{site.url}}/something-of-crunch/assets/images/2023-20-12/figure2.png)
<p style="text-align:center; font-size: 0.85em; padding-right: 30px; padding-left: 30px;">Figure 2. Journal average number of authors since 1975.</p>
<br>

Even though the vast majority of philosophy articles today are still single-authored, philosophy has indeed become somewhat more collaborative (in terms of the number of authors on published philosophy papers). The percentage of single-authored philosophy articles has fallen from 96.5% to 83.5%. Likewise, the journal average number of authors has increased since 1975, from M = 1.04 to M = 1.21.

What accounts for/explains this increase? Here are a few ideas:

1. _Interdisciplinary journals:_ The increase in the number of co-authors on philosophy articles since 1975 is due to work published in interdisciplinary journals rather than in ‘pure’ philosophy journals.
2. _Journals outside the mainstream:_ The increase in the number of co-authors on philosophy articles since 1975 is not a phenomenon of mainstream academic philosophy.
3. _Empirical research:_ The increase in the number of co-authors on philosophy articles since 1975 is owed to the fact that philosophy journals are increasingly publishing original empirical research.
4. _Different sub-fields of philosophy:_ Different sub-fields of philosophy have different norms when it comes to co-authorship, and so the increase in the number of co-authors on philosophy articles since 1975 reflects only some sub-fields, not all of philosophy.

How to investigate these suggestions? 1., 2. and 4. are fairly straight-forward. For 1., I used the [Web of Science’s research areas](https://images.webofknowledge.com/images/help/WOS/hp_research_areas_easca.html) to divide journals into _pure philosophy_ and _interdisciplinary_. A journal is a pure philosophy journals if Philosophy is given as its one and only research area. All other journals, I count as interdisciplinary (note that all of these journals still have Philosophy listed as one of their research areas).

For 2., I needed a list of well-regarded, mainstream philosophy journals. I used a recent meta-ranking (De Bruin 2023) that lists 40 journals (four of these journals are not indexed on the WoS and so I could not include them). I realize that this list is not definitive, but it’s the best I could find.

For 4., I used the five major sub-field clusters listed on [PhilPapers](https://philpapers.org/categories.pl). 77.5% of the articles in my dataset had at least one sub-field cluster listed.

Figure 3 shows the average number of authors since 1975 broken up by sub-field cluster (sub-figure A), journal ranking (mainstream vs. other; B) and purity (C).

![Figure 3. Average number of authors over time by sub-field cluster (A), journal ranking (B) and purity (C); shaded areas show 95% confidence intervals.]({{site.url}}/something-of-crunch/assets/images/2023-20-12/figure3.png)
<p style="text-align:center; font-size: 0.85em; padding-right: 30px; padding-left: 30px;">Figure 3. Average number of authors over time by sub-field cluster (A), journal ranking (B) and purity (C); shaded areas show 95% confidence intervals.</p>
<br>

All three sub-figures suggest differences in trajectories between category levels. To statistically test for these (potential) differences, I used a negative binomial model (to account for over-dispersion) with the number of co-authors (i.e., the number of authors minus one) as the outcome and year, and sub-field cluster, journal ranking and journal purity, and their interactions with year as predictors. Here are the results:

<table>
  <tr>
    <th class="thead firsttablerow firsttablecol">&nbsp;</th>
    <th colspan="3" class="thead firsttablerow">Number of co-authors</th>
  </tr>
  <tr>
    <td class="depvarhead firsttablerow firsttablecol">Predictors</td>
    <td class="depvarhead firsttablerow">IRR</td>
    <td class="depvarhead firsttablerow">95% CI</td>
    <td class="depvarhead firsttablerow">p</td>
  </tr>
  <tr>
    <td class="tdata firsttablecol">Intercept</td>
    <td class="tdata centeralign">0.05</td>
    <td class="tdata centeralign">0.04&nbsp;&ndash;&nbsp;0.06</td>
    <td class="tdata centeralign"><strong>&lt;0.001</strong></td>
</tr>
  <tr>
    <td class="tdata firsttablecol">Year</td>
    <td class="tdata centeralign">1.02</td>
    <td class="tdata centeralign">1.01&nbsp;&ndash;&nbsp;1.03</td>
    <td class="tdata centeralign"><strong>&lt;0.001</strong></td>
</tr>
  <tr>
    <td class="tdata firsttablecol">Purity (Pure philosophy)</td>
    <td class="tdata centeralign">0.55</td>
    <td class="tdata centeralign">0.45&nbsp;&ndash;&nbsp;0.66</td>
    <td class="tdata centeralign"><strong>&lt;0.001</strong></td>
</tr>
  <tr>
    <td class="tdata firsttablecol">Mainstream (Other)</td>
    <td class="tdata centeralign">0.69</td>
    <td class="tdata centeralign">0.57&nbsp;&ndash;&nbsp;0.84</td>
    <td class="tdata centeralign"><strong>&lt;0.001</strong></td>
</tr>
  <tr>
    <td class="tdata firsttablecol">Sub-field cluster (LEM&M)</td>
    <td class="tdata centeralign">0.99</td>
    <td class="tdata centeralign">0.77&nbsp;&ndash;&nbsp;1.27</td>
    <td class="tdata centeralign">0.957</td>
</tr>
  <tr>
    <td class="tdata firsttablecol">Sub-field cluster (Phil. Trad.)</td>
    <td class="tdata centeralign">1.12</td>
    <td class="tdata centeralign">0.81&nbsp;&ndash;&nbsp;1.53</td>
    <td class="tdata centeralign">0.497</td>
</tr>
  <tr>
    <td class="tdata firsttablecol">Sub-field cluster (SL&M)</td>
    <td class="tdata centeralign">2.01</td>
    <td class="tdata centeralign">1.57&nbsp;&ndash;&nbsp;2.57</td>
    <td class="tdata centeralign"><strong>&lt;0.001</strong></td>
</tr>
  <tr>
    <td class="tdata firsttablecol">Year:Sub-field cluster (Value Theory)</td>
    <td class="tdata centeralign">0.94</td>
    <td class="tdata centeralign">0.73&nbsp;&ndash;&nbsp;1.21</td>
    <td class="tdata centeralign">0.646</td>
</tr>
  <tr>
    <td class="tdata firsttablecol">Year:Purity (Pure philosophy)</td>
    <td class="tdata centeralign">1.00</td>
    <td class="tdata centeralign">0.99&nbsp;&ndash;&nbsp;1.00</td>
    <td class="tdata centeralign">0.100</td>
</tr>
  <tr>
    <td class="tdata firsttablecol">Year:Mainstream (Other)</td>
    <td class="tdata centeralign">1.01</td>
    <td class="tdata centeralign">1.01&nbsp;&ndash;&nbsp;1.02</td>
    <td class="tdata centeralign"><strong>&lt;0.001</strong></td>
</tr>
  <tr>
    <td class="tdata firsttablecol">Year:Sub-field cluster (LEM&M)</td>
    <td class="tdata centeralign">1.02</td>
    <td class="tdata centeralign">1.02&nbsp;&ndash;&nbsp;1.03</td>
    <td class="tdata centeralign"><strong>&lt;0.001</strong></td>
</tr>
  <tr>
    <td class="tdata firsttablecol">Year:Sub-field cluster (Phil. Trad.)</td>
    <td class="tdata centeralign">0.99</td>
    <td class="tdata centeralign">0.98&nbsp;&ndash;&nbsp;1.00</td>
    <td class="tdata centeralign">0.101</td>
</tr>
  <tr>
    <td class="tdata firsttablecol">Year:Sub-field cluster (SL&M)</td>
    <td class="tdata centeralign">1.01</td>
    <td class="tdata centeralign">1.01&nbsp;&ndash;&nbsp;1.02</td>
    <td class="tdata centeralign"><strong>&lt;0.001</strong></td>
</tr>
  <tr>
    <td class="tdata firsttablecol">Year:Sub-field cluster (Value Theory)</td>
    <td class="tdata centeralign">1.04</td>
    <td class="tdata centeralign">1.03&nbsp;&ndash;&nbsp;1.05</td>
    <td class="tdata centeralign"><strong>&lt;0.001</strong></td>
</tr>
  <tr>
    <td class="tdata leftalign summary firstsumrow">Observations</td>
    <td class="tdata summary summarydata firstsumrow" colspan="3">98898</td>
  </tr>
  <tr>
    <td class="tdata leftalign summary">R<sup>2</sup> Nagelkerke</td>
    <td class="tdata summary summarydata" colspan="3">0.193</td>
  </tr>
  <tr>
    <th colspan="4" class="thead firsttablerow"></th>
  </tr>
</table>

The model provides evidence for 2. and 4. Year remained an overall significant predictor of the number of co-authors: with ever year, the expected co-author count increased by a factor of 1.02 (while holding all other variables in the model constant). This increase over time was significantly steeper for journals outside of the mainstream compared to mainstream journals and for articles from three of philosophy’s five sub-field clusters (SL&M; LEM&M; Value Theory). In contrast, the interaction between journal purity and year was not significant, and so the model does not provide evidence for explanation 1.

Investigating 3. is a bit more tricky since this requires a way of identifying articles that report original empirical research. I don’t think there is a way to do this reliably based just on the meta-data I have available. However, for a different project, I had already downloaded the full texts of all original research articles (18,442 in total) published between 1971 and 2021 in six journals (_Australasian Journal of Philosophy_; _Analysis_; _Mind_; _Noûs_; _Philosophical Studies_; _Synthese_). Within these texts, I searched for the strings “(our OR my) AND (result[s] OR finding[s])” and “(our OR my) AND (study OR studies OR experiment[s])”, reasoning that if a text included both, it likely reported original empirical results. This is of course not definitive, but I think it generates a reasonable guess. Figure 4 shows the percentage of articles (in the six journals listed above) since 1975 that reported original empirical research (inset figure) and the average number of authors since 1975 on articles that reported empirical research vs. regular philosophy articles (main figure).

![Figure 4. Percentage of articles since 1975 in six journals that reported empirical research (inset figure); average number of authors since 1975 on articles that reported empirical research vs. regular philosophy articles (main figure). Shaded areas show 95% CI (note that before 2001-5, there were not enough articles in the dataset to estimate these).]({{site.url}}/something-of-crunch/assets/images/2023-20-12/figure4.png)
<p style="text-align:center; font-size: 0.85em; padding-right: 30px; padding-left: 30px;">Figure 4. Percentage of articles since 1975 in six journals that reported empirical research (inset figure); average number of authors since 1975 on articles that reported empirical research vs. regular philosophy articles (main figure). Shaded areas show 95% CI (note that before 2001-5, there were not enough articles in the dataset to estimate these).</p>
<br>

The percentage of philosophy articles that report original empirical research (as estimated by my method) has risen substantially since 1975 and in particular since around 2000. Moreover, as one would expect, the average number of authors on these articles is both much larger in general than the average number of authors on ‘regular’ philosophy articles and has also risen steeply since 1975. This provides some evidence for explanation 3. (though note that the average number of authors has also been increasing over time for regular articles, so 3. does not provide a full explanation).

**References**

De Bruin, Boudewijn. 2023. “Ranking Philosophy Journals: A Meta-Ranking and a New Survey Ranking.” _Synthese_ 202 (6): 188. https://doi.org/10.1007/s11229-023-04342-9.



