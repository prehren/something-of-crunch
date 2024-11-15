---
title: "Most Cited Authors on the WoS: There's an App For That!"
date: 2024-11-15
---

I've made a Shiny app that allows people to puruse the WoS citation data [I recently used](https://prehren.github.io/something-of-crunch/2024/11/13/top-wos-authors.html) to rank the most cited authors in philosophy journals since 1975 at their own leasure. Here it is (if the app does not show up below, you can also find it on [shinyapps.io](https://prehren.shinyapps.io/most-cited-philosophers-wos/)):

<iframe src="https://prehren.shinyapps.io/most-cited-philosophers-wos/" title="Figure 1. Development over time of the top 25." style="border:none; margin:0 auto; display: block; width:100%; height:1180px; padding-bottom:1em; overflow:hidden;" scrolling="no"></iframe>
<br>

Brief explanation: The top panel shows the overall ranking; the bottom panel shows the ranking's development over time. _k_ is the number of authors included in the overall ranking. _Lowest rank shown_ is the lowest rank shown in the bottom panel. _Start when?_ asks for the first time bin from which data is supposed to be included in the figures. Some journals have not been running since 1975; other journals have been running for at least that long, but the WoS does not provide (enough) citation data for articles in the journals until a later year. If _Only journals that cover the entire period?_ is selected, then the generated figures only include journals for which data were available for the entire period since _Start when?_. Otherwise, all journals are included.

