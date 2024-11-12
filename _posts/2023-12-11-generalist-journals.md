---
title: "How Generalist are Philosophy's Top Generalist Journals?"
date: 2023-12-11
---

I've often heard the complaint that philosophy's top generalist journals really are LEMM-ings in disguise. That is, instead of being open to articles from all or at least most areas of philosophy, their output is skewed towards the so-called LEMM-ing fields (language, epistemology, mind and metaphysics).

How much truth is there to this complaint? To find out, I turned to two large online databases: *PhilPapers* (PP) and the *Web of Science* (WoS). PP is a ["comprehensive index and bibliography of philosophy maintained by the community of philosophers."](https://philpapers.org/) Available meta-data include author names, publication title, journal name, volume, issue, page numbers and publication year. In addition, many papers indexed on PP are categorized as belonging to one or more of "the traditional fields of philosophy"—philosophy of mind, normative ethics, philosophy of physics, Asian philosophy and 17th/18th century philosophy, that sort of thing.

The WoS is ["a comprehensive interdisciplinary, bibliographic database with article references from journals, books, proceedings."](https://library.ethz.ch/en/locations-and-media/media-types/databases-standards-patents/web-of-science-core-collection.html) It provides lots of useful meta-data like author affiliation, document language, citation count and research area. However, for this post, I only used document type (e.g., article, book review, erratum, front matter, etc.).

I determined which journals are indexed on both PP and WoS, and then downloaded all entries for these journals since 1975 (this is the period for which the WoS has good coverage). PP indexes a huge number of journals (> 1500), and among them are many that few would call philosophy journals (including the journals themselves). Therefore, I restricted the data to journals with the WoS research areas *Philosophy* and *History and Philosophy of Science*. I also restricted the data to original research articles (hence excluding book reviews, editorials, front matter and so on). This left me with meta-data on English-language 103,595 articles from 223 journals.

Next, I needed a list of top generalist philosophy journals. I used [LeiterReports' ranking](https://leiterreports.typepad.com/blog/2022/07/best-general-philosophy-journals-2022.html) of the best general philosophy journals. Four of these journals are not indexed on WoS (*Proceedings of the Aristotelian Society*; *Ergo*; *The Monist*; *Philosophical Topics*) and so I had to exclude them.

For each of the 22 LeiterReports journals, I calculated the proportion of articles published in the last 10 years from each of the five major sub-field clusters listed on PhilPapers. If an article was assigned to more than one sub-field cluster, I included it more than once. Figure 1 shows these proportions averaged across journals. The LEMM-ing fields indeed dominate: The share of LEM&M articles is larger than the share of articles from the other four sub-field clusters *combined* (56.1% vs. 43.9%).

![Figure 1. Mean proportion of articles from philosophy's five major sub-fields across across 22 top generalist journals (SL&M = Philosophy of Science, Logic and Mathematics).](https://raw.githubusercontent.com/prehren/something-of-crunch/71c6d36bf8de523c44411387ea3607a661e1ce1b/assets/images/2023-12-11/fig1.png)
<p style="text-align:center; font-size: 0.75em; padding-right: 30px; padding-left: 30px;">Figure 1. Mean proportion of articles from philosophy's five major sub-fields across across 22 top generalist journals (SL&M = Philosophy of Science, Logic and Mathematics).</p>
<br>

How unusual is this? Perhaps the LEMM-ing fields are just more popular than the other sub-field clusters, in general? No. Figure 2 shows their proportions across the remaining 198 (non-top and/or non-generalist) journals in my data. Here, the five sub-field clusters are spread more or less evenly.

![Figure 2. Mean proportion of articles from philosophy's five major sub-fields across 198 non-top and/or non-generalist journals.](https://raw.githubusercontent.com/prehren/something-of-crunch/refs/heads/main/assets/images/2023-12-11/fig2.png)
<p style="text-align:center; font-size: 0.75em; padding-right: 30px; padding-left: 30px;">Figure 2. Mean proportion of articles from philosophy's five major sub-fields across 198 non-top and/or non-generalist journals.</p>
<br>

One way to quantify *how* over-represented the LEMM-ing fields are is to calculate their representativeness ratio *R*, defined as the propotion of LEM&M articles in the top generalist journals divided by the proportion of LEM&M articles in other philosophy journals. _R_ > 1 indicates over-representation; _R_ < 1 indicates under-representation. The table below shows _R_ for philosophy's five main sub-field clusters.

<table>
<thead>
<tr class="header">
<th align="left">Sub-field cluster</th>
<th align="right"><span class="math inline">(<em>R</em>)</span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">History of Western Philosophy</td>
<td align="right">0.30</td>
</tr>
<tr class="even">
<td align="left">LEM&amp;M</td>
<td align="right">2.39</td>
</tr>
<tr class="odd">
<td align="left">Philosophical Traditions</td>
<td align="right">0.06</td>
</tr>
<tr class="even">
<td align="left">SL&amp;M</td>
<td align="right">0.64</td>
</tr>
<tr class="odd">
<td align="left">Value Theory</td>
<td align="right">0.80</td>
</tr>
</tbody>
</table>
<p style="text-align:center; font-size: 0.75em; padding-right: 30px; padding-left: 30px;">Table 1. Representativeness index *R* for philosophy’s five main sub-field clusters.</p>
<br>

The LEMM-ing fields' R comes out as 2.39—in other words, the proportion of LEM&M articles in the the top generalist journals is more than twice that of LEM&M articles in other journals. In contrast, the other four sub-field clusters all have Rs less than one and so are under-represented (compared to the porportions shown in Figure 2), though not all to the same extent. In particular, History of Western Philosophy and Philosophical Traditions fare quite a lot worse than Value Theory and SL&M. History of Western Philosophy articles are about three times less common in the top generalist journals than in other journals, while Philosophical Traditions articles are almost 17 times less common in the top generalist journals than in other journals.

![Figure 3. Proportion of articles from philosophy's five major sub-fields in 22 top generalist journals.](https://raw.githubusercontent.com/prehren/something-of-crunch/refs/heads/main/assets/images/2023-12-11/fig3.png)
<p style="text-align:center; font-size: 0.75em; padding-right: 30px; padding-left: 30px;">Figure 3. Proportion of articles from philosophy's five major sub-fields in 22 top generalist journals.</p>
<br>

I also broke down the result by journal. Figure 3 shows the results. LEMM-ing fields make up more than 50% of all articles in all but four journals: *Canadian Journal of Philosophy*; *European Journal of Philosophy*; *JAPA*; and *Philosophers' Imprint*. The share of articles from the LEMM-ing fields is larger than the share of articles from any other sub-field cluster in all but one journal. In *Philosophers' Imprint*, LEMM-ing articles and articles on Value Theory are tied at 34%.

With a few exceptions, then, most top generalist philosophy journals really do look an awful lot like LEMM-ings in disguise.
