---
title: "Most Cited Authors on the WoS: There's an App For That!"
date: 2024-11-15
---

I've made a Shiny app that allows people to puruse the WoS citation data [I recently used](https://prehren.github.io/something-of-crunch/2024/11/13/top-wos-authors.html) to rank the most cited authors in philosophy journals since 1975 at their own leasure. Here it is (if the app does not show up below, you can also find it on [shinyapps.io](https://prehren.shinyapps.io/most-cited-philosophers-wos/)):

<iframe src="https://prehren.shinyapps.io/most-cited-philosophers-wos/" title="Shiny app that allows users to puruse the WoS citation data I recently used to rank the most cited authors in philosophy journals since 1975 at their own leasure." style="border:none; width:100%; height:1080px; margin:0 auto; display: block; overflow:hidden;" scrolling="no"></iframe>

Brief explanation: The top panel shows the overall ranking; the bottom panel shows the ranking's development over time. _k_ is the number of authors included in the overall ranking. _Lowest rank shown_ is the lowest rank shown in the bottom panel. _Start when?_ asks for the first time bin from which data is to be included in the figure(s). Some journals have not been running since 1975; other journals have been running for at least that long, but the WoS does not provide (enough) citation data for articles in these journals until a later point in time. If _Only journals that cover the entire period?_ is selected, then the generated figure(s) are based on articles in journals for which data were available for the entire period since _Start when?_. Otherwise, data from all relevant journals are included.

I also assigned journals to the five major sub-field clusters listed on PhilPapers (for a description, see [here](https://prehren.github.io/something-of-crunch/2023/12/11/generalist-journals.html)). To do so, for each journal, I calculated the proportion of articles that journal had published since 1975 in each sub-field cluster (History of Western Philosophy; LEM&M-ing; Philosophy of Science, Logic and Mathematics; Philosophical Traditions; Value Theory). I then categorized a journal as a specialist journal in one of these sub-clusters if the respective proportion was larger than 0.5; all other journals, I categorized as 'Mixed.'
