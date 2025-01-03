---
title: "Measuring Conceptual Change in Philosophy: A Corpus Study"
date: 2025-01-01
---
<p class="noindent" >Last year, together with two collaborators (Lucien Baumgartner; Krzysztof S&#281;kowski), I worked on a
project that aimed to track the semantic disruptiveness of influential philosophy publications. We
presented the material a couple of times, but ultimately decided that the project was not worth
pursuing. Still, I thought the research was interesting enough methodologically to merit some sort of
write up. That&#8217;s what this post is (though I&#8217;m mostly going to focus on the parts that I
contributed).
<!--l. 65--><p class="indent" >   The motivation for the project had to do with <span 
class="ec-lmri-10x-x-109">conceptual engineering </span>(CE). I have to confess
that even though I&#8217;ve now been to more than one workshop on CE, I&#8217;m still not entirely sure what
CE is all about, so here&#8217;s a quote from <a 
 id="x1-2"></a>Chalmers (2020): &#8220;Conceptual engineering is the
design, implementation, and evaluation of concepts. Conceptual engineering includes
or should include de novo conceptual engineering (designing a new concept) as well as
conceptual re-engineering (fixing an old concept)&#8221; (1). Some philosophers think CE is a
new thing; others disagree. One open question question is whether there are examples of
articles or books in the philosophical literature that have caused significant conceptual
change in the philosophical community (or parts of it) in the past. In addition to being
open, the question is also an empirical one, and so we thought we&#8217;d attempt to address it
using the tools of corpus linguistics. We chose three candidate concepts that plausibly
underwent change in the recent history of philosophy: <span 
class="ec-lmri-10x-x-109">belief </span>; <span 
class="ec-lmri-10x-x-109">consciousness</span>; and <span 
class="ec-lmri-10x-x-109">reference</span>.
We chose these three examples because each features prominently in a very influential
book or article published during the last 50 years that many see as having done much
to change the concept in question (at least to some extent). For belief: Clark, A., &amp;
Chalmers, D. (1998). &#8220;The Extended Mind.&#8221; <span 
class="ec-lmri-10x-x-109">Analysis</span>, 58(1), 7&#8211;19; for consciousness:
Chalmers, D. (1996). <span 
class="ec-lmri-10x-x-109">The Conscious Mind: In Search of a Fundamental Theory</span>. Oxford
University Press; for reference: Kripke, S. (1980). <span 
class="ec-lmri-10x-x-109">Naming and Necessity</span>. Harvard University
Press.
<!--l. 67--><p class="indent" >   While major problems still remain with testing for conceptual change directly (e.g., <a 
 id="x1-3"></a>Recchia
et al., 2017; <a 
 id="x1-4"></a>Hengchen et al., 2021), conceptual change tends to (though need not) go hand in hand
with semantic change. This is useful because there are a number of well-established methods to
detect and measure semantic change (for a survey, see, <a 
 id="x1-5"></a>Tahmasebi et al., 2019). We chose to use
(neural) word embeddings with temporal referencing (<a 
 id="x1-6"></a>Dubossarsky et al., 2019); I&#8217;ll explain what
that means in a bit.
<!--l. 69--><p class="indent" >   To construct our corpus, I used a Python script to download the pdfs of all articles published in
                                                                                     
                                                                                     
six high-profile (see, <a 
 id="x1-7"></a>Leiter, 2022), generalist philosophy journals (<span 
class="ec-lmri-10x-x-109">Australasian Journal of</span>
<span 
class="ec-lmri-10x-x-109">Philosophy</span>; <span 
class="ec-lmri-10x-x-109">Analysis</span>; <span 
class="ec-lmri-10x-x-109">Mind</span>; <span 
class="ec-lmri-10x-x-109">No</span><span 
class="ec-lmri-10x-x-109">�s</span>; <span 
class="ec-lmri-10x-x-109">Philosophical Studies</span>; <span 
class="ec-lmri-10x-x-109">Synthese</span>) between 1971 and 2021. We only
included full-length, original articles (so no abstracts, book reviews, errata, etc.). I then removed
cover pages, headers and footers, converted the pdfs to plain text and cleaned up the resulting text
files. Table <a 
href="#x1-8r1">1<!--tex4ht:ref: tab:articles_from_different_journals --></a> shows the number of articles from each journal, as well as the total number of
articles.
   <div class="table">
                                                                                     
                                                                                     
<!--l. 71--><p class="indent" >   <hr class="float"><div class="float" 
>
                                                                                     
                                                                                     
<div class="tabular">
 <table id="TBL-2" class="tabular" 
 
><colgroup id="TBL-2-1g"><col 
id="TBL-2-1"><col 
id="TBL-2-2"></colgroup><tr  
 style="vertical-align:baseline;" id="TBL-2-1-"><td  style="white-space:nowrap; text-align:left;" id="TBL-2-1-1"  
class="td11"> Journal                                     </td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-1-2"  
class="td11">   <span 
class="lmmi-10x-x-109">n    </span></td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-2-2-"><td  style="white-space:nowrap; text-align:left;" id="TBL-2-2-1"  
class="td11"> <span 
class="ec-lmri-10x-x-109">Analysis                                  </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-2-2"  
class="td11">  2654  </td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-2-3-"><td  style="white-space:nowrap; text-align:left;" id="TBL-2-3-1"  
class="td11"> <span 
class="ec-lmri-10x-x-109">Australasian Journal of Philosophy  </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-3-2"  
class="td11">  1608  </td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-2-4-"><td  style="white-space:nowrap; text-align:left;" id="TBL-2-4-1"  
class="td11"> <span 
class="ec-lmri-10x-x-109">Mind                                      </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-4-2"  
class="td11">  1976  </td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-2-5-"><td  style="white-space:nowrap; text-align:left;" id="TBL-2-5-1"  
class="td11"> <span 
class="ec-lmri-10x-x-109">No</span><span 
class="ec-lmri-10x-x-109">�s                                       </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-5-2"  
class="td11">  1468  </td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-2-6-"><td  style="white-space:nowrap; text-align:left;" id="TBL-2-6-1"  
class="td11"> <span 
class="ec-lmri-10x-x-109">Philosophical Studies                   </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-6-2"  
class="td11">  4967  </td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-2-7-"><td  style="white-space:nowrap; text-align:left;" id="TBL-2-7-1"  
class="td11"> <span 
class="ec-lmri-10x-x-109">Synthese                                  </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-7-2"  
class="td11">  5769  </td>

</tr><tr  
 style="vertical-align:baseline;" id="TBL-2-8-"><td  style="white-space:nowrap; text-align:left;" id="TBL-2-8-1"  
class="td11"> Total                                         </td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-8-2"  
class="td11"> 18442  </td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-2-9-"><td  style="white-space:nowrap; text-align:left;" id="TBL-2-9-1"  
class="td11">                               </td></tr></table>                                                </div>
<a 
 id="x1-8r1"></a>
<br />                                                                                     <div class="caption" 
><span class="id">
Table&#x00A0;1: </span><span  
class="content">Number of articles in our corpus from the different journals.
</span></div><!--tex4ht:label?: x1-8r1 -->
                                                                                     
                                                                                     
   </div><hr class="endfloat" />
   </div>
<!--l. 91--><p class="indent" >   Next, we constructed three sub-corpora, one for each target publication <span 
class="ec-lmri-10x-x-109">T</span>. We reasoned that we
should not expect semantic changes to show up across all of philosophy, just in articles on topics
related to that of <span 
class="lmmi-10x-x-109">T</span>. To define the limits of these sub-corpora, I used two restrictions. The first
restriction is based on PhilPapers categories. PhilPapers is a &#8220;comprehensive index and bibliography
of philosophy maintained by the community of philosophers.&#8221; In addition to lots of other useful
meta-data, PhilPapers sorts many of its entries into one or more of &#8220;the traditional fields of
philosophy&#8221; (both, https://philpapers.org/help/categorization.html; accessed Sept 11,
2023)&#8211;philosophy of mind, normative ethics, philosophy of physics, Asian philosophy, 17th/18th
century philosophy, etc. 81.4% of articles in our dataset had at least one field listed.
For each <span 
class="lmmi-10x-x-109">T</span>, I excluded all articles that did not share at least one field in common with
<span 
class="lmmi-10x-x-109">T</span>.
<!--l. 93--><p class="indent" >   While a good start, this first restriction alone would likely have been too permissive. Consider
<a 
 id="x1-9"></a>Chalmers (1996), which is categorized as Philosophy of Cognitive Science and Philosophy of Mind.
Most of the articles published in these two fields are not on belief, and so to keep them all in the
sub-corpus would plausibly have muddied the waters. I therefore introduced a second restriction. For
each of the three sub-corpora (including <span 
class="lmmi-10x-x-109">T</span>; restricted to nouns), I used LDA (with <span 
class="rm-lmr-10x-x-109">2000</span>
Gibbs samples) to identify major topics. As the threshold probability, I more or less
arbitrarily picked <span 
class="rm-lmr-10x-x-109">0</span><span 
class="lmmi-10x-x-109">.</span><span 
class="rm-lmr-10x-x-109">1 </span>(this resulted in 2 major topics for each of our target publications): If
the posterior probability of a topic in a article was at least <span 
class="rm-lmr-10x-x-109">0</span><span 
class="lmmi-10x-x-109">.</span><span 
class="rm-lmr-10x-x-109">1</span>, then I considered that
topic to be one of the major topics of that article. Figure <a 
href="#x1-18r1">1<!--tex4ht:ref: fig:topic-model --></a> shows the results Chalmers
(1996). I then restricted each sub-corpus to articles that shared at least one major topic
with <span 
class="lmmi-10x-x-109">T</span>. This left us with <span 
class="rm-lmr-10x-x-109">384 </span>texts for <a 
 id="x1-10"></a>Kripke (1980) (<span 
class="rm-lmr-10x-x-109">2861310 </span>words); <span 
class="rm-lmr-10x-x-109">281 </span>texts for
Chalmers (1996) (<span 
class="rm-lmr-10x-x-109">2652613 </span>words); and <span 
class="rm-lmr-10x-x-109">498 </span>texts for <a 
 id="x1-11"></a>Clark and Chalmers (1998) (<span 
class="rm-lmr-10x-x-109">4226818</span>
words).
<!--l. 95--><p class="indent" >   <hr class="figure"><div class="figure" 
>
                                                                                     
                                                                                     
                                                                                     
                                                                                     
<div class="subfigure">
<!--l. 97--><p class="noindent" ><!--l. 99--><p class="noindent" ><img 
src="topics_1.png" alt="PIC"  
width="210" height="210" > <a 
 id="x1-12r1"></a>
<div class="caption" ><span class="id"><span 
class="ec-lmr-10">(a) </span></span><span  
class="content"><span 
class="ec-lmr-10">Results (</span><span 
class="lmmi-10">k </span><span 
class="rm-lmr-10">= 35</span><span 
class="ec-lmr-10">) for Kripke (1980).</span>        </span></div></div>                                            <div class="subfigure">
<!--l. 103--><p class="noindent" ><!--l. 105--><p class="noindent" ><img 
src="topics_2.png" alt="PIC"  
width="210" height="210" > <a 
 id="x1-14r2"></a>
<div class="caption" ><span class="id"><span 
class="ec-lmr-10">(b) </span></span><span  
class="content"><span 
class="ec-lmr-10">Results (</span><span 
class="lmmi-10">k </span><span 
class="rm-lmr-10">= 35</span><span 
class="ec-lmr-10">) for Chalmers (1996).</span>     </span></div></div>
<div class="subfigure">
<!--l. 110--><p class="noindent" ><!--l. 112--><p class="noindent" ><img 
src="topics_4.png" alt="PIC"  
width="244" height="244" > <a 
 id="x1-16r3"></a>
<div class="caption" ><span class="id"><span 
class="ec-lmr-10">(c) </span></span><span  
class="content"><span 
class="ec-lmr-10">Results (</span><span 
class="lmmi-10">k </span><span 
class="rm-lmr-10">= 35</span><span 
class="ec-lmr-10">) for Clark and Chalmers (1998).</span>   </span></div></div> <a 
 id="x1-18r1"></a>
<div class="caption" ><span class="id">Figure&#x00A0;1: </span><span  
class="content">Topic distributions with major topics (black); <span 
class="lmmi-10x-x-109">k </span>is the total number of topics.
</span></div>
                                                                                     
                                                                                     
<!--l. 117--><p class="indent" >   </div><hr class="endfigure">
<!--l. 119--><p class="indent" >   To create embeddings of our target words (<span 
class="lmmi-10x-x-109">w</span><sub>T</sub>s), we used two common
methods, <span 
class="ec-lmri-10x-x-109">word2vec </span>(<a 
 id="x1-19"></a>Mikolov et al., 2013) and <span 
class="ec-lmri-10x-x-109">BERT </span>(<a 
 id="x1-20"></a>Devlin et al.,
2019).<span class="footnote-mark"><a 
href="Blog_post_20242.html#fn1x0"><sup class="textsuperscript">1</sup></a></span><a 
 id="x1-21f1"></a> 
word2vec creates static embeddings (for each word, the model creates a single, context-independent
vector), while embeddings created with BERT are context sensitive (the same word can get multiple
different embedding vectors depending on its context in the text), and so we thought it might be
nice to compare the two. I worked with word2vec, and so that&#8217;s what I&#8217;ll focus on. The process for
BERT was similar, however, and I&#8217;ll mention how the BERT embeddings compared to the word2vec
embeddings.
<!--l. 121--><p class="indent" >   To prepare our sub-corpora for training, I removed all stop words, words not in the English
dictionary and single letter words. I also lemmatized and POS-tagged all texts. This was done
because we were only interested in our target words as nouns, yet one of them (reference) can also
be a verb.
<!--l. 123--><p class="indent" >   Recall that our goal was to investigate if the meaning of any of our three target words has
changed perceptibly since 1971 in relevant parts of the philosophical literature. To do so, we used
temporal referencing (<a 
 id="x1-23"></a>Dubossarsky et al., 2019). The idea is simple: First, label your target word(s)
with their time information; then, train a global model on the entire corpus. Since in our case, there
were generally many articles per year, we decided to label target words not just with their year, but
also with the article ID. So, for example, occurrences of &#8216;belief//NOUN&#8217; in <a 
 id="x1-24"></a>Clark and Chalmers
(1998) became &#8216;belief//NOUN_Analysis_1998_58_1_7-19&#8217;. For each of our three sub-corpora, I
then trained a SGNS model (dim <span 
class="rm-lmr-10x-x-109">= 300</span>, window <span 
class="rm-lmr-10x-x-109">= 10</span>).
<!--l. 125--><p class="indent" >   To investigate semantic change, we traced the average pairwise cosine similarity over time. For
years <span 
class="lmmi-10x-x-109">y </span>and <span 
class="lmmi-10x-x-109">y </span><span 
class="rm-lmr-10x-x-109">+ 1</span>, I calculated the pairwise cosine similarity between each of <span 
class="lmmi-10x-x-109">w</span><sub>T</sub>&#8217;s embeddings in
texts published in <span 
class="lmmi-10x-x-109">y </span>(one for each text since word2vec generates static embeddings) and each of
<span 
class="lmmi-10x-x-109">w</span><sub>T</sub>&#8217;s embeddings in texts published in <span 
class="lmmi-10x-x-109">y </span><span 
class="rm-lmr-10x-x-109">+ 1</span>, and then averaged these values. Figure <a 
href="#x1-18r1">1<!--tex4ht:ref: fig:topic-model --></a> shows the
results.
<!--l. 127--><p class="indent" >   <hr class="figure"><div class="figure" 
>
                                                                                     
                                                                                     
                                                                                     
                                                                                     
<!--l. 129--><p class="noindent" ><img 
src="figure1.png" alt="PIC"  
width="332" height="332" > <a 
 id="x1-25r2"></a>
<br />                                                                                     <div class="caption" 
><span class="id">
Figure&#x00A0;2: </span><span  
class="content">Average pairwise cosine similarities over time for our three target words; errorbars
show 95% confidence intervals.                                                         </span></div><!--tex4ht:label?: x1-25r2 -->
                                                                                     
                                                                                     
<!--l. 131--><p class="indent" >   </div><hr class="endfigure">
<!--l. 133--><p class="indent" >   Are there identifiable points at which the meaning of our <span 
class="lmmi-10x-x-109">w</span><sub>T</sub>s has changed? To test for
this, we used change-point detection. There are many methods to look for change-points
in time series data (for a survey, see, <a 
 id="x1-26"></a>Aminikhanghahi and Cook, 2017); here, we used
kernel-based change point analysis with a linear kernel. The basic idea with this method is to
average all the values in the time series within a certain window of time immediately before
and after a given candidate change-point, and then to check if the difference between
these two means exceeds a certain threshold. If it does, a (local) change-point has been
detected. Table <a 
href="#x1-27r2">2<!--tex4ht:ref: tab:change-points --></a> shows the results, for the word2vec embeddings as well as the BERT
embeddings. We find that the only <span 
class="lmmi-10x-x-109">w</span><sub>T</sub> for which there is evidence of the presence of local
change-points across both models is &#8216;consciousness.&#8217; (Lucien had BERT generate two
different kinds of embedding, narrow word embeddings, for which the model considers a
relatively small window of tokens around each word, and broad usage embeddings, for which
the model considers a much larger window of tokens around each word [in this case,
128]).
   <div class="table">
                                                                                     
                                                                                     
<!--l. 135--><p class="indent" >   <hr class="float"><div class="float" 
>
                                                                                     
                                                                                     
<div class="tabular">
 <table id="TBL-3" class="tabular" 
 
><colgroup id="TBL-3-1g"><col 
id="TBL-3-1"><col 
id="TBL-3-2"><col 
id="TBL-3-3"><col 
id="TBL-3-4"></colgroup><tr  
 style="vertical-align:baseline;" id="TBL-3-1-"><td  style="white-space:nowrap; text-align:left;" id="TBL-3-1-1"  
class="td11"> Embedding  </td><td  style="white-space:nowrap; text-align:left;" id="TBL-3-1-2"  
class="td11"> <span 
class="lmmi-10x-x-109">w</span><sub>T</sub>               </td><td  style="white-space:nowrap; text-align:center;" id="TBL-3-1-3"  
class="td11"> Window  </td><td  style="white-space:normal; text-align:left;" id="TBL-3-1-4"  
class="td11">                <!--l. 139--><p class="noindent" >Change-points  </td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-3-2-"><td colspan="3" style="white-space:nowrap; text-align:left;" id="TBL-3-2-1"  
class="td11"></td>                               <div class="multicolumn"  style="white-space:nowrap; text-align:center;">word2vec</div>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-3-3-"><td  style="white-space:nowrap; text-align:left;" id="TBL-3-3-1"  
class="td11"> &#8212;               </td><td  style="white-space:nowrap; text-align:left;" id="TBL-3-3-2"  
class="td11"> consciousness  </td><td  style="white-space:nowrap; text-align:center;" id="TBL-3-3-3"  
class="td11">    4      </td><td  style="white-space:normal; text-align:left;" id="TBL-3-3-4"  
class="td11">                        <!--l. 143--><p class="noindent" >2000  </td></tr><tr  
 style="vertical-align:baseline;" id="TBL-3-4-"><td  style="white-space:nowrap; text-align:left;" id="TBL-3-4-1"  
class="td11"> &#8212; </td><td  style="white-space:nowrap; text-align:left;" id="TBL-3-4-2"  
class="td11"> consciousness </td><td  style="white-space:nowrap; text-align:center;" id="TBL-3-4-3"  
class="td11"> 5 </td><td  style="white-space:normal; text-align:left;" id="TBL-3-4-4"  
class="td11"> <!--l. 144--><p class="noindent" >1998</td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-3-5-"><td  style="white-space:nowrap; text-align:left;" id="TBL-3-5-1"  
class="td11"> &#8212;               </td><td  style="white-space:nowrap; text-align:left;" id="TBL-3-5-2"  
class="td11"> reference        </td><td  style="white-space:nowrap; text-align:center;" id="TBL-3-5-3"  
class="td11">    2      </td><td  style="white-space:normal; text-align:left;" id="TBL-3-5-4"  
class="td11">                        <!--l. 145--><p class="noindent" >1996  </td></tr><tr  
 style="vertical-align:baseline;" id="TBL-3-6-"><td  style="white-space:nowrap; text-align:left;" id="TBL-3-6-1"  
class="td11"> &#8212; </td><td  style="white-space:nowrap; text-align:left;" id="TBL-3-6-2"  
class="td11"> reference </td><td  style="white-space:nowrap; text-align:center;" id="TBL-3-6-3"  
class="td11"> 3 </td><td  style="white-space:normal; text-align:left;" id="TBL-3-6-4"  
class="td11"> <!--l. 146--><p class="noindent" >1996</td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-3-7-"><td  style="white-space:nowrap; text-align:left;" id="TBL-3-7-1"  
class="td11"> &#8212;               </td><td  style="white-space:nowrap; text-align:left;" id="TBL-3-7-2"  
class="td11"> reference        </td><td  style="white-space:nowrap; text-align:center;" id="TBL-3-7-3"  
class="td11">    4      </td><td  style="white-space:normal; text-align:left;" id="TBL-3-7-4"  
class="td11">                        <!--l. 147--><p class="noindent" >1997  </td></tr><tr  
 style="vertical-align:baseline;" id="TBL-3-8-"><td  style="white-space:nowrap; text-align:left;" id="TBL-3-8-1"  
class="td11"> &#8212; </td><td  style="white-space:nowrap; text-align:left;" id="TBL-3-8-2"  
class="td11"> reference </td><td  style="white-space:nowrap; text-align:center;" id="TBL-3-8-3"  
class="td11"> 5 </td><td  style="white-space:normal; text-align:left;" id="TBL-3-8-4"  
class="td11"> <!--l. 148--><p class="noindent" >1996</td>

</tr><tr  
 style="vertical-align:baseline;" id="TBL-3-9-"><td colspan="3" style="white-space:nowrap; text-align:left;" id="TBL-3-9-1"  
class="td11"></td>                                <div class="multicolumn"  style="white-space:nowrap; text-align:center;">BERT</div>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-3-10-"><td  style="white-space:nowrap; text-align:left;" id="TBL-3-10-1"  
class="td11"> broad          </td><td  style="white-space:nowrap; text-align:left;" id="TBL-3-10-2"  
class="td11"> consciousness  </td><td  style="white-space:nowrap; text-align:center;" id="TBL-3-10-3"  
class="td11">    2      </td><td  style="white-space:normal; text-align:left;" id="TBL-3-10-4"  
class="td11">                        <!--l. 152--><p class="noindent" >1993  </td></tr><tr  
 style="vertical-align:baseline;" id="TBL-3-11-"><td  style="white-space:nowrap; text-align:left;" id="TBL-3-11-1"  
class="td11"> broad </td><td  style="white-space:nowrap; text-align:left;" id="TBL-3-11-2"  
class="td11"> consciousness </td><td  style="white-space:nowrap; text-align:center;" id="TBL-3-11-3"  
class="td11"> 3 </td><td  style="white-space:normal; text-align:left;" id="TBL-3-11-4"  
class="td11"> <!--l. 153--><p class="noindent" >1992</td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-3-12-"><td  style="white-space:nowrap; text-align:left;" id="TBL-3-12-1"  
class="td11"> broad          </td><td  style="white-space:nowrap; text-align:left;" id="TBL-3-12-2"  
class="td11"> consciousness  </td><td  style="white-space:nowrap; text-align:center;" id="TBL-3-12-3"  
class="td11">    4      </td><td  style="white-space:normal; text-align:left;" id="TBL-3-12-4"  
class="td11">                        <!--l. 154--><p class="noindent" >1993  </td></tr><tr  
 style="vertical-align:baseline;" id="TBL-3-13-"><td  style="white-space:nowrap; text-align:left;" id="TBL-3-13-1"  
class="td11"> broad </td><td  style="white-space:nowrap; text-align:left;" id="TBL-3-13-2"  
class="td11"> consciousness </td><td  style="white-space:nowrap; text-align:center;" id="TBL-3-13-3"  
class="td11"> 5 </td><td  style="white-space:normal; text-align:left;" id="TBL-3-13-4"  
class="td11"> <!--l. 155--><p class="noindent" >1994</td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-3-14-"><td  style="white-space:nowrap; text-align:left;" id="TBL-3-14-1"  
class="td11"> narrow        </td><td  style="white-space:nowrap; text-align:left;" id="TBL-3-14-2"  
class="td11"> consciousness  </td><td  style="white-space:nowrap; text-align:center;" id="TBL-3-14-3"  
class="td11">    2      </td><td  style="white-space:normal; text-align:left;" id="TBL-3-14-4"  
class="td11">                        <!--l. 156--><p class="noindent" >1976,
                                     1977,
                                     1981,
                                     1983,
                                     1988,
                                     1991,
                                     1993,
                                     1994,
                                      1998  </td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-3-15-"><td  style="white-space:nowrap; text-align:left;" id="TBL-3-15-1"  
class="td11"> narrow        </td><td  style="white-space:nowrap; text-align:left;" id="TBL-3-15-2"  
class="td11"> consciousness  </td><td  style="white-space:nowrap; text-align:center;" id="TBL-3-15-3"  
class="td11">    3      </td><td  style="white-space:normal; text-align:left;" id="TBL-3-15-4"  
class="td11">                        <!--l. 157--><p class="noindent" >1976,
                                     1983,
                                     1987,
                                     1994,
                                      1997  </td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-3-16-"><td  style="white-space:nowrap; text-align:left;" id="TBL-3-16-1"  
class="td11"> narrow        </td><td  style="white-space:nowrap; text-align:left;" id="TBL-3-16-2"  
class="td11"> consciousness  </td><td  style="white-space:nowrap; text-align:center;" id="TBL-3-16-3"  
class="td11">    4      </td><td  style="white-space:normal; text-align:left;" id="TBL-3-16-4"  
class="td11">                        <!--l. 158--><p class="noindent" >1998  </td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-3-17-"><td  style="white-space:nowrap; text-align:left;" id="TBL-3-17-1"  
class="td11">            </td></tr></table>                                                                     </div>
<a 
 id="x1-27r2"></a>
<br />                                                                                     <div class="caption" 
><span class="id">
Table&#x00A0;2: </span><span  
class="content">Results of the change-point analysis.
</span></div><!--tex4ht:label?: x1-27r2 -->
                                                                                     
                                                                                     
   </div><hr class="endfloat" />
   </div>
<!--l. 165--><p class="indent" >   Next, we wanted to investigate the possible role of our target texts. Recall that we chose our
three <span 
class="lmmi-10x-x-109">w</span><sub>T</sub>s because each features prominently in a very influential book or article published
during the last 50 years that many see as having done much to change the concept in
question. To do so, we relied on the idea of a text&#8217;s <span 
class="ec-lmri-10x-x-109">disruptiveness </span>with respect to some
word&#8217;s meaning: when a text <span 
class="lmmi-10x-x-109">T </span>is disruptive with respect to a given word&#8217;s meaning, then
that word&#8217;s meaning will be tend to be more similar to its meaning in texts published
after <span 
class="lmmi-10x-x-109">T </span>(because <span 
class="lmmi-10x-x-109">T </span>had an influence on these texts) than to texts published before <span 
class="lmmi-10x-x-109">T</span>
(see, <a 
 id="x1-28"></a>Hogenbirk, 2023). To quantify disruptiveness, we defined a disruptiveness score
<span 
class="lmmi-10x-x-109">D</span>:
<!--l. 167--><p class="indent" >
<table 
class="align-star">
                   <tr><td 
class="align-odd"><span 
class="lmmi-10x-x-109">D</span><sub><span 
class="lmmi-8">T,w</span></sub> <span 
class="rm-lmr-10x-x-109">=</span></td>                   <td 
class="align-even"><img 
src="Blog_post_20240x.png" alt="--1--
nafter"  class="frac" align="middle"> <span 
class="lmex-10">&#x2211;</span>
      <sub><span 
class="lmmi-8">t</span><span 
class="lmsy8-">|</span><span 
class="lmmi-8">y</span><sub><span 
class="lmmi-6">T</span></sub><span 
class="rm-lmr-8">+</span><span 
class="lmmi-8">o</span><sub>after</sub><span 
class="lmmi-8">&#x003C;y</span><sub><span 
class="lmmi-6">t</span></sub><span 
class="lmsy8-">&#x2264;</span><span 
class="lmmi-8">y</span><sub><span 
class="lmmi-6">T</span></sub><span 
class="rm-lmr-8">+</span><span 
class="lmmi-8">o</span><sub>after</sub><span 
class="rm-lmr-8">+</span><span 
class="lmmi-8">r</span></sub> <span 
class="rm-lmr-10x-x-109">cos</span><span 
class="rm-lmr-10x-x-109">(</span><span 
class="lmmi-10x-x-109">w</span><sub><span 
class="lmmi-8">T</span> </sub><span 
class="lmmi-10x-x-109">,w</span><sub><span 
class="lmmi-8">t</span></sub><span 
class="rm-lmr-10x-x-109">)</span><span 
class="lmsy-10x-x-109">-</span></td>                     <td 
class="align-label"></td>                   <td 
class="align-label">
                   </td></tr><tr><td 
class="align-odd"></td>                          <td 
class="align-even"><img 
src="Blog_post_20241x.png" alt="--1---
nbefore"  class="frac" align="middle"> <span 
class="lmex-10">&#x2211;</span>
       <sub><span 
class="lmmi-8">t</span><span 
class="lmsy8-">|</span><span 
class="lmmi-8">y</span><sub><span 
class="lmmi-6">T</span></sub><span 
class="lmsy8-">-</span><span 
class="lmmi-8">o</span><sub>before</sub><span 
class="lmsy8-">-</span><span 
class="lmmi-8">r</span><span 
class="lmsy8-">&#x2264;</span><span 
class="lmmi-8">y</span><sub><span 
class="lmmi-6">t</span></sub><span 
class="lmmi-8">&#x003C;y</span><sub><span 
class="lmmi-6">T</span></sub><span 
class="lmsy8-">-</span><span 
class="lmmi-8">o</span><sub>before</sub></sub><span 
class="rm-lmr-10x-x-109">cos</span><span 
class="rm-lmr-10x-x-109">(</span><span 
class="lmmi-10x-x-109">w</span><sub><span 
class="lmmi-8">T</span> </sub><span 
class="lmmi-10x-x-109">,w</span><sub><span 
class="lmmi-8">t</span></sub><span 
class="rm-lmr-10x-x-109">)</span><span 
class="lmmi-10x-x-109">,</span></td>                   <td 
class="align-label"></td>                   <td 
class="align-label"></td></tr></table>
<!--l. 171--><p class="indent" >   with <span 
class="lmmi-10x-x-109">y</span><sub><span 
class="lmmi-8">i</span></sub> the year of text <span 
class="lmmi-10x-x-109">i</span>&#8217;s publication, <span 
class="lmmi-10x-x-109">o</span><sub>before</sub> and <span 
class="lmmi-10x-x-109">o</span><sub>after</sub> offsets (how many years immediately
before/after <span 
class="lmmi-10x-x-109">T </span>are not to be included in the calculation), <span 
class="lmmi-10x-x-109">r </span>the time window [how many years
before/after <span 
class="lmmi-10x-x-109">T </span>(minus/plus the offset) to include in the calculation], and <span 
class="lmmi-10x-x-109">n</span><sub>before</sub> and <span 
class="lmmi-10x-x-109">n</span><sub>after</sub> the
numbers of text published in <span 
class="lmmi-10x-x-109">r </span>before/after <span 
class="lmmi-10x-x-109">T</span>. The interpretation of this score is that if <span 
class="lmmi-10x-x-109">D &#x003E; </span><span 
class="rm-lmr-10x-x-109">0</span>, then
the target text <span 
class="lmmi-10x-x-109">T </span>was more similar to texts published after it than to texts before it (with respect to
the meaning of <span 
class="lmmi-10x-x-109">w</span>), and so it was disruptive.
<!--l. 173--><p class="indent" >   Figure <a 
href="#x1-29r3">3<!--tex4ht:ref: fig:d-score-ranking --></a> shows <span 
class="lmmi-10x-x-109">D</span>-score rankings for our three sub-corpora. None of the three target texts rank
near the top; in fact, their <span 
class="lmmi-10x-x-109">D</span>-scores are all negative. (The BERT embeddings yielded similar
results.) Hence, we did not find evidence that any of our targets text were unusually disruptive with
respect to their target words.
<!--l. 175--><p class="indent" >   <hr class="figure"><div class="figure" 
>
                                                                                     
                                                                                     
                                                                                     
                                                                                     
<!--l. 177--><p class="noindent" ><img 
src="figure2.png" alt="PIC"  
width="266" height="266" > <a 
 id="x1-29r3"></a>
<br />                                                                                     <div class="caption" 
><span class="id">
Figure&#x00A0;3: </span><span  
class="content">Ranking of <span 
class="lmmi-10x-x-109">D</span>-scores for each of our three sub-corpora (target text in red; <span 
class="lmmi-10x-x-109">o</span><sub>before</sub> <span 
class="rm-lmr-10x-x-109">=</span>
<span 
class="lmmi-10x-x-109">o</span><sub>after</sub> <span 
class="rm-lmr-10x-x-109">= 0</span>; <span 
class="lmmi-10x-x-109">r </span><span 
class="rm-lmr-10x-x-109">= 10</span>)                                                                   </span></div><!--tex4ht:label?: x1-29r3 -->
                                                                                     
                                                                                     
<!--l. 179--><p class="indent" >   </div><hr class="endfigure">
<!--l. 181--><p class="indent" >   <span 
class="lmmi-10x-x-109">D</span>-scores need not be constant over time. This means that even though our target texts
were not unusually disruptive globally, they may still have been unusually disruptive for
their time. To investigate this possibility, for each sub-corpus, I calculated the average
<span 
class="lmmi-10x-x-109">D</span>-score for each year and compared it with our target&#8217;s <span 
class="lmmi-10x-x-109">D</span>-score (Figure <a 
href="#x1-33r4">4<!--tex4ht:ref: fig:d-score-over-time --></a>). For <a 
 id="x1-30"></a>Clark and
Chalmers (1998) and <a 
 id="x1-31"></a>Kripke (1980), we see little evidence for <span 
class="lmmi-10x-x-109">D</span>-score fluctuations over
time. In contrast, in the case of <a 
 id="x1-32"></a>Chalmers (1996), Figure <a 
href="#x1-33r4">4<!--tex4ht:ref: fig:d-score-over-time --></a> shows a spike in the average
disruptiveness of articles with respect to consciousness around the time of that text&#8217;s publication.
Note, however, that we did not find this spike for the BERT embeddings; moreover, the
95% confidence intervals are such that our results are also consistent with no spike at
all.
<!--l. 183--><p class="indent" >   <hr class="figure"><div class="figure" 
>
                                                                                     
                                                                                     
                                                                                     
                                                                                     
<!--l. 185--><p class="noindent" ><img 
src="figure3.png" alt="PIC"  
width="332" height="332" > <a 
 id="x1-33r4"></a>
<br />                                                                                     <div class="caption" 
><span class="id">
Figure&#x00A0;4: </span><span  
class="content">Average <span 
class="lmmi-10x-x-109">D</span>-scores over time for each of our three sub-corpora (target text in red;
<span 
class="lmmi-10x-x-109">o</span><sub>before</sub> <span 
class="rm-lmr-10x-x-109">= </span><span 
class="lmmi-10x-x-109">o</span><sub>after</sub> <span 
class="rm-lmr-10x-x-109">= 0</span>; <span 
class="lmmi-10x-x-109">r </span><span 
class="rm-lmr-10x-x-109">= 10</span>); errorbars show 95% confidence intervals.                    </span></div><!--tex4ht:label?: x1-33r4 -->
                                                                                     
                                                                                     
<!--l. 187--><p class="indent" >   </div><hr class="endfigure">
<!--l. 189--><p class="indent" >   So far, I have used <span 
class="lmmi-10x-x-109">o</span><sub>before</sub> <span 
class="rm-lmr-10x-x-109">= </span><span 
class="lmmi-10x-x-109">o</span><sub>after</sub> <span 
class="rm-lmr-10x-x-109">= 0 </span>and <span 
class="lmmi-10x-x-109">r </span><span 
class="rm-lmr-10x-x-109">= 10</span>. Perhaps it takes longer than 10 years for a
text&#8217;s disruptiveness to be felt in the relevant literature. To investigate this, I re-calculated the
<span 
class="lmmi-10x-x-109">D</span>-scores using a range of different offsets <span 
class="lmmi-10x-x-109">o</span><sub>after</sub>. Note that the maximum possible value of <span 
class="lmmi-10x-x-109">o</span><sub>after</sub>
depends on a text&#8217;s year of publication. Figure <a 
href="#x1-34r5">5<!--tex4ht:ref: fig:different-offsets --></a> shows the results. The figure suggests that the
choice of <span 
class="lmmi-10x-x-109">o</span><sub>after</sub> does not have a major impact.
<!--l. 191--><p class="indent" >   <hr class="figure"><div class="figure" 
>
                                                                                     
                                                                                     
                                                                                     
                                                                                     
<!--l. 193--><p class="noindent" ><img 
src="figure4.png" alt="PIC"  
width="332" height="332" > <a 
 id="x1-34r5"></a>
<br />                                                                                     <div class="caption" 
><span class="id">
Figure&#x00A0;5: </span><span  
class="content"><span 
class="lmmi-10x-x-109">D</span>-scores for different values of <span 
class="lmmi-10x-x-109">o</span><sub>after</sub> (<span 
class="lmmi-10x-x-109">r </span><span 
class="rm-lmr-10x-x-109">= 10</span>; target texts in red; average <span 
class="lmmi-10x-x-109">D</span>-score
in black).                                                                            </span></div><!--tex4ht:label?: x1-34r5 -->
                                                                                     
                                                                                     
<!--l. 195--><p class="indent" >   </div><hr class="endfigure">
<!--l. 197--><p class="indent" >   Are there examples of articles or books in the philosophical literature that have caused
significant conceptual change in the recent history of analytic philosophy? Of the three
candidate examples we investigated (belief; consciousness; reference), only consciousness
showed robust evidence of semantic change. After mapping the semantic similarity of
&#8216;consciousness&#8217; in a suitable corpus of philosophy articles published since 1971 over time, we
detected the presence of local change-points for embeddings generated using two different
methods (word2vec, BERT). However, even though many of these change-points lay
roughly in the neighbourhood of the publication of <a 
 id="x1-35"></a>Chalmers (1996), the results of our
<span 
class="lmmi-10x-x-109">D</span>-score analysis do not suggest that Chalmers (1996) itself was unusually disruptive with
respect to the meaning of &#8216;consciousness&#8217;. Our results, then, do not support the idea that
any of our three target texts caused substantial conceptual change in the philosophical
literature.
<!--l. 199--><p class="indent" >   To end, I want to briefly describe two of the main problems that ultimately lead me to not want
to pursue the project further. The first is practical. Our corpus consisted of articles published in or
after 1971. This meant that we were limited to target texts published after 1971. Yet most of
the target texts that we (and others) thought worth investigating (e.g., <a 
 id="x1-36"></a>Tarski, 1936;
<a 
 id="x1-37"></a>Gettier, 1963; <a 
 id="x1-38"></a>Carnap, 1936) were published (long) before 1971. In addition, two of our
target text were published in the second half of the 1990s, meaning that we only had
<span 
class="lmsy-10x-x-109">~</span>25 years worth of data to investigate&#8212;conceptual change might take longer than that,
however. The problem is that the further back into the past one wants to go, the more
difficult and labour-intensive it becomes to assemble a corpus of sufficient quality: generally,
the older a document, the more annoying it is going to be to convert it into clean plain
text.
<!--l. 201--><p class="indent" >   The second problem is a fundamental methodological problem. To be persuaded that our
methods do what we want them to do, we&#8217;d (minimally) need a set of examples for which we are
<span 
class="ec-lmri-10x-x-109">reasonably certain </span>that they have undergone conceptual change to calibrate these methods against.
While some studies have attempted this sort of calibration in the past (e.g., <a 
 id="x1-39"></a>Martinc
et al., 2020), our corpus consisted of philosophy publications&#8212;not a discipline particularly
known for its plain or ordinary use of English. This makes it doubtful that these previous
results (which are, in my opinion, not that overwhelming to begin with) generalize to our
corpus. Instead, what we would have needed are clear-cut examples of conceptual change
<span 
class="ec-lmri-10x-x-109">specifically </span>in the philosophical literature (ideally, in the last 50 years or so). Yet the
sense I got while working on this project is that such examples might be impossible to
find. When we presented the material, I cannot remember a single example of a concept
for which everyone in the room agreed that it had undergone substantial change: not
among our chosen examples, nor among any of the many alternative examples people
suggested to us. In light of this, it felt a bit pointless to pour lots more time and effort into
the project, given that fundamental methodological doubts would likely have always
remained.
   <h3 class="sectionHead"><a 
 id="x1-1000"></a>References</h3>
<!--l. 203--><p class="noindent" >
       <dl class="thebibliography"><dt id="X0-aminikhanghahiSurveyMethodsTime2017" class="thebibliography">
</dt><dd 
id="bib-1" class="thebibliography">
       <!--l. 203--><p class="noindent" >Aminikhanghahi,  S.,  &amp;  Cook,  D.&#x00A0;J.  (2017).  A  survey  of  methods  for  time  series
       change  point  detection.  <span 
class="ec-lmri-10x-x-109">Knowledge  and  Information  Systems</span>,  <span 
class="ec-lmri-10x-x-109">51</span>(2),  339&#8211;367.
       https://doi.org/10.1007/s10115-016-0987-z
                                                                                     
                                                                                     
       </dd><dt id="X0-carnapTestabilityMeaning1936" class="thebibliography">
</dt><dd 
id="bib-2" class="thebibliography">
       <!--l. 203--><p class="noindent" >Carnap, R. (1936). Testability and Meaning. <span 
class="ec-lmri-10x-x-109">Philosophy of Science</span>, <span 
class="ec-lmri-10x-x-109">3</span>(4), 419&#8211;471.
       </dd><dt id="X0-chalmersConsciousMindSearch1996" class="thebibliography">
</dt><dd 
id="bib-3" class="thebibliography">
       <!--l. 203--><p class="noindent" >Chalmers, D.&#x00A0;J. (1996). <span 
class="ec-lmri-10x-x-109">The Conscious Mind: In Search of a Fundamental Theory</span>.
       Oxford University Press.
       </dd><dt id="X0-chalmersWhatConceptualEngineering2020" class="thebibliography">
</dt><dd 
id="bib-4" class="thebibliography">
       <!--l. 203--><p class="noindent" >Chalmers,  D.&#x00A0;J.  (2020).  What  is  conceptual  engineering  and  what  should  it  be?
       <span 
class="ec-lmri-10x-x-109">Inquiry</span>, 1&#8211;18. https://doi.org/10.1080/0020174X.2020.1817141
       </dd><dt id="X0-clarkExtendedMind1998" class="thebibliography">
</dt><dd 
id="bib-5" class="thebibliography">
       <!--l. 203--><p class="noindent" >Clark,  A.,  &amp;  Chalmers,  D.  (1998).  The  Extended  Mind.  <span 
class="ec-lmri-10x-x-109">Analysis</span>,  <span 
class="ec-lmri-10x-x-109">58</span>(1),  7&#8211;19.
       https://doi.org/10.1111/1467-8284.00096
       </dd><dt id="X0-devlinBERTPretrainingDeep2019" class="thebibliography">
</dt><dd 
id="bib-6" class="thebibliography">
       <!--l. 203--><p class="noindent" >Devlin,              J.,              Chang,              M.-W.,              Lee,              K.,
       &amp; Toutanova, K. (2019). BERT: Pre-training of Deep Bidirectional Transformers for
       Language Understanding. https://doi.org/10.48550/arXiv.1810.04805
       </dd><dt id="X0-dubossarskyTimeOutTemporalReferencing2019" class="thebibliography">
</dt><dd 
id="bib-7" class="thebibliography">
       <!--l. 203--><p class="noindent" >Dubossarsky, H., Hengchen, S., Tahmasebi, N., &amp; Schlechtweg, D. (2019). Time-Out:
       Temporal Referencing for Robust Modeling of Lexical Semantic Change. <span 
class="ec-lmri-10x-x-109">Proceedings</span>
       <span 
class="ec-lmri-10x-x-109">of the 57th Annual Meeting of the Association for Computational Linguistics</span>, 457&#8211;470.
       https://doi.org/10.18653/v1/P19-1044
       </dd><dt id="X0-gettierJustifiedTrueBelief1963" class="thebibliography">
</dt><dd 
id="bib-8" class="thebibliography">
       <!--l. 203--><p class="noindent" >Gettier, E.&#x00A0;L. (1963). Is justified true belief knowledge? <span 
class="ec-lmri-10x-x-109">Analysis</span>, <span 
class="ec-lmri-10x-x-109">23</span>(6), 121&#8211;123.
       </dd><dt id="X0-hengchenChallengesComputationalLexical2021" class="thebibliography">
</dt><dd 
id="bib-9" class="thebibliography">
       <!--l. 203--><p class="noindent" >Hengchen, S., Tahmasebi, N., Schlechtweg, D., &amp; Dubossarsky, H. (2021). Challenges
       for computational lexical semantic change. In N. Tahmasebi, L. Borin, A. Jatowt,
       Y.  Xu,  &amp;  S.  Hengchen  (Eds.),  <span 
class="ec-lmri-10x-x-109">Computational  approaches  to  semantic  change</span>
       (pp.&#x00A0;341&#8211;372). Zenodo. https://doi.org/10.5281/ZENODO.5040241
       </dd><dt id="X0-hogenbirkEachBookIts2023" class="thebibliography">
</dt><dd 
id="bib-10" class="thebibliography">
       <!--l. 203--><p class="noindent" >Hogenbirk, H.&#x00A0;D. (2023). <span 
class="ec-lmri-10x-x-109">Each book its own Babel: Conceptual unity and disunity in</span>
       <span 
class="ec-lmri-10x-x-109">early      modern      natural      philosophy</span>.       University       of       Groningen.
       https://doi.org/10.33612/diss.849175103
       </dd><dt id="X0-kripkeNamingNecessity1980" class="thebibliography">
</dt><dd 
id="bib-11" class="thebibliography">
       <!--l. 203--><p class="noindent" >Kripke, S.&#x00A0;A. (1980). <span 
class="ec-lmri-10x-x-109">Naming and necessity</span>. Harvard University Press.
       </dd><dt id="X0-leiterBestGeneralPhilosophy2022" class="thebibliography">
</dt><dd 
id="bib-12" class="thebibliography">
       <!--l. 203--><p class="noindent" >Leiter, B. (2022). Best &#8217;general&#8217; philosophy journals, 2022.
       </dd><dt id="X0-martincCapturingEvolutionWord2020" class="thebibliography">
</dt><dd 
id="bib-13" class="thebibliography">
                                                                                     
                                                                                     
       <!--l. 203--><p class="noindent" >Martinc, M., Montariol, S., Zosa, E., &amp; Pivovarova, L. (2020). Capturing Evolution in
       Word Usage: Just Add More Clusters? <span 
class="ec-lmri-10x-x-109">Companion Proceedings of the Web Conference</span>
       <span 
class="ec-lmri-10x-x-109">2020</span>, 343&#8211;349. https://doi.org/10.1145/3366424.3382186
       </dd><dt id="X0-mikolovEfficientEstimationWord2013" class="thebibliography">
</dt><dd 
id="bib-14" class="thebibliography">
       <!--l. 203--><p class="noindent" >Mikolov, T., Chen, K., Corrado, G., &amp; Dean, J. (2013). Efficient Estimation of Word
       Representations in Vector Space. https://doi.org/10.48550/arXiv.1301.3781
       </dd><dt id="X0-recchiaTracingShiftingConceptual2017" class="thebibliography">
</dt><dd 
id="bib-15" class="thebibliography">
       <!--l. 203--><p class="noindent" >Recchia,  G.,  Jones,  E.,  Nulty,  P.,  Regan,  J.,  &amp;  De  Bolla,  P.  (2017).  Tracing
       Shifting  Conceptual  Vocabularies  Through  Time.  In  P.  Ciancarini,  F.  Poggi,  M.
       Horridge,  J.  Zhao,  T.  Groza,  M.&#x00A0;C.  Suarez-Figueroa,  M.  d&#8217;Aquin,  &amp;  V.  Presutti
       (Eds.), <span 
class="ec-lmri-10x-x-109">Knowledge Engineering and Knowledge Management </span>(pp.&#x00A0;19&#8211;28, Vol.&#x00A0;10180).
       Springer International Publishing. https://doi.org/10.1007/978-3-319-58694-6_2
       </dd><dt id="X0-tahmasebiSurveyComputationalApproaches2019" class="thebibliography">
</dt><dd 
id="bib-16" class="thebibliography">
       <!--l. 203--><p class="noindent" >Tahmasebi, N., Borin, L., &amp; Jatowt, A. (2019). Survey of Computational Approaches
       to Lexical Semantic Change. https://doi.org/10.48550/arXiv.1811.06278
       </dd><dt id="X0-tarskiWahrheitsbegriffFormalisiertenSprachen1936" class="thebibliography">
</dt><dd 
id="bib-17" class="thebibliography">
       <!--l. 203--><p class="noindent" >Tarski,  A.  (1936).  Der  Wahrheitsbegriff  in  den  Formalisierten  Sprachen.  <span 
class="ec-lmri-10x-x-109">Studia</span>
       <span 
class="ec-lmri-10x-x-109">Philosophica</span>, <span 
class="ec-lmri-10x-x-109">1</span>, 261&#8211;405.</dd></dl>
