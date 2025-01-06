---
title: "Most Cited Authors on the WoS"
date: 2024-11-13
---

A little while ago, on his [blog](https://schwitzsplinters.blogspot.com/2024/08/the-378-most-cited-contemporary-authors.html), Eric Schwitzgebel posted a list of the most cited authors in philosophy according to the SEP (he's also done this a couple of times before). At the time, I was playing around with citation data from the Web of Science, I so figured it might be interesting to do something similar with these data.

The WoS provides 'Cited References' for many entries. As of Sept 2024 (when I downloaded the data), the WoS indexed around 540,000 articles in the category Philosophy (English: ~410,000; French: ~36,000; German: ~25,000; Spanish: ~16,000; Italian: ~13,000; Russian: ~12,000; everything else: < 10,000). Of these articles, around 495,000 had at least one cited item associated with them, for a total of around 9 million references. Some of the journals the WoS lists under Philosophy strike me as questionable. For instance: Are the _Nursing History Review_, the _Journal of Medical Biography_, the _Journal for the History of Astronomy_ or _Engineering Studies_ really philosophy journals? I think not. As a result, I decided to remove all journals from the dataset that are not also indexed on PhilPapers. After these (and some other, more boring exclusions having to do with missing or insufficient data), I was left with ~5.9 million references from ~328,000 articles published in 338 journals between 1975 and 2024.

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

While there is not a huge amount of information here (e.g., no article titles; no publisher information; no editors), almost all cited items include author names.[^1] That's good. What is not so ideal is that for most authors, we only get initials, not full first names. Yet many first initial-last name combinations are going to be shared by lots of authors. 

[^1]: Or, rather, the name of the first author—my sense is that co-authors are generally omitted. This isn't much of a limitation, though, [given that the vast majority of philosophy articles are single-authored](https://prehren.github.io/something-of-crunch/2023/12/20/co-authorship.html).

One possible way to get around this problem would be to only keep references with at least one full first name. However, this strategy has at least two major problems. First, the strategy filters out references to works by authors without a first name (e.g., Aristotle, Plato, Plutarch, Averroes) or authors who usually get referred to only by last name. Of course, it is possible to simply keep these references in the dataset. This introduces a different problem, though. Consider Aristotle. Aristotle virtually always get referenced as 'Aristotle.' This means that the new filtered dataset would include (almost) all references to Aristotle's works. Compare that to an author like David Lewis, who usually gets referenced either as 'D. Lewis' or 'David Lewis.' The filtered dataset would only contain instances of the second case, but not instances of the first case. As a result, Aristotle's citation count would be inflated (likely dramatically inflated) compared to David Lewis' citation count.

The second problem is that only keeping references with full author names results in inaccurate citation counts if the ratio of citations with full first names to citations with first initials is different for different authors. Suppose that when people reference David Lewis, 20% of the time, they do so as 'David Lewis', while the remaining 80% of the time as 'D. Lewis' (or 'D.K. Lewis'). In that case, the new filtered dataset would include only 20% of all Lewis-references present in the original dataset. If this ratio is the same (or at least similar) for other authors, then everything is fine. However, suppose that Immanuel Kant gets referenced as 'Immanuel Kant' 50% of the time. If so, then the new filtered dataset would lead me to substantially underestimate Lewis' citation count compared to Kant's citation count. Unfortunately, what I have just described is what the actual data look like: 66% of references to the last name 'Lewis' are to 'D. Lewis' or 'D.K. Lewis', while only 14% are to 'David Lewis;' in contrast, 46% of references to the last name 'Kant' are to 'Immanuel Kant,' another 46% are to 'I. Kant.'

Filtering out rows with only first initials, then, is unfortunately not an option. Instead, I decided to convert full first names into first initials (e.g., Immanuel Kant --> I Kant, David Lewis --> D Lewis). This means that I get to keep most of the original data. The trade-off is that my results will need to be taken with a grain of salt: Many first initial(s)-last name combinations are going to be shared by multiple authors. That said, there's reason to believe that this limitation isn't too severe. I restricted the data to rows with full first names available, and then calculated the proportion of full first name(s)-last name combinations associated with each first initial(s)-last name combination in the top 500 (see below). On average, the most common full first name(s)-last name combination accounted for over 90% of all occurences of a given first initial(s)-last name combination. In other words, it seems that the first initial(s)-last name combinations in the top 500 generally refer to a single author, instead of a hodgepode of multiple different authors.

On to data cleaning.[^2] Some authors frequently get referenced only by their last name (e.g., Kant, Marx, Hume, Wittgenstein). To match these occurences to first initial(s)-last name combinations, I calculated the proportion of first initial(s)-last name combinations for each last name in the dataset. Here are the first give lines of the results for 'Kant':

[^2]: Given that I am dealing with millions of references, extensive manual data cleaning was out of the question.

```
   full_nameINITIALS     n     N     prop
   <chr>             <int> <int>    <dbl>
 1 I Kant            25396 27340 0.929   
 2 Kant               1327 27340 0.0485  
 3 E Kant              413 27340 0.0151  
 4 IMMANUEL Kant        46 27340 0.00168 
 5 H Kant               13 27340 0.000475
```

For 'Kant', more than 90% of references are to 'I Kant'. The second most common reference is just to the last name 'Kant'. In this situation, it strikes me as reasonable to assume that these references to the last name are to 'I Kant'. Therefore, whenever for a given last name it was the case that the most common reference was to a first initial(s)-that last name combination and the second most common reference was to just that last name, I replaced all references to just that last name with the most common first initial(s)-last name combination. I also deleted all other instances of just last name references (unless they were the most common type of reference, of course).

Some authors get cited using multiple different sets of first initials (e.g., David Lewis as 'D Lewis' or 'DK Lewis'; Hegel as 'G Hegel,' 'GW Hegel' or 'GWF Hegel'). To combine these and other cases like them into a single first initial(s)-last name combination, I used the following rule: If two or more articles in the same journal cite two authors with the same last name but different sets of first initials in the same five year period (see below) _and_ the two sets of first initials start with the same letter _and_ one of the two sets is an ordered subset of the other, then the two first initial(s)-last name combinations refer to the same author and one can be replaced with the other. While this is not perfect, my sense is that the approach worked rather well—it caught the two examples described at the top of this paragraph, for example.

There are different ways to quantify _most cited author_. One is to simply count up citations. I don't think that is a particularly helpful approach, however, because (a) philosophers today cite a lot more stuff than did philosophers 50 years ago and (b) many more philosophy articles get published today than did 50 years ago. This means that raw citation counts as a measure of influence are biased (heavily) in favor of recent citations.

I instead chose to go with proportions. Now, by itself, this doesn't solve (a) and (b). To illustrate [I'll focus on (a) here, but the problem with (b) is analogous]: Suppose we are looking at two years, 1990 and 2020, for one journal A. In 1990, A published 10 articles, while in 2020, it published 100 articles. Suppose further that articles in 1990 and 2020 cite about the same number of references (say, 10). If an author was very influential in the pages of A in 1990 (say, 10% of all citations were to this author's work) but no longer that influential in 2020 (say, 1%), then we get an overall proportion of citations to this author in A of ~2%. If the descriptions of the two years had been reversed, however, then the overall proportion would have been ~9%. The difference is an artifact of the fact that A published fewer articles in 1990 than in 2020.

To avoid (a) and (b), I divided my data into time bins (five years), calculated the proportion of citations received by a given author in each bin separately, and then calculated the mean across all of these bins. I also did the same thing for journals; otherwise, the results would be biased towards influence in journals that publish more articles and/or feature on average longer reference lists.

Here are the top 502 (brackets show mean percentages):

1\.&nbsp;&nbsp;&nbsp;&nbsp;M Heidegger (0.677%)\
2\.&nbsp;&nbsp;&nbsp;&nbsp;I Kant (0.639%)\
3\.&nbsp;&nbsp;&nbsp;&nbsp;E Husserl (0.418%)\
4\.&nbsp;&nbsp;&nbsp;&nbsp;Aristotle (0.369%)\
5\.&nbsp;&nbsp;&nbsp;&nbsp;J Derrida (0.36%)\
6\.&nbsp;&nbsp;&nbsp;&nbsp;GWF Hegel (0.356%)\
7\.&nbsp;&nbsp;&nbsp;&nbsp;M Foucault (0.342%)\
8\.&nbsp;&nbsp;&nbsp;&nbsp;F Nietzsche (0.275%)\
9\.&nbsp;&nbsp;&nbsp;&nbsp;K Marx (0.274%)\
10\.&nbsp;&nbsp;&nbsp;&nbsp;L Wittgenstein (0.271%)\
11\.&nbsp;&nbsp;&nbsp;&nbsp;G Deleuze (0.26%)\
12\.&nbsp;&nbsp;&nbsp;&nbsp;D Lewis (0.248%)\
13\.&nbsp;&nbsp;&nbsp;&nbsp;Plato (0.238%)\
14\.&nbsp;&nbsp;&nbsp;&nbsp;J Habermas (0.236%)\
15\.&nbsp;&nbsp;&nbsp;&nbsp;J Rawls (0.21%)\
16\.&nbsp;&nbsp;&nbsp;&nbsp;D Hume (0.203%)\
17\.&nbsp;&nbsp;&nbsp;&nbsp;W Quine (0.201%)\
18\.&nbsp;&nbsp;&nbsp;&nbsp;M Merleau Ponty (0.181%)\
19\.&nbsp;&nbsp;&nbsp;&nbsp;JP Sartre (0.178%)\
20\.&nbsp;&nbsp;&nbsp;&nbsp;T Aquinas (0.177%)\
21\.&nbsp;&nbsp;&nbsp;&nbsp;B Russell (0.176%)\
22\.&nbsp;&nbsp;&nbsp;&nbsp;D Davidson (0.166%)\
23\.&nbsp;&nbsp;&nbsp;&nbsp;H Putnam (0.162%)\
24\.&nbsp;&nbsp;&nbsp;&nbsp;R Descartes (0.158%)\
24\.&nbsp;&nbsp;&nbsp;&nbsp;P Ricoeur (0.158%)\
26\.&nbsp;&nbsp;&nbsp;&nbsp;R Rorty (0.155%)\
27\.&nbsp;&nbsp;&nbsp;&nbsp;E Levinas (0.154%)\
28\.&nbsp;&nbsp;&nbsp;&nbsp;J Dewey (0.153%)\
29\.&nbsp;&nbsp;&nbsp;&nbsp;HG Gadamer (0.151%)\
30\.&nbsp;&nbsp;&nbsp;&nbsp;H Arendt (0.147%)\
31\.&nbsp;&nbsp;&nbsp;&nbsp;G Frege (0.138%)\
32\.&nbsp;&nbsp;&nbsp;&nbsp;GW Leibniz (0.127%)\
33\.&nbsp;&nbsp;&nbsp;&nbsp;T Adorno (0.125%)\
34\.&nbsp;&nbsp;&nbsp;&nbsp;J Searle (0.119%)\
35\.&nbsp;&nbsp;&nbsp;&nbsp;S Freud (0.115%)\
36\.&nbsp;&nbsp;&nbsp;&nbsp;T Hobbes (0.114%)\
37\.&nbsp;&nbsp;&nbsp;&nbsp;S Kripke (0.113%)\
38\.&nbsp;&nbsp;&nbsp;&nbsp;K Popper (0.112%)\
39\.&nbsp;&nbsp;&nbsp;&nbsp;M Nussbaum (0.102%)\
40\.&nbsp;&nbsp;&nbsp;&nbsp;J Piaget (0.1%)\
40\.&nbsp;&nbsp;&nbsp;&nbsp;B Williams (0.1%)\
40\.&nbsp;&nbsp;&nbsp;&nbsp;J Locke (0.1%)\
43\.&nbsp;&nbsp;&nbsp;&nbsp;W James (0.098%)\
44\.&nbsp;&nbsp;&nbsp;&nbsp;C Taylor (0.096%)\
45\.&nbsp;&nbsp;&nbsp;&nbsp;J Mc Dowell (0.095%)\
45\.&nbsp;&nbsp;&nbsp;&nbsp;W Benjamin (0.095%)\
47\.&nbsp;&nbsp;&nbsp;&nbsp;M Polanyi (0.091%)\
47\.&nbsp;&nbsp;&nbsp;&nbsp;A Goldman (0.091%)\
49\.&nbsp;&nbsp;&nbsp;&nbsp;M Dummett (0.09%)\
50\.&nbsp;&nbsp;&nbsp;&nbsp;J Fodor (0.088%)\
50\.&nbsp;&nbsp;&nbsp;&nbsp;R Carnap (0.088%)\
52\.&nbsp;&nbsp;&nbsp;&nbsp;JS Mill (0.087%)\
52\.&nbsp;&nbsp;&nbsp;&nbsp;T Nagel (0.087%)\
52\.&nbsp;&nbsp;&nbsp;&nbsp;T Williamson (0.087%)\
52\.&nbsp;&nbsp;&nbsp;&nbsp;G Harman (0.087%)\
52\.&nbsp;&nbsp;&nbsp;&nbsp;C Peirce (0.087%)\
52\.&nbsp;&nbsp;&nbsp;&nbsp;S Kierkegaard (0.087%)\
58\.&nbsp;&nbsp;&nbsp;&nbsp;T Kuhn (0.086%)\
59\.&nbsp;&nbsp;&nbsp;&nbsp;G Agamben (0.081%)\
60\.&nbsp;&nbsp;&nbsp;&nbsp;P Strawson (0.08%)\
61\.&nbsp;&nbsp;&nbsp;&nbsp;D Armstrong (0.077%)\
62\.&nbsp;&nbsp;&nbsp;&nbsp;D Dennett (0.076%)\
62\.&nbsp;&nbsp;&nbsp;&nbsp;J Lacan (0.076%)\
64\.&nbsp;&nbsp;&nbsp;&nbsp;A Badiou (0.072%)\
65\.&nbsp;&nbsp;&nbsp;&nbsp;E Cassirer (0.071%)\
66\.&nbsp;&nbsp;&nbsp;&nbsp;JJ Rousseau (0.069%)\
66\.&nbsp;&nbsp;&nbsp;&nbsp;D Chalmers (0.069%)\
66\.&nbsp;&nbsp;&nbsp;&nbsp;K Fine (0.069%)\
69\.&nbsp;&nbsp;&nbsp;&nbsp;A Plantinga (0.067%)\
70\.&nbsp;&nbsp;&nbsp;&nbsp;C Wright (0.066%)\
71\.&nbsp;&nbsp;&nbsp;&nbsp;A Mac Intyre (0.065%)\
71\.&nbsp;&nbsp;&nbsp;&nbsp;V Lenin (0.065%)\
71\.&nbsp;&nbsp;&nbsp;&nbsp;J Ranciere (0.065%)\
74\.&nbsp;&nbsp;&nbsp;&nbsp;A Whitehead (0.064%)\
74\.&nbsp;&nbsp;&nbsp;&nbsp;J Kim (0.064%)\
76\.&nbsp;&nbsp;&nbsp;&nbsp;R Nozick (0.063%)\
76\.&nbsp;&nbsp;&nbsp;&nbsp;B Van Fraassen (0.063%)\
78\.&nbsp;&nbsp;&nbsp;&nbsp;J Butler (0.061%)\
78\.&nbsp;&nbsp;&nbsp;&nbsp;I Hacking (0.061%)\
80\.&nbsp;&nbsp;&nbsp;&nbsp;GE Moore (0.06%)\
80\.&nbsp;&nbsp;&nbsp;&nbsp;R Dworkin (0.06%)\
80\.&nbsp;&nbsp;&nbsp;&nbsp;T Burge (0.06%)\
80\.&nbsp;&nbsp;&nbsp;&nbsp;R Chisholm (0.06%)\
80\.&nbsp;&nbsp;&nbsp;&nbsp;H Bergson (0.06%)\
80\.&nbsp;&nbsp;&nbsp;&nbsp;W Sellars (0.06%)\
86\.&nbsp;&nbsp;&nbsp;&nbsp;N Goodman (0.059%)\
86\.&nbsp;&nbsp;&nbsp;&nbsp;N Chomsky (0.059%)\
86\.&nbsp;&nbsp;&nbsp;&nbsp;R Brandom (0.059%)\
89\.&nbsp;&nbsp;&nbsp;&nbsp;C Korsgaard (0.058%)\
89\.&nbsp;&nbsp;&nbsp;&nbsp;J Hintikka (0.058%)\
89\.&nbsp;&nbsp;&nbsp;&nbsp;P Singer (0.058%)\
89\.&nbsp;&nbsp;&nbsp;&nbsp;H Frankfurt (0.058%)\
89\.&nbsp;&nbsp;&nbsp;&nbsp;A Honneth (0.058%)\
89\.&nbsp;&nbsp;&nbsp;&nbsp;G Priest (0.058%)\
89\.&nbsp;&nbsp;&nbsp;&nbsp;A Einstein (0.058%)\
96\.&nbsp;&nbsp;&nbsp;&nbsp;Augustine (0.057%)\
96\.&nbsp;&nbsp;&nbsp;&nbsp;M Weber (0.057%)\
96\.&nbsp;&nbsp;&nbsp;&nbsp;P Bourdieu (0.057%)\
96\.&nbsp;&nbsp;&nbsp;&nbsp;F Dretske (0.057%)\
96\.&nbsp;&nbsp;&nbsp;&nbsp;A Sen (0.057%)\
101\.&nbsp;&nbsp;&nbsp;&nbsp;P Van Inwagen (0.056%)\
101\.&nbsp;&nbsp;&nbsp;&nbsp;H Marcuse (0.056%)\
101\.&nbsp;&nbsp;&nbsp;&nbsp;P Kitcher (0.056%)\
104\.&nbsp;&nbsp;&nbsp;&nbsp;B Latour (0.055%)\
104\.&nbsp;&nbsp;&nbsp;&nbsp;B Spinoza (0.055%)\
104\.&nbsp;&nbsp;&nbsp;&nbsp;A Wood (0.055%)\
104\.&nbsp;&nbsp;&nbsp;&nbsp;D Parfit (0.055%)\
108\.&nbsp;&nbsp;&nbsp;&nbsp;C Schmitt (0.054%)\
108\.&nbsp;&nbsp;&nbsp;&nbsp;F Jackson (0.054%)\
108\.&nbsp;&nbsp;&nbsp;&nbsp;R Stalnaker (0.054%)\
108\.&nbsp;&nbsp;&nbsp;&nbsp;C Hartshorne (0.054%)\
112\.&nbsp;&nbsp;&nbsp;&nbsp;J Mackie (0.053%)\
112\.&nbsp;&nbsp;&nbsp;&nbsp;GEM Anscombe (0.053%)\
112\.&nbsp;&nbsp;&nbsp;&nbsp;E Sosa (0.053%)\
115\.&nbsp;&nbsp;&nbsp;&nbsp;J Fichte (0.052%)\
115\.&nbsp;&nbsp;&nbsp;&nbsp;N Rescher (0.052%)\
117\.&nbsp;&nbsp;&nbsp;&nbsp;P Guyer (0.051%)\
117\.&nbsp;&nbsp;&nbsp;&nbsp;F Schelling (0.051%)\
117\.&nbsp;&nbsp;&nbsp;&nbsp;M Friedman (0.051%)\
120\.&nbsp;&nbsp;&nbsp;&nbsp;S Gallagher (0.05%)\
120\.&nbsp;&nbsp;&nbsp;&nbsp;D Pritchard (0.05%)\
120\.&nbsp;&nbsp;&nbsp;&nbsp;JL Nancy (0.05%)\
123\.&nbsp;&nbsp;&nbsp;&nbsp;T Scanlon (0.048%)\
123\.&nbsp;&nbsp;&nbsp;&nbsp;P Geach (0.048%)\
123\.&nbsp;&nbsp;&nbsp;&nbsp;A Schopenhauer (0.048%)\
126\.&nbsp;&nbsp;&nbsp;&nbsp;J Lyotard (0.047%)\
126\.&nbsp;&nbsp;&nbsp;&nbsp;A Rand (0.047%)\
126\.&nbsp;&nbsp;&nbsp;&nbsp;W Ross (0.047%)\
126\.&nbsp;&nbsp;&nbsp;&nbsp;F Engels (0.047%)\
126\.&nbsp;&nbsp;&nbsp;&nbsp;C Hempel (0.047%)\
131\.&nbsp;&nbsp;&nbsp;&nbsp;D Zahavi (0.046%)\
131\.&nbsp;&nbsp;&nbsp;&nbsp;P Pettit (0.046%)\
133\.&nbsp;&nbsp;&nbsp;&nbsp;S Cavell (0.045%)\
133\.&nbsp;&nbsp;&nbsp;&nbsp;H Field (0.045%)\
133\.&nbsp;&nbsp;&nbsp;&nbsp;JL Marion (0.045%)\
133\.&nbsp;&nbsp;&nbsp;&nbsp;H Allison (0.045%)\
133\.&nbsp;&nbsp;&nbsp;&nbsp;S Zizek (0.045%)\
133\.&nbsp;&nbsp;&nbsp;&nbsp;A Smith (0.045%)\
133\.&nbsp;&nbsp;&nbsp;&nbsp;RM Hare (0.045%)\
140\.&nbsp;&nbsp;&nbsp;&nbsp;L Althusser (0.044%)\
140\.&nbsp;&nbsp;&nbsp;&nbsp;J Raz (0.044%)\
140\.&nbsp;&nbsp;&nbsp;&nbsp;G Ryle (0.044%)\
140\.&nbsp;&nbsp;&nbsp;&nbsp;G Lukacs (0.044%)\
140\.&nbsp;&nbsp;&nbsp;&nbsp;N Block (0.044%)\
140\.&nbsp;&nbsp;&nbsp;&nbsp;K Jaspers (0.044%)\
140\.&nbsp;&nbsp;&nbsp;&nbsp;M Scheler (0.044%)\
147\.&nbsp;&nbsp;&nbsp;&nbsp;A Clark (0.043%)\
147\.&nbsp;&nbsp;&nbsp;&nbsp;M Henry (0.043%)\
147\.&nbsp;&nbsp;&nbsp;&nbsp;E Gilson (0.043%)\
147\.&nbsp;&nbsp;&nbsp;&nbsp;L Strauss (0.043%)\
147\.&nbsp;&nbsp;&nbsp;&nbsp;W Alston (0.043%)\
147\.&nbsp;&nbsp;&nbsp;&nbsp;D Kaplan (0.043%)\
153\.&nbsp;&nbsp;&nbsp;&nbsp;A Kenny (0.042%)\
153\.&nbsp;&nbsp;&nbsp;&nbsp;S Shoemaker (0.042%)\
153\.&nbsp;&nbsp;&nbsp;&nbsp;JL Austin (0.042%)\
153\.&nbsp;&nbsp;&nbsp;&nbsp;S Blackburn (0.042%)\
157\.&nbsp;&nbsp;&nbsp;&nbsp;J Bennett (0.041%)\
157\.&nbsp;&nbsp;&nbsp;&nbsp;G Evans (0.041%)\
157\.&nbsp;&nbsp;&nbsp;&nbsp;J Barnes (0.041%)\
160\.&nbsp;&nbsp;&nbsp;&nbsp;J Schaffer (0.04%)\
161\.&nbsp;&nbsp;&nbsp;&nbsp;K Apel (0.039%)\
161\.&nbsp;&nbsp;&nbsp;&nbsp;A Danto (0.039%)\
161\.&nbsp;&nbsp;&nbsp;&nbsp;H Dreyfus (0.039%)\
164\.&nbsp;&nbsp;&nbsp;&nbsp;T Sider (0.038%)\
164\.&nbsp;&nbsp;&nbsp;&nbsp;M Horkheimer (0.038%)\
164\.&nbsp;&nbsp;&nbsp;&nbsp;C Peacocke (0.038%)\
164\.&nbsp;&nbsp;&nbsp;&nbsp;H Jonas (0.038%)\
168\.&nbsp;&nbsp;&nbsp;&nbsp;H Grice (0.037%)\
168\.&nbsp;&nbsp;&nbsp;&nbsp;EJ Lowe (0.037%)\
168\.&nbsp;&nbsp;&nbsp;&nbsp;J Annas (0.037%)\
168\.&nbsp;&nbsp;&nbsp;&nbsp;P Churchland (0.037%)\
168\.&nbsp;&nbsp;&nbsp;&nbsp;D Walton (0.037%)\
173\.&nbsp;&nbsp;&nbsp;&nbsp;R Swinburne (0.036%)\
173\.&nbsp;&nbsp;&nbsp;&nbsp;HLA Hart (0.036%)\
173\.&nbsp;&nbsp;&nbsp;&nbsp;T Irwin (0.036%)\
173\.&nbsp;&nbsp;&nbsp;&nbsp;D Miller (0.036%)\
173\.&nbsp;&nbsp;&nbsp;&nbsp;R Audi (0.036%)\
173\.&nbsp;&nbsp;&nbsp;&nbsp;M Devitt (0.036%)\
173\.&nbsp;&nbsp;&nbsp;&nbsp;P Feyerabend (0.036%)\
180\.&nbsp;&nbsp;&nbsp;&nbsp;J Feinberg (0.035%)\
180\.&nbsp;&nbsp;&nbsp;&nbsp;Z Bauman (0.035%)\
180\.&nbsp;&nbsp;&nbsp;&nbsp;A Ayer (0.035%)\
180\.&nbsp;&nbsp;&nbsp;&nbsp;W Salmon (0.035%)\
180\.&nbsp;&nbsp;&nbsp;&nbsp;A Mele (0.035%)\
185\.&nbsp;&nbsp;&nbsp;&nbsp;C Darwin (0.034%)\
185\.&nbsp;&nbsp;&nbsp;&nbsp;JJ Thomson (0.034%)\
185\.&nbsp;&nbsp;&nbsp;&nbsp;D Wiggins (0.034%)\
185\.&nbsp;&nbsp;&nbsp;&nbsp;N Malcolm (0.034%)\
185\.&nbsp;&nbsp;&nbsp;&nbsp;CS Lewis (0.034%)\
185\.&nbsp;&nbsp;&nbsp;&nbsp;M Smith (0.034%)\
191\.&nbsp;&nbsp;&nbsp;&nbsp;J Patocka (0.033%)\
191\.&nbsp;&nbsp;&nbsp;&nbsp;C Wilson (0.033%)\
193\.&nbsp;&nbsp;&nbsp;&nbsp;F Brentano (0.032%)\
193\.&nbsp;&nbsp;&nbsp;&nbsp;P Hadot (0.032%)\
193\.&nbsp;&nbsp;&nbsp;&nbsp;I Lakatos (0.032%)\
193\.&nbsp;&nbsp;&nbsp;&nbsp;E Dussel (0.032%)\
193\.&nbsp;&nbsp;&nbsp;&nbsp;JM Fischer (0.032%)\
193\.&nbsp;&nbsp;&nbsp;&nbsp;W Lycan (0.032%)\
193\.&nbsp;&nbsp;&nbsp;&nbsp;E Sober (0.032%)\
200\.&nbsp;&nbsp;&nbsp;&nbsp;N Luhmann (0.031%)\
200\.&nbsp;&nbsp;&nbsp;&nbsp;P Foot (0.031%)\
200\.&nbsp;&nbsp;&nbsp;&nbsp;R Brandt (0.031%)\
200\.&nbsp;&nbsp;&nbsp;&nbsp;M Walzer (0.031%)\
200\.&nbsp;&nbsp;&nbsp;&nbsp;J Dancy (0.031%)\
200\.&nbsp;&nbsp;&nbsp;&nbsp;G Bachelard (0.031%)\
200\.&nbsp;&nbsp;&nbsp;&nbsp;R Adams (0.031%)\
200\.&nbsp;&nbsp;&nbsp;&nbsp;D Henrich (0.031%)\
200\.&nbsp;&nbsp;&nbsp;&nbsp;A Gibbard (0.031%)\
209\.&nbsp;&nbsp;&nbsp;&nbsp;L Laudan (0.03%)\
209\.&nbsp;&nbsp;&nbsp;&nbsp;G Cohen (0.03%)\
209\.&nbsp;&nbsp;&nbsp;&nbsp;EO Wilson (0.03%)\
209\.&nbsp;&nbsp;&nbsp;&nbsp;G Vattimo (0.03%)\
209\.&nbsp;&nbsp;&nbsp;&nbsp;M Burnyeat (0.03%)\
209\.&nbsp;&nbsp;&nbsp;&nbsp;Q Skinner (0.03%)\
209\.&nbsp;&nbsp;&nbsp;&nbsp;J Broome (0.03%)\
209\.&nbsp;&nbsp;&nbsp;&nbsp;J Perry (0.03%)\
209\.&nbsp;&nbsp;&nbsp;&nbsp;F Varela (0.03%)\
209\.&nbsp;&nbsp;&nbsp;&nbsp;A Tarski (0.03%)\
219\.&nbsp;&nbsp;&nbsp;&nbsp;G Vlastos (0.029%)\
219\.&nbsp;&nbsp;&nbsp;&nbsp;T Huxley (0.029%)\
219\.&nbsp;&nbsp;&nbsp;&nbsp;M Bratman (0.029%)\
219\.&nbsp;&nbsp;&nbsp;&nbsp;I Newton (0.029%)\
219\.&nbsp;&nbsp;&nbsp;&nbsp;I Berlin (0.029%)\
219\.&nbsp;&nbsp;&nbsp;&nbsp;G Marcel (0.029%)\
219\.&nbsp;&nbsp;&nbsp;&nbsp;R Collingwood (0.029%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;M Buber (0.028%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;S Darwall (0.028%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;R Barthes (0.028%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;S Shapiro (0.028%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;T Horgan (0.028%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;J Waldron (0.028%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;N Carroll (0.028%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;G Berkeley (0.028%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;A Steinbock (0.028%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;K Lehrer (0.028%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;U Eco (0.028%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;K Walton (0.028%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;RG Millikan (0.027%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;G Strawson (0.027%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;H Blumenberg (0.027%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;C Fabro (0.027%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;M Tye (0.027%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;M Fricker (0.027%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;D Haraway (0.027%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;E Balibar (0.027%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;J Elster (0.027%)\
247\.&nbsp;&nbsp;&nbsp;&nbsp;W Kaufmann (0.026%)\
247\.&nbsp;&nbsp;&nbsp;&nbsp;C Kahn (0.026%)\
247\.&nbsp;&nbsp;&nbsp;&nbsp;J Maritain (0.026%)\
247\.&nbsp;&nbsp;&nbsp;&nbsp;C Mills (0.026%)\
247\.&nbsp;&nbsp;&nbsp;&nbsp;O Oneill (0.026%)\
247\.&nbsp;&nbsp;&nbsp;&nbsp;A Camus (0.026%)\
247\.&nbsp;&nbsp;&nbsp;&nbsp;A Thomasson (0.026%)\
247\.&nbsp;&nbsp;&nbsp;&nbsp;R Abulad (0.026%)\
247\.&nbsp;&nbsp;&nbsp;&nbsp;T Parsons (0.026%)\
247\.&nbsp;&nbsp;&nbsp;&nbsp;N Fraser (0.026%)\
247\.&nbsp;&nbsp;&nbsp;&nbsp;R Feldman (0.026%)\
247\.&nbsp;&nbsp;&nbsp;&nbsp;R Bernstein (0.026%)\
247\.&nbsp;&nbsp;&nbsp;&nbsp;J Hawthorne (0.026%)\
247\.&nbsp;&nbsp;&nbsp;&nbsp;W Dilthey (0.026%)\
247\.&nbsp;&nbsp;&nbsp;&nbsp;B Stroud (0.026%)\
247\.&nbsp;&nbsp;&nbsp;&nbsp;F Bacon (0.026%)\
263\.&nbsp;&nbsp;&nbsp;&nbsp;D Kahneman (0.025%)\
263\.&nbsp;&nbsp;&nbsp;&nbsp;C Wolff (0.025%)\
263\.&nbsp;&nbsp;&nbsp;&nbsp;J Stanley (0.025%)\
263\.&nbsp;&nbsp;&nbsp;&nbsp;J Baudrillard (0.025%)\
263\.&nbsp;&nbsp;&nbsp;&nbsp;G Von Wright (0.025%)\
263\.&nbsp;&nbsp;&nbsp;&nbsp;R Boyd (0.025%)\
263\.&nbsp;&nbsp;&nbsp;&nbsp;R Pippin (0.025%)\
263\.&nbsp;&nbsp;&nbsp;&nbsp;K Bach (0.025%)\
263\.&nbsp;&nbsp;&nbsp;&nbsp;P Sloterdijk (0.025%)\
263\.&nbsp;&nbsp;&nbsp;&nbsp;N Salmon (0.025%)\
263\.&nbsp;&nbsp;&nbsp;&nbsp;T Reid (0.025%)\
263\.&nbsp;&nbsp;&nbsp;&nbsp;R Sorabji (0.025%)\
263\.&nbsp;&nbsp;&nbsp;&nbsp;D Gauthier (0.025%)\
263\.&nbsp;&nbsp;&nbsp;&nbsp;E Fink (0.025%)\
263\.&nbsp;&nbsp;&nbsp;&nbsp;N Smith (0.025%)\
278\.&nbsp;&nbsp;&nbsp;&nbsp;C Broad (0.024%)\
278\.&nbsp;&nbsp;&nbsp;&nbsp;P Boghossian (0.024%)\
278\.&nbsp;&nbsp;&nbsp;&nbsp;D Hilbert (0.024%)\
278\.&nbsp;&nbsp;&nbsp;&nbsp;K Godel (0.024%)\
278\.&nbsp;&nbsp;&nbsp;&nbsp;E Mayr (0.024%)\
278\.&nbsp;&nbsp;&nbsp;&nbsp;J Dunn (0.024%)\
278\.&nbsp;&nbsp;&nbsp;&nbsp;P Horwich (0.024%)\
278\.&nbsp;&nbsp;&nbsp;&nbsp;D Papineau (0.024%)\
278\.&nbsp;&nbsp;&nbsp;&nbsp;S De Beauvoir (0.024%)\
278\.&nbsp;&nbsp;&nbsp;&nbsp;S Gould (0.024%)\
278\.&nbsp;&nbsp;&nbsp;&nbsp;S Haack (0.024%)\
278\.&nbsp;&nbsp;&nbsp;&nbsp;J Cohen (0.024%)\
278\.&nbsp;&nbsp;&nbsp;&nbsp;I Young (0.024%)\
278\.&nbsp;&nbsp;&nbsp;&nbsp;J Earman (0.024%)\
278\.&nbsp;&nbsp;&nbsp;&nbsp;J Prinz (0.024%)\
278\.&nbsp;&nbsp;&nbsp;&nbsp;H Reichenbach (0.024%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;F Recanati (0.023%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;S Yablo (0.023%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;J Miller (0.023%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;P Hacker (0.023%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;E Thompson (0.023%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;J Caputo (0.023%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;B Croce (0.023%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;F Ramsey (0.023%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;F Van Eemeren (0.023%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;A Baier (0.023%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;A Koyre (0.023%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;W Kymlicka (0.023%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;R Giere (0.023%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;H Castaneda (0.023%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;G Simmel (0.023%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;R Wollheim (0.023%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;J Greco (0.023%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;T Pogge (0.023%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;P Railton (0.023%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;R Scruton (0.023%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;FA Hayek (0.023%)\
294\.&nbsp;&nbsp;&nbsp;&nbsp;B Smith (0.023%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;AN Prior (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;F Fanon (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;A Damasio (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;L Floridi (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;S Stich (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;S Toulmin (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;M Slote (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;F Jameson (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;H Price (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;R Dawkins (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;R Bhaskar (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;J Haidt (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;R Shusterman (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;P Unger (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;J Levinson (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;E Anderson (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;P Carruthers (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;B Pascal (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;J Bentham (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;N Daniels (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;A Buchanan (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;JJ Smart (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;E Durkheim (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;M Blanchot (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;M Gilbert (0.022%)\
316\.&nbsp;&nbsp;&nbsp;&nbsp;H Sidgwick (0.022%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;S Benhabib (0.021%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;B Stiegler (0.021%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;G Rosen (0.021%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;S Scheffler (0.021%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;M Johnston (0.021%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;M Heller (0.021%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;Cicero (0.021%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;G Wright (0.021%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;S Haslanger (0.021%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;B Skyrms (0.021%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;D Hull (0.021%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;G Lakoff (0.021%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;M Garcia Carpintero (0.021%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;M Tooley (0.021%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;C Perelman (0.021%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;J Margolis (0.021%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;J Woodward (0.021%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;R Solomon (0.021%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;I Murdoch (0.021%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;S Soames (0.021%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;E Stump (0.021%)\
342\.&nbsp;&nbsp;&nbsp;&nbsp;R Arneson (0.021%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;L Irigaray (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;T Fuchs (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;A Schutz (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;JW Goethe (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;R Koselleck (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;S Wolf (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;A Bird (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;S Kagan (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;D Christensen (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;R Ingarden (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;J Gibson (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;S Schiffer (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;G Santayana (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;H Maturana (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;J Brown (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;L Zagzebski (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;O Poggeler (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;GJ Ortega (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;G Canguilhem (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;M Williams (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;M Zambrano (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;M Schroeder (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;W Heisenberg (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;M Black (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;J Greene (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;LW Beck (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;J Cottingham (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;VM Guzman (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;A Flew (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;E Stein (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;M Huemer (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;G Boolos (0.02%)\
364\.&nbsp;&nbsp;&nbsp;&nbsp;R Penrose (0.02%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;C Mc Ginn (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;N Cartwright (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;J Lackey (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;G Currie (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;G Bataille (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;M Lipman (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;P Simons (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;D Mellor (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;G Watson (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;S Weil (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;M Frede (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;E Laclau (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;C Mouffe (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;B Waldenfels (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;R Hursthouse (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;M Ruse (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;J Kvanvig (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;M Tomasello (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;M Sandel (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;A Giddens (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;J Stewart (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;A Long (0.019%)\
397\.&nbsp;&nbsp;&nbsp;&nbsp;D Diderot (0.019%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;N Wolterstorff (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;T Crane (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;R Taylor (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;H Poincare (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;E Bloch (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;K Nielsen (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;M Clark (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;JC Beall (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;J Owens (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;J Harris (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;G Lloyd (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;D Sedley (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;C Levi Strauss (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;A Gewirth (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;K Wiredu (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;H Weyl (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;K Lowith (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;HJ Glock (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;E Mach (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;C Glymour (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;N Belnap (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;W Bechtel (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;A Noe (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;R Popkin (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;G Graham (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;P Duhem (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;N Bostrom (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;O Hoffe (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;S Cohen (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;D Bohm (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;M Zimmerman (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;B Leiter (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;K Donnellan (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;R Sokolowski (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;G Scholem (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;J Conant (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;R Esposito (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;A Church (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;J Campbell (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;D Pereboom (0.018%)\
420\.&nbsp;&nbsp;&nbsp;&nbsp;M Bunge (0.018%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;D Bell (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;L Baker (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;G Baker (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;J Ladyman (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;P Maddy (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;JM Cooper (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;A Byrne (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;Avicenna (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;H Kelsen (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;E Schwitzgebel (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;P Berger (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;A Gramsci (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;F Schiller (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;E Tugendhat (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;F Guattari (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;T Beauchamp (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;R Williams (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;H Kornblith (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;P Tillich (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;R Bernasconi (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;B Lonergan (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;E Berti (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;A Nehamas (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;SO Hansson (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;WKC Guthrie (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;R Routley (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;W Chan (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;J Hick (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;R Kane (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;S Feferman (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;JD Velleman (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;A Grunbaum (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;J Pocock (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;S Davies (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;N Bohr (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;R Martin (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;J Heil (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;W Jaeger (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;E Nagel (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;R Jeffrey (0.017%)\
461\.&nbsp;&nbsp;&nbsp;&nbsp;M Schlick (0.017%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;D Enoch (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;J Mc Mahan (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;K Rahner (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;R Tuomela (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;JL Pollock (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;E Said (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;R Langton (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;R Goodin (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;P Thagard (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;S French (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;H Diels (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;P Suppes (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;A Cortina (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;C Jung (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;C Diamond (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;J Barwise (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;J Lear (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;J Van Cleve (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;R Hanna (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;AC Graham (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;B Barry (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;H Simon (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;E Schrodinger (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;I Levi (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;T Metz (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;E Fromm (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;K Ameriks (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;E Zalta (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;F Fukuyama (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;W Brown (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;D Copp (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;H White (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;H Cohen (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;S Shapin (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;R Fogelin (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;D Brink (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;F Suarez (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;M Eliade (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;O Bazaluk (0.016%)\
502\.&nbsp;&nbsp;&nbsp;&nbsp;W Frankena (0.016%)

A few observations. First, I've now been at uni studying philosophy for more than a decade, but I have never read anything by two of the authors in the top 5. Curious, that. Second, Aristotle and Plato are both in the top 15 even though they have been dead for more than 2000 years. I'm not sure there are many other disciplines for which something like that is true (perhaps Religious Studies?). Third, the first non-philosopher on this list (as far as I can see) is a psychologists, Sigmund Freud (#35), who has not been very influential in his own discipline for decades. Fourth, the authors who top Schwitzgebel's ranking also end up near the top of the current list. For instance, almost everyone in his top 10 is included in my top 50 (the two exceptions are Thomas Nagel and Timothy Williamson, tied at #52). The order is different (e.g., Williamson is SG's #6 while Nagel is #10). I think this is explained by the fact that my data cover the last 50 years, while articles on the SEP tend to be more recent. Finally, a number of people in Schwitzgebel's comments asked questions/expressed dismay about the low rankings of various (European) authors. On the current list, these authors tend to rank much higher: Derrida (ranked #5), Foucault (#7), Merleau-Ponty (#18), Gadamer (#29) and  Adorno (#33), for example, are all in the top 50.

A brief comment on that last observation: Schwitzgebel makes it clear that his ranking captures current influence in 'mainstream Anglophone philosophy,' and so the fact that Derrida, Foucault et al. are not particularly high up on his list is not surprising. This raises the question what the current ranking captures. Mostly, the answer depends on what one thinks of the selection of journals the ranking is based on. In my experience, the WoS and PP both err on the side of being overly comprehensive. If so, then it is not on its face unreasonable to claim that the current list (based, as it is, on a list of journals indexed on both platforms) captures (something like) influence in (published) academic philosophy during the last 50 years. Others may disagree, of course.

Since the data are longitudinal, we can also look at how citation rates for different authors changed during the last 50 years. Figure 1 shows the top 25 ranked authors over time (bottom panel). The top panel shows all authors who made it into the top 25 at one point in time or another (darker gray). The figure is interactive; hover over a bar, and it will highlight the corresponding rank trajectory over time (and vice versa).

<iframe src="https://prehren.github.io/something-of-crunch/assets/html/2024-11-13/figure1NEW.html" title="Figure 1. Development over time of the top 25." style="border:none; margin:0 auto; display: block; padding-bottom:1em; overflow:hidden;" scrolling="no" id="IFrameThatAutoResizes"></iframe>
<p style="text-align:center; font-size: 0.85em; padding-right: 30px; padding-left: 30px;">Figure 1. Development over time of the top 25.</p>
<br>

Two brief observations. First, in 1971-75, Aristotle and Plato were #1 and #2. Since then, however, both of these authors lost considerable ground and have now fallen out of the top 10. I think this fits well with the finding that the proportion of history of philosophy papers published in philosophy's top generalist journals has been on the decline in the last 50 years (described [here](https://prehren.github.io/something-of-crunch/2023/12/12/publishing-trends.html)), in that both results suggest that the history of philosophy has lost the spotlight to some extent. Second, apart from Aristotle, the last 50 years have seen only _two_ other authors take the #1 spot: Heidegger and Kant. Since the mid-1980s, the latter two have been trading the top spot back and forth (currently, Heidegger's #1 and Kant's #2). That is some impressively stable influence!
