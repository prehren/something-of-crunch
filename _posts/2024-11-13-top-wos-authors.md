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

While there is not a huge amount of information here (e.g., no article titles; no publisher information; no editors), almost all cited items include author names.[^1] That's good. What is less ideal is that for most authors, we only get initials, not full first names. Yet many first initial-last name combinations are going to be shared by lots of authors. 

[^1]: Or, rather, the name of the first author—my sense is that co-authors are generally omitted. This isn't much of a limitation, though, [given that the vast majority of philosophy articles are single-authored](https://prehren.github.io/something-of-crunch/2023/12/20/co-authorship.html).

One possible way to get around this problem would be to only keep references with at least one full first name. However, this strategy has at least two major problems. First, the strategy filters out references to works by authors without a first name (e.g., Aristotle, Plato, Plutarch, Averroes) or authors who usually get referred to only by last name. Of course, it is possible to simply keep these references in the dataset. This introduces a different problem, though. Consider Aristotle. Aristotle virtually always get referenced as 'Aristotle.' This means that the new filtered dataset would include (almost) all references to Aristotle's works. Compare that to an author like David Lewis, who usually gets referenced either as 'D. Lewis' or 'David Lewis.' The filtered dataset would only contain instances of the second case, but not instances of the first case. As a result, Aristotle's citation count would be inflated (likely dramatically inflated) compared to David Lewis' citation count.

The second problem is that only keeping references with full author names results in inaccurate citation counts if the ratio of citations with full first names to citations with just initial is different for different authors. Suppose that when people reference David Lewis, 20% of the time, they do so as 'David Lewis', while the remaining 80% of the time, as 'D. Lewis' (or 'D.K. Lewis'). In that case, the new filtered dataset would include only 20% of all Lewis-references present in the original dataset. If this ratio is the same (or at least similar) for other authors, then everything is fine. However, suppose that Immanuel Kant gets referenced as 'Immanuel Kant' 50% of the time. If so, then the new filtered dataset would lead me to substantially underestimate Lewis' citation count compared to Kant's citation count. Unfortunately, what I have just described is what the data in fact look like: 66% of references to the last name Lewis are to 'D. Lewis' or 'D.K. Lewis', while only 14% are to 'David Lewis;' in contrast, 46% of references to the last name Kant are to 'Immanuel Kant,' another 46% are to 'I. Kant.'

Filtering out rows with only first initials, then, is unfortunately not an option. Instead, I decided to convert full first names into first initials (e.g., Immanuel Kant -> I Kant, David Lewis -> D Lewis). This means that I get to keep most of the original data. The trade-off is that my results will need to be taken with a grain of salt: Many first initial(s)-last name combinations are going to be shared by multiple authors. That said, there's reason to believe that this limitation isn't too severe. I restricted the data to rows with full first names available, and then calculated the proportion of full first name(s)-last name combinations associated with each first initial(s)-last name combination in the top 500 (see below). On average, the most common full first name(s)-last name combination accounted for over 90% of all occurences of a given first initial(s)-last name combination. In other words, it seems that the first initial(s)-last name combinations in the top 500 generally refer to a single author, instead of a hodgepode of multiple different authors.

On to data cleaning.[^2] Some authors frequently get referenced only by their last name (e.g., Kant, Marx, Hume, Wittgenstein). To match these occurences to first initial(s)-last name combinations, I calculated the proportion of first initial(s)-last name combinations for each last name in the dataset. Here are the first ten lines of the results for Kant:

```
   full_nameINITIALS     n     N     prop
   <chr>             <int> <int>    <dbl>
 1 I Kant            25396 27340 0.929   
 2 Kant               1327 27340 0.0485  
 3 E Kant              413 27340 0.0151  
 4 IMMANUEL Kant        46 27340 0.00168 
 5 H Kant               13 27340 0.000475
 6 L Kant               13 27340 0.000475
 7 T Kant               10 27340 0.000366
 8 D Kant                9 27340 0.000329
 9 A Kant                8 27340 0.000293
10 P Kant                8 27340 0.000293
```

We see that for Kant, more than 90% of references are to I Kant. The second most common reference is just to the last name Kant. In this situation, it strikes me as reasonable to assume that these references to the last name mean I Kant. Therefore, whenever it was the case for a given last name that the most common reference was to a first initial(s)-that last name combination and the second most common reference was to just that last name, I replaced all references to just that last name with the most common first initial(s)-last name combination.

If articles in the same in the same journal cited two authors with the same last name but different first initials in the same five year time span (see below) _and_ the first initials started with the same letter _and_ one of the two sets of first initials was an ordered subset of the other.

[^2]: Given that I am dealing with millions of references, extensive manual data cleaning was out of the question.

Some of the journals the WoS lists under Philosophy strike me as questionable. For instance: Are the _Nursing History Review_, the _Journal of Medical Biography_, the _Journal for the History of Astronomy_ or _Engineering Studies_ really philosophy journals? I think not. As a result, I decided to remove all journals from the dataset that are not also indexed on PhilPapers. This method isn't perfect, of course, but I think it is good enough.

After these (and some other, more boring exclusions having to do with missing data), I was  left with a final dataset containing ~1.6 million references from articles published in 269 journals between 1975 and 2024.

There are different ways to quantify _most cited author_. One is to just count up citations. I don't think that is a particularly helpful approach, however, because (a) philosophers today cite a lot more stuff than did philosophers 50 years ago and (b) many more philosophy articles get published today than did 50 years ago. This means that raw citation counts as a measure of influence are biased (heavily) in favor of recent citations.

I instead chose to go with proportions. Note that, by itself, this doesn't solve (a) and (b). To illustrate [I'll focus on (a), but the problem with (b) is analogous]: Suppose we are looking at two years, 1990 and 2020, for one journal A. In 1990, A published 10 articles, while in 2020, it published 100 articles. Suppose further that articles in 1990 and 2020 cite about the same number of references (say, 10). If an author was very influential in the pages of A in 1990 (say, 10% of all citations were to this author's work) but no longer that influential in 2020 (say, 1%), then we get an overall proportion of citations to this author in A of ~2%. If the roles of 1990 and 2020 had been reversed, however, then this overall proportion would have been ~9%. Yet it looks like this differences is just an artifact of the fact that A published fewer articles in 1990 than in 2020.

To avoid (a) and (b), I divided my data into time bins (I chose five years), calculated the proportion of citations received by a given author in each bin separately, and only then calculated the mean across all of these bins. I also did the same thing for journals; otherwise, the results would be biased towards influence in journals that publish more articles and/or have higher average citation rates.

Here are the top 510 (brackets show mean percentages):

1\.&nbsp;&nbsp;&nbsp;&nbsp;M Heidegger (0.676%)\
2\.&nbsp;&nbsp;&nbsp;&nbsp;I Kant (0.615%)\
3\.&nbsp;&nbsp;&nbsp;&nbsp;E Husserl (0.445%)\
4\.&nbsp;&nbsp;&nbsp;&nbsp;J Derrida (0.381%)\
5\.&nbsp;&nbsp;&nbsp;&nbsp;M Foucault (0.363%)\
6\.&nbsp;&nbsp;&nbsp;&nbsp;Aristotle (0.358%)\
7\.&nbsp;&nbsp;&nbsp;&nbsp;GWF Hegel (0.309%)\
8\.&nbsp;&nbsp;&nbsp;&nbsp;L Wittgenstein (0.281%)\
9\.&nbsp;&nbsp;&nbsp;&nbsp;G Deleuze (0.271%)\
10\.&nbsp;&nbsp;&nbsp;&nbsp;D Lewis (0.263%)\
11\.&nbsp;&nbsp;&nbsp;&nbsp;F Nietzsche (0.259%)\
12\.&nbsp;&nbsp;&nbsp;&nbsp;J Habermas (0.242%)\
13\.&nbsp;&nbsp;&nbsp;&nbsp;Plato (0.216%)\
14\.&nbsp;&nbsp;&nbsp;&nbsp;D Hume (0.21%)\
14\.&nbsp;&nbsp;&nbsp;&nbsp;W Quine (0.21%)\
16\.&nbsp;&nbsp;&nbsp;&nbsp;J Rawls (0.205%)\
17\.&nbsp;&nbsp;&nbsp;&nbsp;K Marx (0.202%)\
18\.&nbsp;&nbsp;&nbsp;&nbsp;M Merleau Ponty (0.186%)\
19\.&nbsp;&nbsp;&nbsp;&nbsp;JP Sartre (0.181%)\
20\.&nbsp;&nbsp;&nbsp;&nbsp;J Dewey (0.177%)\
21\.&nbsp;&nbsp;&nbsp;&nbsp;D Davidson (0.176%)\
22\.&nbsp;&nbsp;&nbsp;&nbsp;B Russell (0.169%)\
23\.&nbsp;&nbsp;&nbsp;&nbsp;P Ricoeur (0.168%)\
24\.&nbsp;&nbsp;&nbsp;&nbsp;H Putnam (0.166%)\
25\.&nbsp;&nbsp;&nbsp;&nbsp;E Levinas (0.161%)\
26\.&nbsp;&nbsp;&nbsp;&nbsp;R Rorty (0.159%)\
27\.&nbsp;&nbsp;&nbsp;&nbsp;H Arendt (0.156%)\
28\.&nbsp;&nbsp;&nbsp;&nbsp;R Descartes (0.153%)\
29\.&nbsp;&nbsp;&nbsp;&nbsp;G Frege (0.151%)\
30\.&nbsp;&nbsp;&nbsp;&nbsp;HG Gadamer (0.15%)\
31\.&nbsp;&nbsp;&nbsp;&nbsp;T Aquinas (0.148%)\
32\.&nbsp;&nbsp;&nbsp;&nbsp;GW Leibniz (0.134%)\
33\.&nbsp;&nbsp;&nbsp;&nbsp;T Adorno (0.123%)\
34\.&nbsp;&nbsp;&nbsp;&nbsp;S Kripke (0.117%)\
35\.&nbsp;&nbsp;&nbsp;&nbsp;M Nussbaum (0.114%)\
36\.&nbsp;&nbsp;&nbsp;&nbsp;J Piaget (0.113%)\
36\.&nbsp;&nbsp;&nbsp;&nbsp;S Freud (0.113%)\
38\.&nbsp;&nbsp;&nbsp;&nbsp;T Hobbes (0.112%)\
39\.&nbsp;&nbsp;&nbsp;&nbsp;W James (0.11%)\
40\.&nbsp;&nbsp;&nbsp;&nbsp;B Williams (0.106%)\
41\.&nbsp;&nbsp;&nbsp;&nbsp;J Mc Dowell (0.104%)\
42\.&nbsp;&nbsp;&nbsp;&nbsp;K Popper (0.101%)\
43\.&nbsp;&nbsp;&nbsp;&nbsp;W Benjamin (0.1%)\
44\.&nbsp;&nbsp;&nbsp;&nbsp;C Peirce (0.098%)\
45\.&nbsp;&nbsp;&nbsp;&nbsp;J Locke (0.097%)\
45\.&nbsp;&nbsp;&nbsp;&nbsp;A Goldman (0.097%)\
47\.&nbsp;&nbsp;&nbsp;&nbsp;C Taylor (0.096%)\
48\.&nbsp;&nbsp;&nbsp;&nbsp;T Williamson (0.094%)\
49\.&nbsp;&nbsp;&nbsp;&nbsp;M Dummett (0.092%)\
49\.&nbsp;&nbsp;&nbsp;&nbsp;J Fodor (0.092%)\
51\.&nbsp;&nbsp;&nbsp;&nbsp;G Harman (0.091%)\
51\.&nbsp;&nbsp;&nbsp;&nbsp;S Kierkegaard (0.091%)\
53\.&nbsp;&nbsp;&nbsp;&nbsp;T Nagel (0.088%)\
54\.&nbsp;&nbsp;&nbsp;&nbsp;R Carnap (0.085%)\
55\.&nbsp;&nbsp;&nbsp;&nbsp;JS Mill (0.084%)\
56\.&nbsp;&nbsp;&nbsp;&nbsp;P Strawson (0.081%)\
56\.&nbsp;&nbsp;&nbsp;&nbsp;G Agamben (0.081%)\
58\.&nbsp;&nbsp;&nbsp;&nbsp;JR Searle (0.08%)\
58\.&nbsp;&nbsp;&nbsp;&nbsp;D Dennett (0.08%)\
60\.&nbsp;&nbsp;&nbsp;&nbsp;T Kuhn (0.079%)\
61\.&nbsp;&nbsp;&nbsp;&nbsp;D Chalmers (0.078%)\
62\.&nbsp;&nbsp;&nbsp;&nbsp;E Cassirer (0.074%)\
62\.&nbsp;&nbsp;&nbsp;&nbsp;C Wright (0.074%)\
64\.&nbsp;&nbsp;&nbsp;&nbsp;K Fine (0.073%)\
64\.&nbsp;&nbsp;&nbsp;&nbsp;D Armstrong (0.073%)\
66\.&nbsp;&nbsp;&nbsp;&nbsp;A Mac Intyre (0.071%)\
66\.&nbsp;&nbsp;&nbsp;&nbsp;J Ranciere (0.071%)\
68\.&nbsp;&nbsp;&nbsp;&nbsp;J Lacan (0.07%)\
69\.&nbsp;&nbsp;&nbsp;&nbsp;J Kim (0.069%)\
70\.&nbsp;&nbsp;&nbsp;&nbsp;A Plantinga (0.068%)\
70\.&nbsp;&nbsp;&nbsp;&nbsp;T Burge (0.068%)\
72\.&nbsp;&nbsp;&nbsp;&nbsp;A Badiou (0.067%)\
72\.&nbsp;&nbsp;&nbsp;&nbsp;JJ Rousseau (0.067%)\
74\.&nbsp;&nbsp;&nbsp;&nbsp;J Butler (0.066%)\
75\.&nbsp;&nbsp;&nbsp;&nbsp;C Korsgaard (0.065%)\
75\.&nbsp;&nbsp;&nbsp;&nbsp;R Brandom (0.065%)\
75\.&nbsp;&nbsp;&nbsp;&nbsp;W Sellars (0.065%)\
78\.&nbsp;&nbsp;&nbsp;&nbsp;G Priest (0.063%)\
78\.&nbsp;&nbsp;&nbsp;&nbsp;A Honneth (0.063%)\
78\.&nbsp;&nbsp;&nbsp;&nbsp;C Schmitt (0.063%)\
81\.&nbsp;&nbsp;&nbsp;&nbsp;N Goodman (0.062%)\
81\.&nbsp;&nbsp;&nbsp;&nbsp;F Dretske (0.062%)\
81\.&nbsp;&nbsp;&nbsp;&nbsp;I Hacking (0.062%)\
81\.&nbsp;&nbsp;&nbsp;&nbsp;B Van Fraassen (0.062%)\
85\.&nbsp;&nbsp;&nbsp;&nbsp;H Frankfurt (0.061%)\
85\.&nbsp;&nbsp;&nbsp;&nbsp;P Bourdieu (0.061%)\
85\.&nbsp;&nbsp;&nbsp;&nbsp;R Stalnaker (0.061%)\
88\.&nbsp;&nbsp;&nbsp;&nbsp;M Weber (0.06%)\
88\.&nbsp;&nbsp;&nbsp;&nbsp;F Jackson (0.06%)\
90\.&nbsp;&nbsp;&nbsp;&nbsp;P Van Inwagen (0.059%)\
91\.&nbsp;&nbsp;&nbsp;&nbsp;E Sosa (0.058%)\
91\.&nbsp;&nbsp;&nbsp;&nbsp;H Bergson (0.058%)\
91\.&nbsp;&nbsp;&nbsp;&nbsp;R Dworkin (0.058%)\
91\.&nbsp;&nbsp;&nbsp;&nbsp;N Chomsky (0.058%)\
91\.&nbsp;&nbsp;&nbsp;&nbsp;R Chisholm (0.058%)\
96\.&nbsp;&nbsp;&nbsp;&nbsp;G Anscombe (0.057%)\
96\.&nbsp;&nbsp;&nbsp;&nbsp;J Hintikka (0.057%)\
98\.&nbsp;&nbsp;&nbsp;&nbsp;P Singer (0.056%)\
98\.&nbsp;&nbsp;&nbsp;&nbsp;D Pritchard (0.056%)\
98\.&nbsp;&nbsp;&nbsp;&nbsp;D Parfit (0.056%)\
98\.&nbsp;&nbsp;&nbsp;&nbsp;A Wood (0.056%)\
98\.&nbsp;&nbsp;&nbsp;&nbsp;A Sen (0.056%)\
103\.&nbsp;&nbsp;&nbsp;&nbsp;B Latour (0.055%)\
103\.&nbsp;&nbsp;&nbsp;&nbsp;J Mackie (0.055%)\
103\.&nbsp;&nbsp;&nbsp;&nbsp;P Kitcher (0.055%)\
103\.&nbsp;&nbsp;&nbsp;&nbsp;S Gallagher (0.055%)\
107\.&nbsp;&nbsp;&nbsp;&nbsp;P Guyer (0.054%)\
107\.&nbsp;&nbsp;&nbsp;&nbsp;F Schelling (0.054%)\
107\.&nbsp;&nbsp;&nbsp;&nbsp;GE Moore (0.054%)\
107\.&nbsp;&nbsp;&nbsp;&nbsp;H Marcuse (0.054%)\
107\.&nbsp;&nbsp;&nbsp;&nbsp;R Nozick (0.054%)\
112\.&nbsp;&nbsp;&nbsp;&nbsp;D Zahavi (0.052%)\
112\.&nbsp;&nbsp;&nbsp;&nbsp;N Rescher (0.052%)\
112\.&nbsp;&nbsp;&nbsp;&nbsp;JL Nancy (0.052%)\
115\.&nbsp;&nbsp;&nbsp;&nbsp;Augustine (0.051%)\
115\.&nbsp;&nbsp;&nbsp;&nbsp;P Pettit (0.051%)\
115\.&nbsp;&nbsp;&nbsp;&nbsp;B Spinoza (0.051%)\
118\.&nbsp;&nbsp;&nbsp;&nbsp;JL Marion (0.05%)\
118\.&nbsp;&nbsp;&nbsp;&nbsp;T Scanlon (0.05%)\
118\.&nbsp;&nbsp;&nbsp;&nbsp;J Fichte (0.05%)\
121\.&nbsp;&nbsp;&nbsp;&nbsp;M Henry (0.049%)\
121\.&nbsp;&nbsp;&nbsp;&nbsp;H Field (0.049%)\
121\.&nbsp;&nbsp;&nbsp;&nbsp;A Whitehead (0.049%)\
121\.&nbsp;&nbsp;&nbsp;&nbsp;M Friedman (0.049%)\
121\.&nbsp;&nbsp;&nbsp;&nbsp;J Lyotard (0.049%)\
126\.&nbsp;&nbsp;&nbsp;&nbsp;P Geach (0.048%)\
126\.&nbsp;&nbsp;&nbsp;&nbsp;A Clark (0.048%)\
126\.&nbsp;&nbsp;&nbsp;&nbsp;A Schopenhauer (0.048%)\
126\.&nbsp;&nbsp;&nbsp;&nbsp;J Raz (0.048%)\
130\.&nbsp;&nbsp;&nbsp;&nbsp;W Ross (0.047%)\
130\.&nbsp;&nbsp;&nbsp;&nbsp;N Block (0.047%)\
132\.&nbsp;&nbsp;&nbsp;&nbsp;H Allison (0.046%)\
132\.&nbsp;&nbsp;&nbsp;&nbsp;M Scheler (0.046%)\
132\.&nbsp;&nbsp;&nbsp;&nbsp;D Kaplan (0.046%)\
132\.&nbsp;&nbsp;&nbsp;&nbsp;S Cavell (0.046%)\
132\.&nbsp;&nbsp;&nbsp;&nbsp;H Jonas (0.046%)\
137\.&nbsp;&nbsp;&nbsp;&nbsp;G Evans (0.045%)\
137\.&nbsp;&nbsp;&nbsp;&nbsp;S Blackburn (0.045%)\
137\.&nbsp;&nbsp;&nbsp;&nbsp;J Searle (0.045%)\
137\.&nbsp;&nbsp;&nbsp;&nbsp;S Zizek (0.045%)\
137\.&nbsp;&nbsp;&nbsp;&nbsp;A Smith (0.045%)\
137\.&nbsp;&nbsp;&nbsp;&nbsp;J Bennett (0.045%)\
137\.&nbsp;&nbsp;&nbsp;&nbsp;D Walton (0.045%)\
137\.&nbsp;&nbsp;&nbsp;&nbsp;J Barnes (0.045%)\
137\.&nbsp;&nbsp;&nbsp;&nbsp;L Strauss (0.045%)\
146\.&nbsp;&nbsp;&nbsp;&nbsp;W Alston (0.044%)\
146\.&nbsp;&nbsp;&nbsp;&nbsp;G Ryle (0.044%)\
148\.&nbsp;&nbsp;&nbsp;&nbsp;C Hempel (0.043%)\
148\.&nbsp;&nbsp;&nbsp;&nbsp;S Shoemaker (0.043%)\
150\.&nbsp;&nbsp;&nbsp;&nbsp;A Einstein (0.042%)\
150\.&nbsp;&nbsp;&nbsp;&nbsp;C Peacocke (0.042%)\
150\.&nbsp;&nbsp;&nbsp;&nbsp;JL Austin (0.042%)\
150\.&nbsp;&nbsp;&nbsp;&nbsp;A Danto (0.042%)\
154\.&nbsp;&nbsp;&nbsp;&nbsp;K Jaspers (0.041%)\
154\.&nbsp;&nbsp;&nbsp;&nbsp;J Schaffer (0.041%)\
154\.&nbsp;&nbsp;&nbsp;&nbsp;K Apel (0.041%)\
154\.&nbsp;&nbsp;&nbsp;&nbsp;A Kenny (0.041%)\
158\.&nbsp;&nbsp;&nbsp;&nbsp;H Grice (0.04%)\
158\.&nbsp;&nbsp;&nbsp;&nbsp;E Gilson (0.04%)\
158\.&nbsp;&nbsp;&nbsp;&nbsp;G Lukacs (0.04%)\
158\.&nbsp;&nbsp;&nbsp;&nbsp;Z Bauman (0.04%)\
158\.&nbsp;&nbsp;&nbsp;&nbsp;H Dreyfus (0.04%)\
163\.&nbsp;&nbsp;&nbsp;&nbsp;J Annas (0.039%)\
163\.&nbsp;&nbsp;&nbsp;&nbsp;R Swinburne (0.039%)\
163\.&nbsp;&nbsp;&nbsp;&nbsp;R Audi (0.039%)\
163\.&nbsp;&nbsp;&nbsp;&nbsp;C Wilson (0.039%)\
167\.&nbsp;&nbsp;&nbsp;&nbsp;A Mele (0.038%)\
167\.&nbsp;&nbsp;&nbsp;&nbsp;D Miller (0.038%)\
167\.&nbsp;&nbsp;&nbsp;&nbsp;M Horkheimer (0.038%)\
167\.&nbsp;&nbsp;&nbsp;&nbsp;L Althusser (0.038%)\
171\.&nbsp;&nbsp;&nbsp;&nbsp;M Devitt (0.037%)\
171\.&nbsp;&nbsp;&nbsp;&nbsp;J Patocka (0.037%)\
171\.&nbsp;&nbsp;&nbsp;&nbsp;EJ Lowe (0.037%)\
174\.&nbsp;&nbsp;&nbsp;&nbsp;JM Fischer (0.036%)\
174\.&nbsp;&nbsp;&nbsp;&nbsp;E Dussel (0.036%)\
174\.&nbsp;&nbsp;&nbsp;&nbsp;N Luhmann (0.036%)\
174\.&nbsp;&nbsp;&nbsp;&nbsp;RM Hare (0.036%)\
178\.&nbsp;&nbsp;&nbsp;&nbsp;M Smith (0.035%)\
178\.&nbsp;&nbsp;&nbsp;&nbsp;M Bratman (0.035%)\
178\.&nbsp;&nbsp;&nbsp;&nbsp;P Hadot (0.035%)\
178\.&nbsp;&nbsp;&nbsp;&nbsp;D Wiggins (0.035%)\
178\.&nbsp;&nbsp;&nbsp;&nbsp;T Irwin (0.035%)\
178\.&nbsp;&nbsp;&nbsp;&nbsp;T Sider (0.035%)\
178\.&nbsp;&nbsp;&nbsp;&nbsp;P Churchland (0.035%)\
178\.&nbsp;&nbsp;&nbsp;&nbsp;W Lycan (0.035%)\
186\.&nbsp;&nbsp;&nbsp;&nbsp;R Adams (0.034%)\
186\.&nbsp;&nbsp;&nbsp;&nbsp;J Dancy (0.034%)\
186\.&nbsp;&nbsp;&nbsp;&nbsp;Q Skinner (0.034%)\
186\.&nbsp;&nbsp;&nbsp;&nbsp;G Bachelard (0.034%)\
190\.&nbsp;&nbsp;&nbsp;&nbsp;T Horgan (0.033%)\
190\.&nbsp;&nbsp;&nbsp;&nbsp;A Steinbock (0.033%)\
190\.&nbsp;&nbsp;&nbsp;&nbsp;P Foot (0.033%)\
190\.&nbsp;&nbsp;&nbsp;&nbsp;P Feyerabend (0.033%)\
190\.&nbsp;&nbsp;&nbsp;&nbsp;EO Wilson (0.033%)\
190\.&nbsp;&nbsp;&nbsp;&nbsp;J Perry (0.033%)\
190\.&nbsp;&nbsp;&nbsp;&nbsp;A Gibbard (0.033%)\
190\.&nbsp;&nbsp;&nbsp;&nbsp;S Shapiro (0.033%)\
190\.&nbsp;&nbsp;&nbsp;&nbsp;J Broome (0.033%)\
190\.&nbsp;&nbsp;&nbsp;&nbsp;JJ Thomson (0.033%)\
190\.&nbsp;&nbsp;&nbsp;&nbsp;M Burnyeat (0.033%)\
190\.&nbsp;&nbsp;&nbsp;&nbsp;HLA Hart (0.033%)\
202\.&nbsp;&nbsp;&nbsp;&nbsp;N Malcolm (0.032%)\
202\.&nbsp;&nbsp;&nbsp;&nbsp;F Varela (0.032%)\
202\.&nbsp;&nbsp;&nbsp;&nbsp;W Salmon (0.032%)\
202\.&nbsp;&nbsp;&nbsp;&nbsp;J Feinberg (0.032%)\
202\.&nbsp;&nbsp;&nbsp;&nbsp;N Carroll (0.032%)\
202\.&nbsp;&nbsp;&nbsp;&nbsp;R Abulad (0.032%)\
202\.&nbsp;&nbsp;&nbsp;&nbsp;M Walzer (0.032%)\
202\.&nbsp;&nbsp;&nbsp;&nbsp;K Walton (0.032%)\
210\.&nbsp;&nbsp;&nbsp;&nbsp;F Brentano (0.031%)\
210\.&nbsp;&nbsp;&nbsp;&nbsp;A Tarski (0.031%)\
210\.&nbsp;&nbsp;&nbsp;&nbsp;S Darwall (0.031%)\
210\.&nbsp;&nbsp;&nbsp;&nbsp;F Engels (0.031%)\
210\.&nbsp;&nbsp;&nbsp;&nbsp;V Lenin (0.031%)\
210\.&nbsp;&nbsp;&nbsp;&nbsp;G Strawson (0.031%)\
210\.&nbsp;&nbsp;&nbsp;&nbsp;CS Lewis (0.031%)\
210\.&nbsp;&nbsp;&nbsp;&nbsp;J Waldron (0.031%)\
218\.&nbsp;&nbsp;&nbsp;&nbsp;C Darwin (0.03%)\
218\.&nbsp;&nbsp;&nbsp;&nbsp;G Vattimo (0.03%)\
218\.&nbsp;&nbsp;&nbsp;&nbsp;E Sober (0.03%)\
218\.&nbsp;&nbsp;&nbsp;&nbsp;M Fricker (0.03%)\
218\.&nbsp;&nbsp;&nbsp;&nbsp;M Tye (0.03%)\
218\.&nbsp;&nbsp;&nbsp;&nbsp;L Laudan (0.03%)\
218\.&nbsp;&nbsp;&nbsp;&nbsp;R Brandt (0.03%)\
218\.&nbsp;&nbsp;&nbsp;&nbsp;H Blumenberg (0.03%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;J Hawthorne (0.029%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;D Henrich (0.029%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;A Ayer (0.029%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;C Kahn (0.029%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;C Mills (0.029%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;D Haraway (0.029%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;G Vlastos (0.029%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;G Cohen (0.029%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;O Oneill (0.029%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;J Stanley (0.029%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;C Fabro (0.029%)\
226\.&nbsp;&nbsp;&nbsp;&nbsp;U Eco (0.029%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;F Van Eemeren (0.028%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;R Barthes (0.028%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;T Parsons (0.028%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;N Salmon (0.028%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;N Fraser (0.028%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;T Reid (0.028%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;I Newton (0.028%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;I Lakatos (0.028%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;I Young (0.028%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;P Sloterdijk (0.028%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;F Recanati (0.028%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;R Sorabji (0.028%)\
238\.&nbsp;&nbsp;&nbsp;&nbsp;K Bach (0.028%)\
251\.&nbsp;&nbsp;&nbsp;&nbsp;I Berlin (0.027%)\
251\.&nbsp;&nbsp;&nbsp;&nbsp;R Feldman (0.027%)\
251\.&nbsp;&nbsp;&nbsp;&nbsp;B Stroud (0.027%)\
251\.&nbsp;&nbsp;&nbsp;&nbsp;L Floridi (0.027%)\
251\.&nbsp;&nbsp;&nbsp;&nbsp;G Berkeley (0.027%)\
251\.&nbsp;&nbsp;&nbsp;&nbsp;E Fink (0.027%)\
251\.&nbsp;&nbsp;&nbsp;&nbsp;J Baudrillard (0.027%)\
251\.&nbsp;&nbsp;&nbsp;&nbsp;D Hilbert (0.027%)\
251\.&nbsp;&nbsp;&nbsp;&nbsp;R Bhaskar (0.027%)\
251\.&nbsp;&nbsp;&nbsp;&nbsp;C Wolff (0.027%)\
251\.&nbsp;&nbsp;&nbsp;&nbsp;A Thomasson (0.027%)\
251\.&nbsp;&nbsp;&nbsp;&nbsp;D Kahneman (0.027%)\
251\.&nbsp;&nbsp;&nbsp;&nbsp;P Boghossian (0.027%)\
264\.&nbsp;&nbsp;&nbsp;&nbsp;S Yablo (0.026%)\
264\.&nbsp;&nbsp;&nbsp;&nbsp;A Baier (0.026%)\
264\.&nbsp;&nbsp;&nbsp;&nbsp;J Dunn (0.026%)\
264\.&nbsp;&nbsp;&nbsp;&nbsp;K Godel (0.026%)\
264\.&nbsp;&nbsp;&nbsp;&nbsp;A Koyre (0.026%)\
264\.&nbsp;&nbsp;&nbsp;&nbsp;M Gilbert (0.026%)\
264\.&nbsp;&nbsp;&nbsp;&nbsp;J Prinz (0.026%)\
264\.&nbsp;&nbsp;&nbsp;&nbsp;R Shusterman (0.026%)\
264\.&nbsp;&nbsp;&nbsp;&nbsp;W Kaufmann (0.026%)\
264\.&nbsp;&nbsp;&nbsp;&nbsp;J Cohen (0.026%)\
264\.&nbsp;&nbsp;&nbsp;&nbsp;R Bernstein (0.026%)\
264\.&nbsp;&nbsp;&nbsp;&nbsp;J Levinson (0.026%)\
276\.&nbsp;&nbsp;&nbsp;&nbsp;J Caputo (0.025%)\
276\.&nbsp;&nbsp;&nbsp;&nbsp;J Greco (0.025%)\
276\.&nbsp;&nbsp;&nbsp;&nbsp;R Wollheim (0.025%)\
276\.&nbsp;&nbsp;&nbsp;&nbsp;J Elster (0.025%)\
276\.&nbsp;&nbsp;&nbsp;&nbsp;E Thompson (0.025%)\
276\.&nbsp;&nbsp;&nbsp;&nbsp;RG Millikan (0.025%)\
276\.&nbsp;&nbsp;&nbsp;&nbsp;S Haack (0.025%)\
276\.&nbsp;&nbsp;&nbsp;&nbsp;G Marcel (0.025%)\
276\.&nbsp;&nbsp;&nbsp;&nbsp;S De Beauvoir (0.025%)\
276\.&nbsp;&nbsp;&nbsp;&nbsp;R Collingwood (0.025%)\
276\.&nbsp;&nbsp;&nbsp;&nbsp;A Camus (0.025%)\
276\.&nbsp;&nbsp;&nbsp;&nbsp;N Smith (0.025%)\
276\.&nbsp;&nbsp;&nbsp;&nbsp;R Boyd (0.025%)\
289\.&nbsp;&nbsp;&nbsp;&nbsp;VM Guzman (0.024%)\
289\.&nbsp;&nbsp;&nbsp;&nbsp;M Heller (0.024%)\
289\.&nbsp;&nbsp;&nbsp;&nbsp;M Slote (0.024%)\
289\.&nbsp;&nbsp;&nbsp;&nbsp;W Kymlicka (0.024%)\
289\.&nbsp;&nbsp;&nbsp;&nbsp;E Stump (0.024%)\
289\.&nbsp;&nbsp;&nbsp;&nbsp;L Zagzebski (0.024%)\
289\.&nbsp;&nbsp;&nbsp;&nbsp;GJ Ortega (0.024%)\
289\.&nbsp;&nbsp;&nbsp;&nbsp;B Smith (0.024%)\
289\.&nbsp;&nbsp;&nbsp;&nbsp;C Perelman (0.024%)\
289\.&nbsp;&nbsp;&nbsp;&nbsp;P Carruthers (0.024%)\
289\.&nbsp;&nbsp;&nbsp;&nbsp;H Price (0.024%)\
289\.&nbsp;&nbsp;&nbsp;&nbsp;R Scruton (0.024%)\
289\.&nbsp;&nbsp;&nbsp;&nbsp;D Gauthier (0.024%)\
289\.&nbsp;&nbsp;&nbsp;&nbsp;M Schroeder (0.024%)\
289\.&nbsp;&nbsp;&nbsp;&nbsp;P Railton (0.024%)\
289\.&nbsp;&nbsp;&nbsp;&nbsp;G Lakoff (0.024%)\
289\.&nbsp;&nbsp;&nbsp;&nbsp;G Rosen (0.024%)\
289\.&nbsp;&nbsp;&nbsp;&nbsp;AN Prior (0.024%)\
289\.&nbsp;&nbsp;&nbsp;&nbsp;F Fanon (0.024%)\
289\.&nbsp;&nbsp;&nbsp;&nbsp;G Simmel (0.024%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;S Soames (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;H Maturana (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;R Pippin (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;F Bacon (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;G Von Wright (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;A Damasio (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;A Buchanan (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;M Zambrano (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;H Castaneda (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;S Scheffler (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;P Unger (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;R Hursthouse (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;M Buber (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;D Papineau (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;J Maritain (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;J Earman (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;K Lehrer (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;M Johnston (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;S Wolf (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;Cicero (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;L Irigaray (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;S Schiffer (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;D Christensen (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;F Ramsey (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;P Horwich (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;M Garcia Carpintero (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;C Broad (0.023%)\
309\.&nbsp;&nbsp;&nbsp;&nbsp;S Gould (0.023%)\
337\.&nbsp;&nbsp;&nbsp;&nbsp;H Sidgwick (0.022%)\
337\.&nbsp;&nbsp;&nbsp;&nbsp;R Arneson (0.022%)\
337\.&nbsp;&nbsp;&nbsp;&nbsp;M Tomasello (0.022%)\
337\.&nbsp;&nbsp;&nbsp;&nbsp;B Waldenfels (0.022%)\
337\.&nbsp;&nbsp;&nbsp;&nbsp;J Stewart (0.022%)\
337\.&nbsp;&nbsp;&nbsp;&nbsp;G Boolos (0.022%)\
337\.&nbsp;&nbsp;&nbsp;&nbsp;G Currie (0.022%)\
337\.&nbsp;&nbsp;&nbsp;&nbsp;M Blanchot (0.022%)\
337\.&nbsp;&nbsp;&nbsp;&nbsp;J Lackey (0.022%)\
337\.&nbsp;&nbsp;&nbsp;&nbsp;T Pogge (0.022%)\
337\.&nbsp;&nbsp;&nbsp;&nbsp;B Stiegler (0.022%)\
337\.&nbsp;&nbsp;&nbsp;&nbsp;N Bostrom (0.022%)\
337\.&nbsp;&nbsp;&nbsp;&nbsp;J Royce (0.022%)\
337\.&nbsp;&nbsp;&nbsp;&nbsp;S Kagan (0.022%)\
337\.&nbsp;&nbsp;&nbsp;&nbsp;R Koselleck (0.022%)\
337\.&nbsp;&nbsp;&nbsp;&nbsp;JJ Smart (0.022%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;B Croce (0.021%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;JC Beall (0.021%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;G Canguilhem (0.021%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;S Benhabib (0.021%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;P Hacker (0.021%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;A Giddens (0.021%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;N Wolterstorff (0.021%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;G Wright (0.021%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;S Stich (0.021%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;E Durkheim (0.021%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;J Bentham (0.021%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;W Dilthey (0.021%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;M Polanyi (0.021%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;J Gibson (0.021%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;J Brown (0.021%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;D Diderot (0.021%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;J Woodward (0.021%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;M Frede (0.021%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;M Huemer (0.021%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;B Leiter (0.021%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;B Pascal (0.021%)\
353\.&nbsp;&nbsp;&nbsp;&nbsp;T Crane (0.021%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;J Margolis (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;R Solomon (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;M Williams (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;R Ingarden (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;J Miller (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;A Long (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;A Schutz (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;N Belnap (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;C Mc Ginn (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;D Pereboom (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;J Harris (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;G Watson (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;G Graham (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;A Byrne (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;A Noe (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;D Sedley (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;J Cottingham (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;J Greene (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;K Donnellan (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;S Haslanger (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;M Lipman (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;M Sandel (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;E Mayr (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;R Penrose (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;S Toulmin (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;C Castoriadis (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;J Haidt (0.02%)\
375\.&nbsp;&nbsp;&nbsp;&nbsp;N Daniels (0.02%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;M Clark (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;LW Beck (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;P Tillich (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;A Bird (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;R Goodin (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;S Davies (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;JM Cooper (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;C Mouffe (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;G Lloyd (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;JW Goethe (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;N Cartwright (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;P Maddy (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;J Kvanvig (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;M Black (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;JD Velleman (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;H Reichenbach (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;S Cohen (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;F Guattari (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;E Laclau (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;D Enoch (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;R Routley (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;O Bazaluk (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;M Zimmerman (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;I Murdoch (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;B Skyrms (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;S Feferman (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;T Metz (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;E Balibar (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;K Rahner (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;D Hull (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;M Archer (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;K Lowith (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;R Bernasconi (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;S Weil (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;T Griffero (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;R Esposito (0.019%)\
403\.&nbsp;&nbsp;&nbsp;&nbsp;E Tugendhat (0.019%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;J Barwise (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;H Diels (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;R Giere (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;A Church (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;W Bechtel (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;J Ladyman (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;E Bloch (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;D Garrett (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;J Hick (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;H Kelsen (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;R Tuomela (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;B Lonergan (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;L Baker (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;Avicenna (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;E Stein (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;H Weyl (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;J Mc Mahan (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;M Thompson (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;D Bell (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;W Jaeger (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;J Van Cleve (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;JL Pollock (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;A Nehamas (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;W Brown (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;SO Hansson (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;D Copp (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;D Mellor (0.018%)\
440\.&nbsp;&nbsp;&nbsp;&nbsp;G Sher (0.018%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;E Schwitzgebel (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;R Kane (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;U Kriegel (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;R Sokolowski (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;P Simons (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;D Ihde (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;O Hoffe (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;E Zalta (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;R Langton (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;H Kornblith (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;J Burgess (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;W Heisenberg (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;A Gramsci (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;N Bobbio (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;F Feldman (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;T Hurka (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;E Schrodinger (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;GH Mead (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;C Levi Strauss (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;F Jameson (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;R Popkin (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;C Parsons (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;T Beauchamp (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;R Fogelin (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;W Chan (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;M Tooley (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;T Fuchs (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;D Brink (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;K Ameriks (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;S French (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;L Bon Jour (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;J Van Benthem (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;P Duhem (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;J Finnis (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;R Hanna (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;DW Smith (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;E Said (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;R Williams (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;F Beiser (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;R Martin (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;W Craig (0.017%)\
468\.&nbsp;&nbsp;&nbsp;&nbsp;R Kraut (0.017%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;H Plessner (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;E Berti (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;R Crisp (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;R Roberts (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;R Sorensen (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;S Shapin (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;D Harvey (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;WKC Guthrie (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;H White (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;C Diamond (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;M Gueroult (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;AC Graham (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;F Schleiermacher (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;J Pocock (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;D Scott (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;W Beierwaltes (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;C Hartshorne (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;M Bunge (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;C Sunstein (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;S Pinker (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;B Herman (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;N Levy (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;P Freire (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;H Poincare (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;M Schlick (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;R Bernet (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;P Suppes (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;Y Saito (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;F Suarez (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;C List (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;M Ruse (0.016%)\
510\.&nbsp;&nbsp;&nbsp;&nbsp;K Wiredu (0.016%)

Here are a few observations: First, while I am of course aware that Aristotle and Plato are ...like, important, I still find it pretty incredible that they come in first and third after having been dead for more than 2000 years. Second, there is a sharp drop-off after the first four authors (Aristotle, Kant, Plato, Heidegger): Their cumulative score is roughly equal to the cumulative score of the next fourteen authors (Wittgenstein to Habermas). Big Four? Third, a number of people in Schwitzgebel's comments asked questions/expressed dismay about the low ranks of various (European) authors. On the current list, these authors tend to rank much higher: Derrida (ranked #9), Foucault (#21), Merleau-Ponty (#23), Gadamer (#50), Adorno (#65) and Cavell (#90), for example, are all in the top 100.

Schwitzgebel makes it clear, of course, that his ranking only captures current influence in 'mainstream Anglophone philosophy,' and so the fact that Derrida, Foucault et al. are not particularly high up on his list is not surprising. The question, then, is: What does the current ranking capture? The answer I think depends a lot on whether the journals in my dataset capture published academic philosophy. he current ranking captures  is not unreasonable to claim that the current ranking is able to capture influence across philosophy more broadly. I will probably make a shiny app that allows people to select which journals they want included an the like, so that people who disagree can puruse the dataset at their own leasure.

Since this data is longitudinal (1975-2024), I also looked at . I made the graph interactive because it is a mess otherwise.
