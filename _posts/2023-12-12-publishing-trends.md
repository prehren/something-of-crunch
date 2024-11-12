---
title: "Publishing Trends: The End of History?"
date: 2023-12-12
---

<style>
html, body { background-color: white; font-family:Arial,Helvetica,sans-serif; font-size:12px }
table { border-collapse:collapse; border:none; }
caption { font-weight: bold; text-align:left; }
td {  }
.thead { border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm; }
.tdata { padding:0.2cm; text-align:left; vertical-align:top; }
.arc { background-color:#f2f2f2; }
.summary { padding-top:0.1cm; padding-bottom:0.1cm; }
.summarydata { text-align:left; }
.fixedparts { font-weight:bold; text-align:left; }
.randomparts { font-weight:bold; text-align:left; padding-top:.8em; }
.zeroparts { font-weight:bold; text-align:left; padding-top:.8em; }
.simplexparts { font-weight:bold; text-align:left; padding-top:.8em; }
.lasttablerow { border-bottom: double; }
.firsttablerow {  }
.firstsumrow { border-top:1px solid; }
.labelcellborder { border-bottom:1px solid; }
.depvarhead { text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal; }
.depvarheadnodv { border-top: double; text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal; }
.leftalign { text-align:left; }
.centeralign { text-align:center; }
.firsttablecol { text-align:left; }
.footnote { font-style:italic; border-top:double black; text-align:right; }
.subtitle { font-weight: normal; }
.modelcolumn1 {  }
.modelcolumn2 {  }
.modelcolumn3 {  }
.modelcolumn4 {  }
.modelcolumn5 {  }
.modelcolumn6 {  }
.modelcolumn7 {  }
.col1 {  }
.col2 {  }
.col3 {  }
.col4 {  }
.col5 {  }
.col6 {  }
</style>

<body>
  
Philosophy, like any other academic disciplines, goes through fashions: different sub-fields receive different amounts of attention at different points in time. I thought it would be fun to try and chart some of these developments. In this post, I show that articles on the history of philosophy used to be much more common in philosophy's top journals than they are today.

I'm again using the dataset described in my [last post](https://prehren.github.io/something-of-crunch/2023/12/11/generalist-journals.html) (meta-data on 103,595 articles published between 1975 and 2021 in one of 223 journals). To start, Figure 1 shows the journal average proportion of articles from each of PhilPapers’ five major sub-field clusters since 1975 in 22 top generalist philosophy journals (for more information, see [here](https://prehren.github.io/something-of-crunch/2023/12/11/generalist-journals.html)). By journal average, I mean that I first calculated the proportion of articles for each journal seperately, and then averaged these values.

![Figure 1. Journal average proportion of articles from each of PhilPapers’ five major sub-field clusters since 1975 in 22 top generalist philosophy journal (SL&M = Philosophy of Science, Logic and Mathematics).]({{site.url}}/something-of-crunch/assets/images/2023-12-12/fig1.png)
<p style="text-align:center; font-size: 0.85em; padding-right: 30px; padding-left: 30px;">Figure 1. Journal average proportion of articles from each of PhilPapers’ five major sub-field clusters since 1975 in 22 top generalist philosophy journal (SL&M = Philosophy of Science, Logic and Mathematics).</p>
<br>

We see that over the last ~50 years, the journal average of History of Western Philosophy (HoWP) has declined quite dramatically. In 1975, HoWP articles made up on average 21.6% of all articles in philosophy's top generalist journals. By 2021, this percentage had more than halved, to 10.8%.

Do we find a similar trend in other (non-top and/or non-generalist) philosophy journals? No.

![Figure 2. Journal average proportion of articles from each of PhilPapers’ five major sub-field clusters since 1975 in 198 non-top and/or non-generalist philosophy journals.]({{site.url}}/something-of-crunch/assets/images/2023-12-12/fig2.png)
<p style="text-align:center; font-size: 0.85em; padding-right: 30px; padding-left: 30px;">Figure 2. Journal average proportion of articles from each of PhilPapers’ five major sub-field clusters since 1975 in 198 non-top and/or non-generalist philosophy journals.</p>
<br>

What happened to all the work on the history of philosophy that used to be published in the top generalist journals? Of course, there are many possible answers, most of which I cannot check (easily). One possible answer I _can_ say something about is that historians of philosophy shifted away from publishing in generalist journals in favor of publishing in new specialist journals. If this explanation holds water, then we would expect to see an increase in the share of specialist history of philosophy journals over time.

To identify specialist history journals, I calculated the proportion of HoWP articles published in two well-known history journals, the _British Journal for the History of Philosophy_ and the _Journal of the History of Philosophy_. On average, these journals publish 66.8% and 69.8% of HoWP articles each year, respectively. Based on these values, I count a journal as a specialist history of philosophy journal (during a given year) if it published 65% or more HoWP articles (in that year). Figure 3 shows the proportion of specialist history journals (so defined) for each year since 1975.

![Figure 3. Proportion of specialist history of philosophy journals over time. Errorbars show 95% Wilson CIs.]({{site.url}}/something-of-crunch/assets/images/2023-12-12/fig3.png)
<p style="text-align:center; font-size: 0.85em; padding-right: 30px; padding-left: 30px;">Figure 3. Proportion of specialist history of philosophy journals over time. Errorbars show 95% Wilson CIs.</p>
<br>

From Figure 3, it looks like there has indeed been an increase in the proportion of specialist history of philosophy journals since the mid 2000s (though note the range of the 95% confidence intervals shown in the figure). However, the proportion of HoWP articles has been on the decline in the top generalist journals for much longer than the mid 2000s (see, Figure 1). Can an increase in the number of specialist outlets for history of philosophy articles still explain (some of) this decline? To investigate this, I used a logistic mixed-effects regression model, predicting the proportion of HoWP articles in the top generalist journals by year and the proportion of specialist history journals. The model also included random intercepts and slopes for journal. The table below shows the results.

<table style="border-collapse: collapse; width: auto; table-layout:auto; margin-left:auto;margin-right:auto;">
<tr>
  <th class="thead firsttablerow firsttablecol col1">&nbsp;</th>
  <th colspan="3" class="thead firsttablerow">Prop. of history articles</th>
</tr>
<tr>
  <td class="depvarhead firsttablerow firsttablecol col1">Predictors</td>
  <td class="depvarhead firsttablerow col2">Odds Ratios</td>
  <td class="depvarhead firsttablerow col3">CI</td>
  <td class="depvarhead firsttablerow col4">p</td>
</tr>
<tr>
  <td class="tdata firsttablecol col1">Intercept</td>
  <td class="tdata centeralign modelcolumn1 col2">0.39</td>
  <td class="tdata centeralign modelcolumn1 col3">0.27&nbsp;&ndash;&nbsp;0.55</td>
  <td class="tdata centeralign modelcolumn1 col4"><strong>&lt;0.001</strong></td>
</tr>
<tr>
  <td class="tdata firsttablecol col1">Year</td>
  <td class="tdata centeralign modelcolumn1 col2">0.97</td>
  <td class="tdata centeralign modelcolumn1 col3">0.96&nbsp;&ndash;&nbsp;0.97</td>
  <td class="tdata centeralign modelcolumn1 col4"><strong>&lt;0.001</strong></td>
</tr>
<tr>
  <td class="tdata firsttablecol col1">Prop. of specialist journals</td>
  <td class="tdata centeralign modelcolumn1 col2">0.35</td>
  <td class="tdata centeralign modelcolumn1 col3">0.12&nbsp;&ndash;&nbsp;1.04</td>
  <td class="tdata centeralign modelcolumn1 col4">0.059</td>
</tr>
<tr>
  <td colspan="4" class="randomparts">Random Effects</td>
</tr>
<tr>
  <td class="tdata leftalign summary">&sigma;<sup>2</sup></td>
  <td class="tdata summary summarydata" colspan="3">3.29</td>
</tr>
<tr>
  <td class="tdata leftalign summary">&tau;<sub>00</sub> <sub>Journal</sub></td>
  <td class="tdata summary summarydata" colspan="3">0.34</td>
<tr>
  <td class="tdata leftalign summary">&tau;<sub>11</sub> <sub>Journal.Year</sub></td>
  <td class="tdata summary summarydata" colspan="3">0.00</td>
<tr>
  <td class="tdata leftalign summary">&rho;<sub>01</sub> <sub>Journal</sub></td>
  <td class="tdata summary summarydata" colspan="3">-0.22</td>
<tr>
  <td class="tdata leftalign summary">ICC</td>
  <td class="tdata summary summarydata" colspan="3">0.11</td>
<tr>
  <td class="tdata leftalign summary">N <sub>Journal</sub></td>
  <td class="tdata summary summarydata" colspan="3">22</td>
<tr>
  <td class="tdata leftalign summary firstsumrow">Observations</td>
  <td class="tdata summary summarydata firstsumrow" colspan="3">649</td>
</tr>
<tr>
  <td class="tdata leftalign summary">Marginal R<sup>2</sup> / Conditional R<sup>2</sup></td>
  <td class="tdata summary summarydata" colspan="3">0.055 / 0.155</td>
</tr>
</table>

Unlike year, the proportion of specialist history journals does not significantly predict the proportion of HoWP articles in philosophy's top generalist journals. Therefore, it doesn't look like historians of philosophy shifting away from publishing in top generalist journals in favor of new specialist journals well explains HoWP's decline in these journals.

</body>
