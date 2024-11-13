---
title: "Most Cited Philosophy Authors on the WoS"
date: 2024-11-13
---

On his [blog](https://schwitzsplinters.blogspot.com/2024/08/the-378-most-cited-contemporary-authors.html), Eric Schwitzgebel has posted a list of the most cited authors in philosophy according to the SEP. While playing around with citation data from the Web of Science, I figured it might be interesting to do something similar with these data.

The WoS provides 'Cited References' for many of its entries. As of Sept 2024 (when I downloaded the data), the WoS indexed around 540,000 articles in the category Philosophy (English: ~410,000; French: ~36,000; German: ~25,000; Spanish: ~16,000; Italian: ~13,000; Russian: ~12,000; everything else: < 10,000). Of these articles, around 495,000 had at least one cited item associated with them, for a total of around 9 million references.

Here is a random sample of 10 references:

- Field Hartry, 1972, Journal of Philosophy, V69, P347.
- DEP HLTH, 1895, REP MUN LAB DEP HLTH, P178.
- FERRARA Alessandro, 1997, ETIKA AUTONOMIE AUTE.
- BOLZANO B, WISSENSCHAFTSLEHRE.
- Aristotle, POLITICS.
- Zalta E., 2020, STANFORD ENCY PHILOS.
- PFETSCH F, UNPUBLISHED MANUSCRI.
- McCarthy E.Doyle., 1985, History of Sociology, V5, P21.
- Chisholm R. M., 1957, Perceiving: A philosophical study.
- BOLLNOW OF, 1997, HERMENEUUSCHE PHILOS, P323.

While there is not a huge amount of information here (e.g., no article titles; no publisher information; no editors), almost all cited items include author names[^1]. That's good. What is less ideal is that for most authors, we only get initials, not full first names. Yet many first initial-last name combinations are going to be shared by lots of authors. 

[^1]: Or, rather, the name of the first author—my sense is that co-authors are generally omitted. This isn't much of a problem, though, [given that the vast majority of philosophy articles are single-authored](https://prehren.github.io/something-of-crunch/2023/12/20/co-authorship.html).

One possible way to get around this problem would be to only keep references with at least one full first name. However, this strategy has at least two severe issues. First, the strategy filters out references to works by authors without a first name (e.g., Aristotle, Plato, Plutarch, Averroes). Of course, it is possible to keep these references in the dataset. This introduces a different problem, however. Consider Aristotle. Aristotle virtually always get referenced as 'Aristotle.' This means that my filtered dataset would include (almost) all references to Aristotle's works. Compare that to an author like David Lewis, who usually gets referenced as 'David Lewis' or 'D. Lewis.' The filtered dataset would only contain instances of the first case, but not instances of the second case. As a result, Aristotle's citation count would be (quite dramatically) inflated compared to David Lewis' citation count.

The second issue is that 

These two problems combined mean that I 

Some of the journals the WoS lists under Philosophy strike me as questionable. For instance: Are the _Nursing History Review_, the _Journal of Medical Biography_, the _Journal for the History of Astronomy_ or _Engineering Studies_ really philosophy journals? I think not. As a result, I decided to remove all journals from the dataset that are not also indexed on PhilPapers. This method isn't perfect, of course, but I think it is good enough.

After these (and some other, more boring exclusions having to do with missing data), I was  left with a final dataset containing ~1.6 million references from articles published in 269 journals between 1975 and 2024.

There are different ways to quantify _most cited author_. One is to just count up citations. I don't think that is a particularly helpful approach, however, because (a) philosophers today cite a lot more stuff than did philosophers 50 years ago and (b) many more philosophy articles get published today than did 50 years ago. This means that raw citation counts as a measure of influence are biased (heavily) in favor of recent citations.

I instead chose to go with proportions. Note that, by itself, this doesn't solve (a) and (b). To illustrate [I'll focus on (a), but the problem with (b) is analogous]: Suppose we are looking at two years, 1990 and 2020, for one journal A. In 1990, A published 10 articles, while in 2020, it published 100 articles. Suppose further that articles in 1990 and 2020 cite about the same number of references (say, 10). If an author was very influential in the pages of A in 1990 (say, 10% of all citations were to this author's work) but no longer that influential in 2020 (say, 1%), then we get an overall proportion of citations to this author in A of ~2%. If the roles of 1990 and 2020 had been reversed, however, then this overall proportion would have been ~9%. Yet it looks like this differences is just an artifact of the fact that A published fewer articles in 1990 than in 2020.

To avoid (a) and (b), I divided my data into time bins (I chose five years), calculated the proportion of citations received by a given author in each bin separately, and only then calculated the mean across all of these bins. I also did the same thing for journals; otherwise, the results would be biased towards influence in journals that publish more articles and/or have higher average citation rates.

[TOP LIST]

Here are a few observations: First, while I am of course aware that Aristotle and Plato are ...like, important, I still find it pretty incredible that they come in first and third after having been dead for more than 2000 years. Second, there is a sharp drop-off after the first four authors (Aristotle, Kant, Plato, Heidegger): Their cumulative score is roughly equal to the cumulative score of the next fourteen authors (Wittgenstein to Habermas). Big Four? Third, a number of people in Schwitzgebel's comments asked questions/expressed dismay about the low ranks of various (European) authors. On the current list, these authors tend to rank much higher: Derrida (ranked #9), Foucault (#21), Merleau-Ponty (#23), Gadamer (#50), Adorno (#65) and Cavell (#90), for example, are all in the top 100.

Schwitzgebel makes it clear, of course, that his ranking only captures current influence in 'mainstream Anglophone philosophy,' and so the fact that Derrida, Foucault et al. are not particularly high up on his list is not surprising. The question, then, is: What does the current ranking capture? The answer I think depends a lot on whether the journals in my dataset capture published academic philosophy. he current ranking captures  is not unreasonable to claim that the current ranking is able to capture influence across philosophy more broadly. I will probably make a shiny app that allows people to select which journals they want included an the like, so that people who disagree can puruse the dataset at their own leasure.

Since this data is longitudinal (1975-2024), I also looked at . I made the graph interactive because it is a mess otherwise.
