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

One possible way to get around this problem would be to only keep references with at least one full first name. However, this strategy has at least two major problems. First, the strategy filters out references to works by authors without a first name (e.g., Aristotle, Plato, Plutarch, Averroes) or authors who usually get referred to only by last name. Of course, it is possible to simply keep these references in the dataset. This introduces a different problem, though. Consider Aristotle. Aristotle virtually always get referenced as 'Aristotle.' This means that the new filtered dataset would include (almost) all references to Aristotle's works. Compare that to an author like David Lewis, who usually gets referenced either as 'D. Lewis' or 'David Lewis.' The filtered dataset would only contain instances of the second case, but not instances of the first case. As a result, Aristotle's citation count would be inflated (likely dramatically inflated) compared to David Lewis' citation count.

The second problem is that only keeping references with full author names results in inaccurate citation counts if the ratio of citations with full first names to citations with just initial is different for different authors. Suppose that when people reference David Lewis, 20% of the time, they do so as 'David Lewis', while the remaining 80% of the time, as 'D. Lewis' (or 'D.K. Lewis'). In that case, the new filtered dataset would include only 20% of all Lewis-references present in the original dataset. If this ratio is the same (or at least similar) for other authors, then everything is fine. However, suppose that Immanuel Kant gets referenced as 'Immanuel Kant' 50% of the time. If so, then the new filtered dataset would lead me to substantially underestimate Lewis' citation count compared to Kant's citation count. Unfortunately, what I have just described is what the data in fact look like: 66% of references to the last name Lewis are to 'D. Lewis' or 'D.K. Lewis', while only 14% are to 'David Lewis;' in contrast, 46% of references to the last name Kant are to 'Immanuel Kant,' another 46% are to 'I. Kant.'

Filtering out authors for whom the dataset only contains initials, then, is not an option. Instead, I chose to stick with initials, converting full first names into initials. This means that I get to keep a much larger proportion of the original data. It also means that my results need to be taken with a grain of salt: many first initial-last name combinations are going to be shared by lots of authors. However, there is reason to believe that the issue is not massive. [...]

[Data cleaning]

Some of the journals the WoS lists under Philosophy strike me as questionable. For instance: Are the _Nursing History Review_, the _Journal of Medical Biography_, the _Journal for the History of Astronomy_ or _Engineering Studies_ really philosophy journals? I think not. As a result, I decided to remove all journals from the dataset that are not also indexed on PhilPapers. This method isn't perfect, of course, but I think it is good enough.

After these (and some other, more boring exclusions having to do with missing data), I was  left with a final dataset containing ~1.6 million references from articles published in 269 journals between 1975 and 2024.

There are different ways to quantify _most cited author_. One is to just count up citations. I don't think that is a particularly helpful approach, however, because (a) philosophers today cite a lot more stuff than did philosophers 50 years ago and (b) many more philosophy articles get published today than did 50 years ago. This means that raw citation counts as a measure of influence are biased (heavily) in favor of recent citations.

I instead chose to go with proportions. Note that, by itself, this doesn't solve (a) and (b). To illustrate [I'll focus on (a), but the problem with (b) is analogous]: Suppose we are looking at two years, 1990 and 2020, for one journal A. In 1990, A published 10 articles, while in 2020, it published 100 articles. Suppose further that articles in 1990 and 2020 cite about the same number of references (say, 10). If an author was very influential in the pages of A in 1990 (say, 10% of all citations were to this author's work) but no longer that influential in 2020 (say, 1%), then we get an overall proportion of citations to this author in A of ~2%. If the roles of 1990 and 2020 had been reversed, however, then this overall proportion would have been ~9%. Yet it looks like this differences is just an artifact of the fact that A published fewer articles in 1990 than in 2020.

To avoid (a) and (b), I divided my data into time bins (I chose five years), calculated the proportion of citations received by a given author in each bin separately, and only then calculated the mean across all of these bins. I also did the same thing for journals; otherwise, the results would be biased towards influence in journals that publish more articles and/or have higher average citation rates.

Here are the top 510 (brackets show mean percentages):

1\.\t M Heidegger (0.676%)\
2\. I Kant (0.615%)\
3\. E Husserl (0.445%)\
4\. J Derrida (0.381%)\
5\. M Foucault (0.363%)\
6\. Aristotle (0.358%)\
7\. GWF Hegel (0.309%)\
8\. L Wittgenstein (0.281%)\
9\. G Deleuze (0.271%)\
10\. D Lewis (0.263%)\
11\. F Nietzsche (0.259%)\
12\. J Habermas (0.242%)\
13\. Plato (0.216%)\
14\. D Hume (0.21%)\
14\. W Quine (0.21%)\
16\. J Rawls (0.205%)\
17\. K Marx (0.202%)\
18\. M Merleau Ponty (0.186%)\
19\. JP Sartre (0.181%)\
20\. J Dewey (0.177%)\
21\. D Davidson (0.176%)\
22\. B Russell (0.169%)\
23\. P Ricoeur (0.168%)\
24\. H Putnam (0.166%)\
25\. E Levinas (0.161%)\
26\. R Rorty (0.159%)\
27\. H Arendt (0.156%)\
28\. R Descartes (0.153%)\
29\. G Frege (0.151%)\
30\. HG Gadamer (0.15%)\
31\. T Aquinas (0.148%)\
32\. GW Leibniz (0.134%)\
33\. T Adorno (0.123%)\
34\. S Kripke (0.117%)\
35\. M Nussbaum (0.114%)\
36\. J Piaget (0.113%)\
36\. S Freud (0.113%)\
38\. T Hobbes (0.112%)\
39\. W James (0.11%)\
40\. B Williams (0.106%)\
41\. J Mc Dowell (0.104%)\
42\. K Popper (0.101%)\
43\. W Benjamin (0.1%)\
44\. C Peirce (0.098%)\
45\. J Locke (0.097%)\
45\. A Goldman (0.097%)\
47\. C Taylor (0.096%)\
48\. T Williamson (0.094%)\
49\. M Dummett (0.092%)\
49\. J Fodor (0.092%)\
51\. G Harman (0.091%)\
51\. S Kierkegaard (0.091%)\
53\. T Nagel (0.088%)\
54\. R Carnap (0.085%)\
55\. JS Mill (0.084%)\
56\. P Strawson (0.081%)\
56\. G Agamben (0.081%)\
58\. JR Searle (0.08%)\
58\. D Dennett (0.08%)\
60\. T Kuhn (0.079%)\
61\. D Chalmers (0.078%)\
62\. E Cassirer (0.074%)\
62\. C Wright (0.074%)\
64\. K Fine (0.073%)\
64\. D Armstrong (0.073%)\
66\. A Mac Intyre (0.071%)\
66\. J Ranciere (0.071%)\
68\. J Lacan (0.07%)\
69\. J Kim (0.069%)\
70\. A Plantinga (0.068%)\
70\. T Burge (0.068%)\
72\. A Badiou (0.067%)\
72\. JJ Rousseau (0.067%)\
74\. J Butler (0.066%)\
75\. C Korsgaard (0.065%)\
75\. R Brandom (0.065%)\
75\. W Sellars (0.065%)\
78\. G Priest (0.063%)\
78\. A Honneth (0.063%)\
78\. C Schmitt (0.063%)\
81\. N Goodman (0.062%)\
81\. F Dretske (0.062%)\
81\. I Hacking (0.062%)\
81\. B Van Fraassen (0.062%)\
85\. H Frankfurt (0.061%)\
85\. P Bourdieu (0.061%)\
85\. R Stalnaker (0.061%)\
88\. M Weber (0.06%)\
88\. F Jackson (0.06%)\
90\. P Van Inwagen (0.059%)\
91\. E Sosa (0.058%)\
91\. H Bergson (0.058%)\
91\. R Dworkin (0.058%)\
91\. N Chomsky (0.058%)\
91\. R Chisholm (0.058%)\
96\. G Anscombe (0.057%)\
96\. J Hintikka (0.057%)\
98\. P Singer (0.056%)\
98\. D Pritchard (0.056%)\
98\. D Parfit (0.056%)\
98\. A Wood (0.056%)\
98\. A Sen (0.056%)\
103\. B Latour (0.055%)\
103\. J Mackie (0.055%)\
103\. P Kitcher (0.055%)\
103\. S Gallagher (0.055%)\
107\. P Guyer (0.054%)\
107\. F Schelling (0.054%)\
107\. GE Moore (0.054%)\
107\. H Marcuse (0.054%)\
107\. R Nozick (0.054%)\
112\. D Zahavi (0.052%)\
112\. N Rescher (0.052%)\
112\. JL Nancy (0.052%)\
115\. Augustine (0.051%)\
115\. P Pettit (0.051%)\
115\. B Spinoza (0.051%)\
118\. JL Marion (0.05%)\
118\. T Scanlon (0.05%)\
118\. J Fichte (0.05%)\
121\. M Henry (0.049%)\
121\. H Field (0.049%)\
121\. A Whitehead (0.049%)\
121\. M Friedman (0.049%)\
121\. J Lyotard (0.049%)\
126\. P Geach (0.048%)\
126\. A Clark (0.048%)\
126\. A Schopenhauer (0.048%)\
126\. J Raz (0.048%)\
130\. W Ross (0.047%)\
130\. N Block (0.047%)\
132\. H Allison (0.046%)\
132\. M Scheler (0.046%)\
132\. D Kaplan (0.046%)\
132\. S Cavell (0.046%)\
132\. H Jonas (0.046%)\
137\. G Evans (0.045%)\
137\. S Blackburn (0.045%)\
137\. J Searle (0.045%)\
137\. S Zizek (0.045%)\
137\. A Smith (0.045%)\
137\. J Bennett (0.045%)\
137\. D Walton (0.045%)\
137\. J Barnes (0.045%)\
137\. L Strauss (0.045%)\
146\. W Alston (0.044%)\
146\. G Ryle (0.044%)\
148\. C Hempel (0.043%)\
148\. S Shoemaker (0.043%)\
150\. A Einstein (0.042%)\
150\. C Peacocke (0.042%)\
150\. JL Austin (0.042%)\
150\. A Danto (0.042%)\
154\. K Jaspers (0.041%)\
154\. J Schaffer (0.041%)\
154\. K Apel (0.041%)\
154\. A Kenny (0.041%)\
158\. H Grice (0.04%)\
158\. E Gilson (0.04%)\
158\. G Lukacs (0.04%)\
158\. Z Bauman (0.04%)\
158\. H Dreyfus (0.04%)\
163\. J Annas (0.039%)\
163\. R Swinburne (0.039%)\
163\. R Audi (0.039%)\
163\. C Wilson (0.039%)\
167\. A Mele (0.038%)\
167\. D Miller (0.038%)\
167\. M Horkheimer (0.038%)\
167\. L Althusser (0.038%)\
171\. M Devitt (0.037%)\
171\. J Patocka (0.037%)\
171\. EJ Lowe (0.037%)\
174\. JM Fischer (0.036%)\
174\. E Dussel (0.036%)\
174\. N Luhmann (0.036%)\
174\. RM Hare (0.036%)\
178\. M Smith (0.035%)\
178\. M Bratman (0.035%)\
178\. P Hadot (0.035%)\
178\. D Wiggins (0.035%)\
178\. T Irwin (0.035%)\
178\. T Sider (0.035%)\
178\. P Churchland (0.035%)\
178\. W Lycan (0.035%)\
186\. R Adams (0.034%)\
186\. J Dancy (0.034%)\
186\. Q Skinner (0.034%)\
186\. G Bachelard (0.034%)\
190\. T Horgan (0.033%)\
190\. A Steinbock (0.033%)\
190\. P Foot (0.033%)\
190\. P Feyerabend (0.033%)\
190\. EO Wilson (0.033%)\
190\. J Perry (0.033%)\
190\. A Gibbard (0.033%)\
190\. S Shapiro (0.033%)\
190\. J Broome (0.033%)\
190\. JJ Thomson (0.033%)\
190\. M Burnyeat (0.033%)\
190\. HLA Hart (0.033%)\
202\. N Malcolm (0.032%)\
202\. F Varela (0.032%)\
202\. W Salmon (0.032%)\
202\. J Feinberg (0.032%)\
202\. N Carroll (0.032%)\
202\. R Abulad (0.032%)\
202\. M Walzer (0.032%)\
202\. K Walton (0.032%)\
210\. F Brentano (0.031%)\
210\. A Tarski (0.031%)\
210\. S Darwall (0.031%)\
210\. F Engels (0.031%)\
210\. V Lenin (0.031%)\
210\. G Strawson (0.031%)\
210\. CS Lewis (0.031%)\
210\. J Waldron (0.031%)\
218\. C Darwin (0.03%)\
218\. G Vattimo (0.03%)\
218\. E Sober (0.03%)\
218\. M Fricker (0.03%)\
218\. M Tye (0.03%)\
218\. L Laudan (0.03%)\
218\. R Brandt (0.03%)\
218\. H Blumenberg (0.03%)\
226\. J Hawthorne (0.029%)\
226\. D Henrich (0.029%)\
226\. A Ayer (0.029%)\
226\. C Kahn (0.029%)\
226\. C Mills (0.029%)\
226\. D Haraway (0.029%)\
226\. G Vlastos (0.029%)\
226\. G Cohen (0.029%)\
226\. O Oneill (0.029%)\
226\. J Stanley (0.029%)\
226\. C Fabro (0.029%)\
226\. U Eco (0.029%)\
238\. F Van Eemeren (0.028%)\
238\. R Barthes (0.028%)\
238\. T Parsons (0.028%)\
238\. N Salmon (0.028%)\
238\. N Fraser (0.028%)\
238\. T Reid (0.028%)\
238\. I Newton (0.028%)\
238\. I Lakatos (0.028%)\
238\. I Young (0.028%)\
238\. P Sloterdijk (0.028%)\
238\. F Recanati (0.028%)\
238\. R Sorabji (0.028%)\
238\. K Bach (0.028%)\
251\. I Berlin (0.027%)\
251\. R Feldman (0.027%)\
251\. B Stroud (0.027%)\
251\. L Floridi (0.027%)\
251\. G Berkeley (0.027%)\
251\. E Fink (0.027%)\
251\. J Baudrillard (0.027%)\
251\. D Hilbert (0.027%)\
251\. R Bhaskar (0.027%)\
251\. C Wolff (0.027%)\
251\. A Thomasson (0.027%)\
251\. D Kahneman (0.027%)\
251\. P Boghossian (0.027%)\
264\. S Yablo (0.026%)\
264\. A Baier (0.026%)\
264\. J Dunn (0.026%)\
264\. K Godel (0.026%)\
264\. A Koyre (0.026%)\
264\. M Gilbert (0.026%)\
264\. J Prinz (0.026%)\
264\. R Shusterman (0.026%)\
264\. W Kaufmann (0.026%)\
264\. J Cohen (0.026%)\
264\. R Bernstein (0.026%)\
264\. J Levinson (0.026%)\
276\. J Caputo (0.025%)\
276\. J Greco (0.025%)\
276\. R Wollheim (0.025%)\
276\. J Elster (0.025%)\
276\. E Thompson (0.025%)\
276\. RG Millikan (0.025%)\
276\. S Haack (0.025%)\
276\. G Marcel (0.025%)\
276\. S De Beauvoir (0.025%)\
276\. R Collingwood (0.025%)\
276\. A Camus (0.025%)\
276\. N Smith (0.025%)\
276\. R Boyd (0.025%)\
289\. VM Guzman (0.024%)\
289\. M Heller (0.024%)\
289\. M Slote (0.024%)\
289\. W Kymlicka (0.024%)\
289\. E Stump (0.024%)\
289\. L Zagzebski (0.024%)\
289\. GJ Ortega (0.024%)\
289\. B Smith (0.024%)\
289\. C Perelman (0.024%)\
289\. P Carruthers (0.024%)\
289\. H Price (0.024%)\
289\. R Scruton (0.024%)\
289\. D Gauthier (0.024%)\
289\. M Schroeder (0.024%)\
289\. P Railton (0.024%)\
289\. G Lakoff (0.024%)\
289\. G Rosen (0.024%)\
289\. AN Prior (0.024%)\
289\. F Fanon (0.024%)\
289\. G Simmel (0.024%)\
309\. S Soames (0.023%)\
309\. H Maturana (0.023%)\
309\. R Pippin (0.023%)\
309\. F Bacon (0.023%)\
309\. G Von Wright (0.023%)\
309\. A Damasio (0.023%)\
309\. A Buchanan (0.023%)\
309\. M Zambrano (0.023%)\
309\. H Castaneda (0.023%)\
309\. S Scheffler (0.023%)\
309\. P Unger (0.023%)\
309\. R Hursthouse (0.023%)\
309\. M Buber (0.023%)\
309\. D Papineau (0.023%)\
309\. J Maritain (0.023%)\
309\. J Earman (0.023%)\
309\. K Lehrer (0.023%)\
309\. M Johnston (0.023%)\
309\. S Wolf (0.023%)\
309\. Cicero (0.023%)\
309\. L Irigaray (0.023%)\
309\. S Schiffer (0.023%)\
309\. D Christensen (0.023%)\
309\. F Ramsey (0.023%)\
309\. P Horwich (0.023%)\
309\. M Garcia Carpintero (0.023%)\
309\. C Broad (0.023%)\
309\. S Gould (0.023%)\
337\. H Sidgwick (0.022%)\
337\. R Arneson (0.022%)\
337\. M Tomasello (0.022%)\
337\. B Waldenfels (0.022%)\
337\. J Stewart (0.022%)\
337\. G Boolos (0.022%)\
337\. G Currie (0.022%)\
337\. M Blanchot (0.022%)\
337\. J Lackey (0.022%)\
337\. T Pogge (0.022%)\
337\. B Stiegler (0.022%)\
337\. N Bostrom (0.022%)\
337\. J Royce (0.022%)\
337\. S Kagan (0.022%)\
337\. R Koselleck (0.022%)\
337\. JJ Smart (0.022%)\
353\. B Croce (0.021%)\
353\. JC Beall (0.021%)\
353\. G Canguilhem (0.021%)\
353\. S Benhabib (0.021%)\
353\. P Hacker (0.021%)\
353\. A Giddens (0.021%)\
353\. N Wolterstorff (0.021%)\
353\. G Wright (0.021%)\
353\. S Stich (0.021%)\
353\. E Durkheim (0.021%)\
353\. J Bentham (0.021%)\
353\. W Dilthey (0.021%)\
353\. M Polanyi (0.021%)\
353\. J Gibson (0.021%)\
353\. J Brown (0.021%)\
353\. D Diderot (0.021%)\
353\. J Woodward (0.021%)\
353\. M Frede (0.021%)\
353\. M Huemer (0.021%)\
353\. B Leiter (0.021%)\
353\. B Pascal (0.021%)\
353\. T Crane (0.021%)\
375\. J Margolis (0.02%)\
375\. R Solomon (0.02%)\
375\. M Williams (0.02%)\
375\. R Ingarden (0.02%)\
375\. J Miller (0.02%)\
375\. A Long (0.02%)\
375\. A Schutz (0.02%)\
375\. N Belnap (0.02%)\
375\. C Mc Ginn (0.02%)\
375\. D Pereboom (0.02%)\
375\. J Harris (0.02%)\
375\. G Watson (0.02%)\
375\. G Graham (0.02%)\
375\. A Byrne (0.02%)\
375\. A Noe (0.02%)\
375\. D Sedley (0.02%)\
375\. J Cottingham (0.02%)\
375\. J Greene (0.02%)\
375\. K Donnellan (0.02%)\
375\. S Haslanger (0.02%)\
375\. M Lipman (0.02%)\
375\. M Sandel (0.02%)\
375\. E Mayr (0.02%)\
375\. R Penrose (0.02%)\
375\. S Toulmin (0.02%)\
375\. C Castoriadis (0.02%)\
375\. J Haidt (0.02%)\
375\. N Daniels (0.02%)\
403\. M Clark (0.019%)\
403\. LW Beck (0.019%)\
403\. P Tillich (0.019%)\
403\. A Bird (0.019%)\
403\. R Goodin (0.019%)\
403\. S Davies (0.019%)\
403\. JM Cooper (0.019%)\
403\. C Mouffe (0.019%)\
403\. G Lloyd (0.019%)\
403\. JW Goethe (0.019%)\
403\. N Cartwright (0.019%)\
403\. P Maddy (0.019%)\
403\. J Kvanvig (0.019%)\
403\. M Black (0.019%)\
403\. JD Velleman (0.019%)\
403\. H Reichenbach (0.019%)\
403\. S Cohen (0.019%)\
403\. F Guattari (0.019%)\
403\. E Laclau (0.019%)\
403\. D Enoch (0.019%)\
403\. R Routley (0.019%)\
403\. O Bazaluk (0.019%)\
403\. M Zimmerman (0.019%)\
403\. I Murdoch (0.019%)\
403\. B Skyrms (0.019%)\
403\. S Feferman (0.019%)\
403\. T Metz (0.019%)\
403\. E Balibar (0.019%)\
403\. K Rahner (0.019%)\
403\. D Hull (0.019%)\
403\. M Archer (0.019%)\
403\. K Lowith (0.019%)\
403\. R Bernasconi (0.019%)\
403\. S Weil (0.019%)\
403\. T Griffero (0.019%)\
403\. R Esposito (0.019%)\
403\. E Tugendhat (0.019%)\
440\. J Barwise (0.018%)\
440\. H Diels (0.018%)\
440\. R Giere (0.018%)\
440\. A Church (0.018%)\
440\. W Bechtel (0.018%)\
440\. J Ladyman (0.018%)\
440\. E Bloch (0.018%)\
440\. D Garrett (0.018%)\
440\. J Hick (0.018%)\
440\. H Kelsen (0.018%)\
440\. R Tuomela (0.018%)\
440\. B Lonergan (0.018%)\
440\. L Baker (0.018%)\
440\. Avicenna (0.018%)\
440\. E Stein (0.018%)\
440\. H Weyl (0.018%)\
440\. J Mc Mahan (0.018%)\
440\. M Thompson (0.018%)\
440\. D Bell (0.018%)\
440\. W Jaeger (0.018%)\
440\. J Van Cleve (0.018%)\
440\. JL Pollock (0.018%)\
440\. A Nehamas (0.018%)\
440\. W Brown (0.018%)\
440\. SO Hansson (0.018%)\
440\. D Copp (0.018%)\
440\. D Mellor (0.018%)\
440\. G Sher (0.018%)\
468\. E Schwitzgebel (0.017%)\
468\. R Kane (0.017%)\
468\. U Kriegel (0.017%)\
468\. R Sokolowski (0.017%)\
468\. P Simons (0.017%)\
468\. D Ihde (0.017%)\
468\. O Hoffe (0.017%)\
468\. E Zalta (0.017%)\
468\. R Langton (0.017%)\
468\. H Kornblith (0.017%)\
468\. J Burgess (0.017%)\
468\. W Heisenberg (0.017%)\
468\. A Gramsci (0.017%)\
468\. N Bobbio (0.017%)\
468\. F Feldman (0.017%)\
468\. T Hurka (0.017%)\
468\. E Schrodinger (0.017%)\
468\. GH Mead (0.017%)\
468\. C Levi Strauss (0.017%)\
468\. F Jameson (0.017%)\
468\. R Popkin (0.017%)\
468\. C Parsons (0.017%)\
468\. T Beauchamp (0.017%)\
468\. R Fogelin (0.017%)\
468\. W Chan (0.017%)\
468\. M Tooley (0.017%)\
468\. T Fuchs (0.017%)\
468\. D Brink (0.017%)\
468\. K Ameriks (0.017%)\
468\. S French (0.017%)\
468\. L Bon Jour (0.017%)\
468\. J Van Benthem (0.017%)\
468\. P Duhem (0.017%)\
468\. J Finnis (0.017%)\
468\. R Hanna (0.017%)\
468\. DW Smith (0.017%)\
468\. E Said (0.017%)\
468\. R Williams (0.017%)\
468\. F Beiser (0.017%)\
468\. R Martin (0.017%)\
468\. W Craig (0.017%)\
468\. R Kraut (0.017%)\
510\. H Plessner (0.016%)\
510\. E Berti (0.016%)\
510\. R Crisp (0.016%)\
510\. R Roberts (0.016%)\
510\. R Sorensen (0.016%)\
510\. S Shapin (0.016%)\
510\. D Harvey (0.016%)\
510\. WKC Guthrie (0.016%)\
510\. H White (0.016%)\
510\. C Diamond (0.016%)\
510\. M Gueroult (0.016%)\
510\. AC Graham (0.016%)\
510\. F Schleiermacher (0.016%)\
510\. J Pocock (0.016%)\
510\. D Scott (0.016%)\
510\. W Beierwaltes (0.016%)\
510\. C Hartshorne (0.016%)\
510\. M Bunge (0.016%)\
510\. C Sunstein (0.016%)\
510\. S Pinker (0.016%)\
510\. B Herman (0.016%)\
510\. N Levy (0.016%)\
510\. P Freire (0.016%)\
510\. H Poincare (0.016%)\
510\. M Schlick (0.016%)\
510\. R Bernet (0.016%)\
510\. P Suppes (0.016%)\
510\. Y Saito (0.016%)\
510\. F Suarez (0.016%)\
510\. C List (0.016%)\
510\. M Ruse (0.016%)\
510\. K Wiredu (0.016%)

Here are a few observations: First, while I am of course aware that Aristotle and Plato are ...like, important, I still find it pretty incredible that they come in first and third after having been dead for more than 2000 years. Second, there is a sharp drop-off after the first four authors (Aristotle, Kant, Plato, Heidegger): Their cumulative score is roughly equal to the cumulative score of the next fourteen authors (Wittgenstein to Habermas). Big Four? Third, a number of people in Schwitzgebel's comments asked questions/expressed dismay about the low ranks of various (European) authors. On the current list, these authors tend to rank much higher: Derrida (ranked #9), Foucault (#21), Merleau-Ponty (#23), Gadamer (#50), Adorno (#65) and Cavell (#90), for example, are all in the top 100.

Schwitzgebel makes it clear, of course, that his ranking only captures current influence in 'mainstream Anglophone philosophy,' and so the fact that Derrida, Foucault et al. are not particularly high up on his list is not surprising. The question, then, is: What does the current ranking capture? The answer I think depends a lot on whether the journals in my dataset capture published academic philosophy. he current ranking captures  is not unreasonable to claim that the current ranking is able to capture influence across philosophy more broadly. I will probably make a shiny app that allows people to select which journals they want included an the like, so that people who disagree can puruse the dataset at their own leasure.

Since this data is longitudinal (1975-2024), I also looked at . I made the graph interactive because it is a mess otherwise.
