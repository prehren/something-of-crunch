---
title: "Measuring Conceptual Change in Philosophy: A Corpus Study"
date: 2025-01-01
---
Last year, together with two collaborators (Lucien Baumgartner; Krzysztof S&#281;kowski), I worked on a 
project that aimed to track the semantic disruptiveness of influential philosophy publications. We
presented the material a couple of times, but ultimately decided that the project was not worth
pursuing. Still, I thought the research was interesting enough methodologically to merit some sort of
write up. That&#8217;s what this post is (though I&#8217;m mostly going to focus on the parts that I
contributed).

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
