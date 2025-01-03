---
title: "Measuring Conceptual Change in Philosophy: A Corpus Study"
date: 2025-01-01
---

Last year, together with two collaborators (Lucien Baumgartner; Krzysztof S&#281;kowski), I worked on a project that aimed to track the semantic disruptiveness of influential philosophy publications. We presented the material a couple of times, but ultimately decided that the project was not worth pursuing. Still, I thought the research was interesting enough methodologically to merit some sort of write up. That&#8217;s what this post is (though I&#8217;m mostly going to focus on the parts that I contributed).

The motivation for the project had to do with <em>conceptual engineering </em>(CE). I have to confess that even though I&#8217;ve now been to more than one workshop on CE, I&#8217;m still not entirely sure what CE is all about, so here&#8217;s a quote from Chalmers (2020): &#8220;Conceptual engineering is the design, implementation, and evaluation of concepts. Conceptual engineering includes or should include de novo conceptual engineering (designing a new concept) as well as conceptual re-engineering (fixing an old concept)&#8221; (1). Some philosophers think CE is a new thing; others disagree. One open question question is whether there are examples of articles or books in the philosophical literature that have caused significant conceptual change in the philosophical community (or parts of it) in the past. In addition to being open, the question is also an empirical one, and so we thought we&#8217;d attempt to address it using the tools of corpus linguistics. We chose three candidate concepts that plausibly underwent change in the recent history of philosophy: <em>belief </em>; <em>consciousness</em>; and <em>reference</em>. We chose these three examples because each features prominently in a very influential book or article published during the last 50 years that many see as having done much to change the concept in question (at least to some extent). For belief: Clark, A., &amp; Chalmers, D. (1998). &#8220;The Extended Mind.&#8221; <em>Analysis</em>, 58(1), 7&#8211;19; for consciousness: Chalmers, D. (1996). <em>The Conscious Mind: In Search of a Fundamental Theory</em>. Oxford University Press; for reference: Kripke, S. (1980). <em>Naming and Necessity</em>. Harvard University Press.

While major problems still remain with testing for conceptual change directly (e.g., Recchia et al., 2017; Hengchen et al., 2021), conceptual change tends to (though need not) go hand in hand with semantic change. This is useful because there are a number of well-established methods to detect and measure semantic change (for a survey, see, Tahmasebi et al., 2019). We chose to use (neural) word embeddings with temporal referencing (Dubossarsky et al., 2019); I&#8217;ll explain what that means in a bit.

To construct our corpus, I used a Python script to download the pdfs of all articles published in six [high-profile, generalist philosophy journals](https://leiterreports.typepad.com/blog/2022/07/best-general-philosophy-journals-2022.html) (<em>Australasian Journal of</em> <em>Philosophy</em>; <em>Analysis</em>; <em>Mind</em>; <em>Noûs</em>; <em>Philosophical Studies</em>; <em>Synthese</em>) between 1971 and 2021. We only included full-length, original articles (so no abstracts, book reviews, errata, etc.). I then removed cover pages, headers and footers, converted the pdfs to plain text and cleaned up the resulting text files. The table below shows the number of articles from each journal, as well as the total number of articles.

<br>
<table>
       <tr>
           <td class="thead depvarhead firsttablerow leftalign" style="font-weight:bold; font-style:normal;">Journal</td>
           <td class="thead depvarhead firsttablerow" style="font-weight:bold; font-style:normal;"><em>n</em></td>
       </tr>
       <tr>
           <td class="tdata firsttablecol"><em>Analysis</em></td>
           <td class="tdata centeralign">2654</td>
       </tr>
       <tr>
           <td class="tdata firsttablecol"><em>Australasian Journal of Philosophy</em></td>
           <td class="tdata centeralign">1608</td>
       </tr>
       <tr>
           <td class="tdata firsttablecol"><em>Mind</em></td>
           <td class="tdata centeralign">1976</td>
       </tr>
       <tr>
           <td class="tdata firsttablecol"><em>Noûs</em></td>
           <td class="tdata centeralign">1468</td>
       </tr>
       <tr>
           <td class="tdata firsttablecol"><em>Philosophical Studies</em></td>
           <td class="tdata centeralign">4967</td>
       </tr>
       <tr>
           <td class="tdata firsttablecol"><em>Synthese</em></td>
           <td class="tdata centeralign">5769</td>
       </tr>
       <tr>
           <td class="tdata leftalign firstsumrow">Total</td>
           <td class="tdata firstsumrow">18442</td>
       </tr>
       <tr>
           <th colspan="2" class="thead firsttablerow"></th>
       </tr>
</table>

Next, we constructed three sub-corpora, one for each target publication <em>T</em>. We reasoned that we should not expect semantic changes to show up across all of philosophy, just in articles on topics related to that of <em>T</em>. To define the limits of these sub-corpora, I used two restrictions. The first restriction is based on PhilPapers categories. PhilPapers is a &#8220;comprehensive index and bibliography of philosophy maintained by the community of philosophers.&#8221; In addition to lots of other useful meta-data, PhilPapers sorts many of its entries into one or more of &#8220;the traditional fields of philosophy&#8221; (both, [https://philpapers.org/help/categorization.html](https://philpapers.org/help/categorization.html); accessed Sept 11, 2023)&#8211;philosophy of mind, normative ethics, philosophy of physics, Asian philosophy, 17th/18th century philosophy, etc. 81.4% of articles in our dataset had at least one field listed. For each <em>T</em>, I excluded all articles that did not share at least one field in common with <em>T</em>.

While a good start, this first restriction alone would likely have been too permissive. Consider Chalmers (1996), which is categorized as Philosophy of Cognitive Science and Philosophy of Mind. Most of the articles published in these two fields are not on belief, and so to keep them all in the sub-corpus would plausibly have muddied the waters. I therefore introduced a second restriction. For each of the three sub-corpora (including <em>T</em>; restricted to nouns), I used LDA (with 2000 Gibbs samples) to identify major topics. As the threshold probability, I more or less arbitrarily picked 0<em>.</em>1 (this resulted in 2 major topics for each of our target publications): If the posterior probability of a topic in a article was at least 0<em>.</em>1, then I considered that topic to be one of the major topics of that article. Figure 1 shows the results. I then restricted each sub-corpus to articles that shared at least one major topic with <em>T</em>. This left us with 384 texts for Kripke (1980) (2861310 words); 281 texts for Chalmers (1996) (2652613 words); and 498 texts for Clark and Chalmers (1998) (4226818 words).

![Figure 1. Topic distributions with major topics (black); <em>k</em> is the total number of topics.]({{site.url}}/something-of-crunch/assets/images/2025-01-01/figure0NEW.png){: width="90%"}
<p style="text-align:center; font-size: 0.85em; padding-right: 30px; padding-left: 30px;">Figure 1. Topic distributions with major topics (black); <em>k</em> is the total number of topics.</p>
<br>

To create embeddings of our target words (<em>w</em><sub>T</sub>s), we used two common methods, <em>word2vec </em>(Mikolov et al., 2013) and <em>BERT </em>(Devlin et al., 2019).[^1] word2vec creates static embeddings (for each word, the model creates a single, context-independent vector), while embeddings created with BERT are context sensitive (the same word can get multiple different embedding vectors depending on its context in the text), and so we thought it might be nice to compare the two. I worked with word2vec, and so that&#8217;s what I&#8217;ll focus on. The process for BERT was similar, however, and I&#8217;ll mention how the BERT embeddings compared to the word2vec embeddings.

[^1]: For visual introductions to these models, see https://jalammar.github.io/illustrated-word2vec/ and https://jalammar.github.io/illustrated-bert/.

To prepare our sub-corpora for training, I removed all stop words, words not in the English dictionary and single letter words. I also lemmatized and POS-tagged all texts. This was done because we were only interested in our target words as nouns, yet one of them (reference) can also be a verb.

Recall that our goal was to investigate if the meaning of any of our three target words has changed perceptibly since 1971 in relevant parts of the philosophical literature. To do so, we used temporal referencing (Dubossarsky et al., 2019). The idea is simple: First, label your target word(s) with their time information; then, train a global model on the entire corpus. Since in our case, there were generally many articles per year, we decided to label target words not just with their year, but also with the article ID. So, for example, occurrences of &#8216;belief//NOUN&#8217; in Clark and Chalmers (1998) became &#8216;belief//NOUN_Analysis_1998_58_1_7-19&#8217;. For each of our three sub-corpora, I then trained a SGNS model (dim = 300, window = 10). To investigate semantic change, we traced the average pairwise cosine similarity over time. For years <em>y </em>and <em>y</em>+1, I calculated the pairwise cosine similarity between each of <em>w</em><sub>T</sub>&#8217;s embeddings in texts published in <em>y </em>(one for each text since word2vec generates static embeddings) and each of <em>w</em><sub>T</sub>&#8217;s embeddings in texts published in <em>y</em>+1, and then averaged these values. Figure 2 shows the results.

![Figure 2. Average pairwise cosine similarities over time for our three target words; errorbars show 95\% confidence intervals.]({{site.url}}/something-of-crunch/assets/images/2025-01-01/figure1.png){: width="95%"}
<p style="text-align:center; font-size: 0.85em; padding-right: 30px; padding-left: 30px;">Figure 2. Average pairwise cosine similarities over time for our three target words; errorbars show 95\% confidence intervals.</p>
<br>

Are there identifiable points at which the meaning of our <em>w</em><sub>T</sub>s has changed? To test for this, we used change-point detection. There are many methods to look for change-points in time series data (for a survey, see, Aminikhanghahi and Cook, 2017); here, we used kernel-based change point analysis with a linear kernel. The basic idea with this method is to average all the values in the time series within a certain window of time immediately before and after a given candidate change-point, and then to check if the difference between these two means exceeds a certain threshold. If it does, a (local) change-point has been detected. The table below shows the results, for the word2vec embeddings as well as the BERT embeddings. We find that the only <em>w</em><sub>T</sub> for which there is evidence of the presence of local change-points across both models is &#8216;consciousness.&#8217; (Lucien had BERT generate two different kinds of embedding, narrow word embeddings, for which the model considers a relatively small window of tokens around each word, and broad usage embeddings, for which the model considers a much larger window of tokens around each word [in this case, 128]).

<br>
<table>
    <tr>
        <td class="thead depvarhead firsttablerow leftalign" style="font-weight:bold; font-style:normal;">Embedding</td>
        <td class="thead depvarhead firsttablerow leftalign" style="font-weight:bold; font-style:normal;"><em>w</em><sub>T</sub></td>
        <td class="thead depvarhead firsttablerow centeralign" style="font-weight:bold; font-style:normal;">Window</td>
        <td class="thead depvarhead firsttablerow leftalign" style="font-weight:bold; font-style:normal;">Change-points</td>
    </tr>
    <tr>
       <th colspan="4" class="depvarhead">word2vec</th>
    </tr>
    <tr>
       <td class="tdata firsttablecol">---</td>
       <td class="tdata">consciousness</td>
       <td class="tdata centeralign">4</td>
       <td class="tdata">2000</td>
    </tr>
    <tr>
       <td class="tdata firsttablecol">---</td>
        <td class="tdata">consciousness</td>
        <td class="tdata centeralign">5</td>
        <td class="tdata">1998</td>
    </tr>
    <tr>
       <td class="tdata firsttablecol">---</td>
        <td class="tdata">reference</td>
        <td class="tdata centeralign">2</td>
        <td class="tdata">1996</td>
    </tr>
    <tr>
       <td class="tdata firsttablecol">---</td>
        <td class="tdata">reference</td>
        <td class="tdata centeralign">3</td>
        <td class="tdata">1996</td>
    </tr>
    <tr>
       <td class="tdata firsttablecol">---</td>
        <td class="tdata">reference</td>
        <td class="tdata centeralign">4</td>
        <td class="tdata">1997</td>
    </tr>
    <tr>
       <td class="tdata firsttablecol">---</td>
        <td class="tdata">reference</td>
        <td class="tdata centeralign">5</td>
        <td class="tdata">1996</td>
    </tr>
    <tr>
       <th colspan="4" class="depvarhead firstsumrow">BERT</th>
    </tr>
    <tr>
       <td class="tdata firsttablecol">broad</td>
        <td class="tdata">consciousness</td>
        <td class="tdata centeralign">2</td>
        <td class="tdata">1993</td>
    </tr>
    <tr>
       <td class="tdata firsttablecol">broad</td>
        <td class="tdata">consciousness</td>
        <td class="tdata centeralign">3</td>
        <td class="tdata">1992</td>
    </tr>
    <tr>
       <td class="tdata firsttablecol">broad</td>
        <td class="tdata">consciousness</td>
        <td class="tdata centeralign">4</td>
        <td class="tdata">1993</td>
    </tr>
    <tr>
       <td class="tdata firsttablecol">broad</td>
        <td class="tdata">consciousness</td>
        <td class="tdata centeralign">5</td>
        <td class="tdata">1994</td>
    </tr>
    <tr>
       <td class="tdata firsttablecol">narrow</td>
        <td class="tdata">consciousness</td>
        <td class="tdata centeralign">2</td>
        <td class="tdata">1976, 1977, 1981, 1983, 1988, 1991, 1993, 1994, 1998</td>
    </tr>
    <tr>
       <td class="tdata firsttablecol">narrow</td>
        <td class="tdata">consciousness</td>
        <td class="tdata centeralign">3</td>
        <td class="tdata">1976, 1983, 1987, 1994, 1997</td>
    </tr>
    <tr>
       <td class="tdata firsttablecol">narrow</td>
        <td class="tdata">consciousness</td>
        <td class="tdata centeralign">4</td>
        <td class="tdata">1998</td>
    </tr>
    <tr>
       <th colspan="4" class="thead firsttablerow"></th>
    </tr>
</table>

Next, we wanted to investigate the possible role of our target texts. Recall that we chose our three <em>w</em><sub>T</sub>s because each features prominently in a very influential book or article published during the last 50 years that many see as having done much to change the concept in question. To do so, we relied on the idea of a text&#8217;s <em>disruptiveness </em>with respect to some word&#8217;s meaning: when a text <em>T </em>is disruptive with respect to a given word&#8217;s meaning, then that word&#8217;s meaning will be tend to be more similar to its meaning in texts published after <em>T </em>(because <em>T </em>had an influence on these texts) than to texts published before <em>T</em> (see, Hogenbirk, 2023). To quantify disruptiveness, we defined a disruptiveness score <em>D</em>:

$$D_{T,w} = \frac{1}{n_{\text{after}}} \sum_{t | y_T + o_{\text{after}} < y_t \leq y_T + o_{\text{after}} + r} \cos(w_T, w_t) -\\ \frac{1}{n_{\text{before}}} \sum_{t | y_T - o_{\text{before}} - r \leq y_t < y_T - o_{\text{before}}} \cos(w_T, w_t),$$

with <em>y</em><sub>i</sub> the year of text <em>i</em>&#8217;s publication, <em>o</em><sub>before</sub> and <em>o</em><sub>after</sub> offsets (how many years immediately before/after <em>T </em>are not to be included in the calculation), <em>r </em>the time window [how many years before/after <em>T </em>(minus/plus the offset) to include in the calculation], and <em>n</em><sub>before</sub> and <em>n</em><sub>after</sub> the numbers of text published in <em>r </em>before/after <em>T</em>. The interpretation of this score is that if <em>D &#x003E; </em>0, then the target text <em>T </em>was more similar to texts published after it than to texts before it (with respect to the meaning of <em>w</em>), and so it was disruptive. 

Figure 3 shows <em>D</em>-score rankings for our three sub-corpora. None of the three target texts rank near the top; in fact, their <em>D</em>-scores are all negative. (The BERT embeddings yielded similar results.) Hence, we did not find evidence that any of our targets text were unusually disruptive with respect to their target words.

![Figure 3. Ranking of <em>D</em>-scores for each of our three sub-corpora (target text in red; <em>o</em><sub>before</sub> = <em>o</em><sub>after</sub> = 0; <em>r</em> = 10)]({{site.url}}/something-of-crunch/assets/images/2025-01-01/figure2.png){: width="60%"}
<p style="text-align:center; font-size: 0.85em; padding-right: 30px; padding-left: 30px;">Figure 3. Ranking of <em>D</em>-scores for each of our three sub-corpora (target text in red; <em>o</em><sub>before</sub> = <em>o</em><sub>a</sub> = 0; <em>r</em> = 10)</p>
<br>

<em>D</em>-scores need not be constant over time. This means that even though our target texts were not unusually disruptive globally, they may still have been unusually disruptive for their time. To investigate this possibility, for each sub-corpus, I calculated the average <em>D</em>-score for each year and compared it with our target&#8217;s <em>D</em>-score (Figure 4). For Clark and Chalmers (1998) and Kripke (1980), we see little evidence for <em>D</em>-score fluctuations over time. In contrast, in the case of Chalmers (1996), Figure 4 shows a spike in the average disruptiveness of articles with respect to consciousness around the time of that text&#8217;s publication. Note, however, that we did not find this spike for the BERT embeddings; moreover, the 95% confidence intervals are such that our results are also consistent with no spike at all.

![Figure 4. Average <em>D</em>-scores over time for each of our three sub-corpora (target text in red; <em>o</em><sub>before</sub> = <em>o</em><sub>after</sub> = 0; <em>r</em> = 10); errorbars show 95% confidence intervals.]({{site.url}}/something-of-crunch/assets/images/2025-01-01/figure3.png){: width="75%"}
<p style="text-align:center; font-size: 0.85em; padding-right: 30px; padding-left: 30px;">Figure 4. Average <em>D</em>-scores over time for each of our three sub-corpora (target text in red; <em>o</em><sub>before</sub> = <em>o</em><sub>after</sub> = 0; <em>r</em> = 10); errorbars show 95% confidence intervals.</p>
<br>

So far, I have used <em>o</em><sub>before</sub> = <em>o</em><sub>after</sub> = 0 and <em>r </em>= 10. Perhaps it takes longer than 10 years for a text&#8217;s disruptiveness to be felt in the relevant literature. To investigate this, I re-calculated the <em>D</em>-scores using a range of different offsets <em>o</em><sub>after</sub>. Note that the maximum possible value of <em>o</em><sub>after</sub> depends on a text&#8217;s year of publication. Figure 5 shows the results. The figure suggests that the choice of <em>o</em><sub>after</sub> does not have a major impact. 

![Figure 5. <em>D</em>-scores for different values of <em>o</em><sub>after</sub> (<em>r</em> = 10; target texts in red; average <em>D</em>-score in black).]({{site.url}}/something-of-crunch/assets/images/2025-01-01/figure4.png){: width="95%"}
<p style="text-align:center; font-size: 0.85em; padding-right: 30px; padding-left: 30px;">Figure 5. <em>D</em>-scores for different values of <em>o</em><sub>after</sub> (<em>r</em> = 10; target texts in red; average <em>D</em>-score in black).</p>
<br>

Are there examples of articles or books in the philosophical literature that have caused significant conceptual change in the recent history of analytic philosophy? Of the three candidate examples we investigated (belief; consciousness; reference), only consciousness showed robust evidence of semantic change. After mapping the semantic similarity of &#8216;consciousness&#8217; in a suitable corpus of philosophy articles published since 1971 over time, we detected the presence of local change-points for embeddings generated using two different methods (word2vec, BERT). However, even though many of these change-points lay roughly in the neighbourhood of the publication of Chalmers (1996), the results of our <em>D</em>-score analysis do not suggest that Chalmers (1996) itself was unusually disruptive with respect to the meaning of &#8216;consciousness&#8217;. Our results, then, do not support the idea that any of our three target texts caused substantial conceptual change in the philosophical literature.

To end, I want to briefly describe two of the main problems that ultimately lead me to not want to pursue the project further. The first is practical. Our corpus consisted of articles published in or after 1971. This meant that we were limited to target texts published after 1971. Yet most of the target texts that we (and others) thought worth investigating (e.g., Tarski, 1936; Gettier, 1963; Carnap, 1936) were published (long) before 1971. In addition, two of our target text were published in the second half of the 1990s, meaning that we only had <span class="lmsy-10x-x-109">~</span>25 years worth of data to investigate&#8212;conceptual change might take longer than that, however. The problem is that the further back into the past one wants to go, the more difficult and labour-intensive it becomes to assemble a corpus of sufficient quality: generally, the older a document, the more annoying it is going to be to convert it into clean plain text.

The second problem is a fundamental methodological problem. To be persuaded that our methods do what we want them to do, we&#8217;d (minimally) need a set of examples for which we are <em>reasonably certain </em>that they have undergone conceptual change to calibrate these methods against. While some studies have attempted this sort of calibration in the past (e.g., Martinc et al., 2020), our corpus consisted of philosophy publications&#8212;not a discipline particularly known for its plain or ordinary use of English. This makes it doubtful that these previous results (which are, in my opinion, not that overwhelming to begin with) generalize to our corpus. Instead, what we would have needed are clear-cut examples of conceptual change <em>specifically </em>in the philosophical literature (ideally, in the last 50 years or so). Yet the sense I got while working on this project is that such examples might be impossible to find. When we presented the material, I cannot remember a single example of a concept for which everyone in the room agreed that it had undergone substantial change: not among our chosen examples, nor among any of the many alternative examples people suggested to us. In light of this, it felt a bit pointless to pour lots more time and effort into the project, given that fundamental methodological doubts would likely have always remained.

**References**

<div style="text-indent: -2em; padding-left: 2em;">Aminikhanghahi, S., &amp; Cook, D.&#x00A0;J. (2017). A survey of methods for time series change point detection. <em>Knowledge and Information Systems</em>, <em>51</em>(2), 339&#8211;367. https://doi.org/10.1007/s10115-016-0987-z.</div>
<div style="text-indent: -2em; padding-left: 2em;">Carnap, R. (1936). Testability and Meaning. <em>Philosophy of Science</em>, <em>3</em>(4), 419&#8211;471.</div>
<div style="text-indent: -2em; padding-left: 2em;">Chalmers, D.&#x00A0;J. (1996). <em>The Conscious Mind: In Search of a Fundamental Theory</em>. Oxford University Press.</div>
<div style="text-indent: -2em; padding-left: 2em;">Chalmers, D.&#x00A0;J. (2020). What is conceptual engineering and what should it be? <em>Inquiry</em>, 1&#8211;18. https://doi.org/10.1080/0020174X.2020.1817141.</div>
<div style="text-indent: -2em; padding-left: 2em;">Clark, A., &amp; Chalmers, D. (1998). The Extended Mind. <em>Analysis</em>, <em>58</em>(1), 7&#8211;19. https://doi.org/10.1111/1467-8284.00096.</div>
<div style="text-indent: -2em; padding-left: 2em;">Devlin, J., Chang, M.-W., Lee, K., &amp; Toutanova, K. (2019). BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding. https://doi.org/10.48550/arXiv.1810.04805.</div>
<div style="text-indent: -2em; padding-left: 2em;">Dubossarsky, H., Hengchen, S., Tahmasebi, N., &amp; Schlechtweg, D. (2019). Time-Out: Temporal Referencing for Robust Modeling of Lexical Semantic Change. <em>Proceedings</em> <em>of the 57th Annual Meeting of the Association for Computational Linguistics</em>, 457&#8211;470. https://doi.org/10.18653/v1/P19-1044.</div>
<div style="text-indent: -2em; padding-left: 2em;">Gettier, E.&#x00A0;L. (1963). Is justified true belief knowledge? <em>Analysis</em>, <em>23</em>(6), 121&#8211;123.</div>
<div style="text-indent: -2em; padding-left: 2em;">Hengchen, S., Tahmasebi, N., Schlechtweg, D., &amp; Dubossarsky, H. (2021). Challenges for computational lexical semantic change. In N. Tahmasebi, L. Borin, A. Jatowt, Y. Xu, &amp; S. Hengchen (Eds.), <em>Computational approaches to semantic change</em> (pp.&#x00A0;341&#8211;372). Zenodo. https://doi.org/10.5281/ZENODO.5040241.</div>
<div style="text-indent: -2em; padding-left: 2em;">Hogenbirk, H.&#x00A0;D. (2023). <em>Each book its own Babel: Conceptual unity and disunity in</em> <em>early modern natural philosophy</em>. University of Groningen. https://doi.org/10.33612/diss.849175103.</div>
<div style="text-indent: -2em; padding-left: 2em;">Kripke, S.&#x00A0;A. (1980). <em>Naming and necessity</em>. Harvard University Press.</div>
<div style="text-indent: -2em; padding-left: 2em;">Martinc, M., Montariol, S., Zosa, E., &amp; Pivovarova, L. (2020). Capturing Evolution in Word Usage: Just Add More Clusters? <em>Companion Proceedings of the Web Conference</em> <em>2020</em>, 343&#8211;349. https://doi.org/10.1145/3366424.3382186.</div>
<div style="text-indent: -2em; padding-left: 2em;">Mikolov, T., Chen, K., Corrado, G., &amp; Dean, J. (2013). Efficient Estimation of Word Representations in Vector Space. https://doi.org/10.48550/arXiv.1301.3781.</div>
<div style="text-indent: -2em; padding-left: 2em;">Recchia, G., Jones, E., Nulty, P., Regan, J., &amp; De Bolla, P. (2017). Tracing Shifting Conceptual Vocabularies Through Time. In P. Ciancarini, F. Poggi, M. Horridge, J. Zhao, T. Groza, M.&#x00A0;C. Suarez-Figueroa, M. d&#8217;Aquin, &amp; V. Presutti (Eds.), <em>Knowledge Engineering and Knowledge Management </em>(pp.&#x00A0;19&#8211;28, Vol.&#x00A0;10180). Springer International Publishing. https://doi.org/10.1007/978-3-319-58694-6_2.</div>
<div style="text-indent: -2em; padding-left: 2em;">Tahmasebi, N., Borin, L., &amp; Jatowt, A. (2019). Survey of Computational Approaches to Lexical Semantic Change. https://doi.org/10.48550/arXiv.1811.06278.</div>
<div style="text-indent: -2em; padding-left: 2em;">Tarski, A. (1936). Der Wahrheitsbegriff in den Formalisierten Sprachen. <em>Studia</em> <em>Philosophica</em>, <em>1</em>, 261&#8211;405.</div>
