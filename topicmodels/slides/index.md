##   {#section .hideslideheader data-background="#061C30"}

::: {style="display:table;width:100%;table-layout: fixed;"}
::: {.title-without-logo style="display:table-cell;width:100%;padding-right:3%;padding-left:3%;vertical-align:middle;"}
SRC 2024/25 PhD course 'Data Science for Sustainable Development'

Structural Topic Modeling with R

 

 

 

 
:::
:::

::: {style="display:table;width:100%;table-layout: fixed;"}
::: {.mytitlepage .linksection style="display:table-cell;width:30%;padding-left:3%;vertical-align:bottom;"}
*<https://scitingly.net/>*

*<stefan.daume@su.se>*
:::

::: {.mytitlepage .authorsection style="display:table-cell;width:70%;padding-right:3%;"}
  **Stefan Daume**

*[Stockholm Resilience Centre, Stockholm
University](https://www.stockholmresilience.org/meet-our-team/staff/2021-01-27-daume.html)*

& *[Beijer Institute of Ecological
Economics](https://beijer.kva.se/programmes/complexity/)*

 

*11. April 2025*
:::
:::

# Topic modeling: "Text as data"

## The notion of "latent topics"

Topic modeling applies **unsupervised probabilistic classification** to
identify the **latent** ("hidden") topics in a collection of documents.

```{=html}
<aside class="notes">
```
-   requires document collections!
-   topics are defined as collections of words

```{=html}
</aside>
```
## Supervised vs unsupervised learning/classification

Key difference: supervised learning requires **labelled** training data

```{=html}
<aside class="notes">
```
-   Key takeaway: this has substantial practical and economical
    implications for research (different efforts, costs, teams)
-   add examples of effort processes

```{=html}
</aside>
```
## Why topic modeling?

-   summarize large text collections
-   discover "latent" topics
-   text-based (causal) inferences and testing social science theories

# Examples

## Long-term trends in climate change reports

A topography of climate change research [@CallaghanMinx_et_2020_NCC_10]

-   more than 400.000 climate change publications analysed
-   over-representation of social sciences are in recent assessment
    reports
-   demand of more solution-oriented research

## Corporate sustainability reporting

Analysis of 9,500 corporate sustainability reports (published 1999 to
2015) [@SzekelyBrocke_2017_PO_12]:

-   reports cover environmental, social, and economic sustainability
-   economic sustainability is of increasing importance
-   environmental sustainability is focused on emissions and energy
-   biodiversity receives little attention

```{=html}
<aside class="notes">
```
-   sustainability reports published between 1999 and 2015 for our
    study. We retrieved the PDF documents from the GRI website
    (<http://database.globalreporting.org/search>)

```{=html}
</aside>
```
## Climate communication

-   **topic modeling** of **organizational climate communication** to
    identify **impact of corporate funding** on climate polarization
    [@Farell_2016_PNAS_113]

```{=html}
<aside class="notes">
```
-   the last example is based on text and illustrates the use of the
    method we will focus on today

```{=html}
</aside>
```
## Perception and communication of policies

Analysis of open-ended survey responses asking why carbon taxes are
unfair [@PovitkinaCarlssonJagers_et_2021_GEC_70]:

-   impact of demographic factors on perceptions of fairness
-   implications for policy design

```{=html}
<aside class="notes">
```
-   Why are carbon taxes unfair? Disentangling public perceptions of
    fairness

-   mention that this (open-ended survey responses) is also the original
    usecase for STM

-   **several usecases that might relate to your own research and give
    an indication where topic models may be useful**

-   **also the reason we chose this techniques because we all deal with
    text in one way or another**

```{=html}
</aside>
```
# Topic modeling algorithm

## How does it work?

Generative model that reverses the assumed document generation process.

## Generative model {#generative-model .xs-small-pg-text}

`<img src="images/topic_modelling_explained.jpg" width="60%" />`{=html}

Illustration of the topic modeling process
([@DaumeAlbertEt2014_FORESTECOSYST_1] (adapted from
[@Blei2012_COMMACM_55])).

## Topic modelling algorithms

-   LSA - [Latent semantic
    analysis](https://asistdl.onlinelibrary.wiley.com/doi/10.1002/(SICI)1097-4571(199009)41:6%3C391::AID-ASI1%3E3.0.CO;2-9)
-   LDA - Latent dirichlet allocation [@BleiNgEt2003_JMLR_3]
-   CTM - Correlated topic model [@BleiLafferty2007_AAS_1]
-   STM - Structural topic model [@RobertsStewart_et_2019_JSTATS_91]

## STM vs "vanilla LDA"

-   STM extends CTM (i.e. assumes that topics are correlated)
-   STM can incorporate arbitrary document meta-data into the topic
    model

## Basic text mining concepts

-   documents
-   corpus
-   tokens
-   terms

## Basic Topic modeling steps

1.  get documents to analyse
2.  preprocess
3.  create a corpus
4.  tokenize
5.  create document-term/feature matrix
6.  *(evaluate alternative topic numbers)*
7.  decide on K, the number of topics, and fit a topic model
8.  *(validate semantic integrity of the topic model)*
9.  test impact of document meta-data on topics

## R packages to use

-   quanteda
-   tidytext
-   (snowballc)
-   (spacyr)
-   stringr
-   stm

# Structural topic modeling applied

## A Topic model of Covid preprints

The following slides step through a detailed example of fitting a topic
model to preprints on [bioRxiv](https://www.biorxiv.org/) and
[medRxiv](https://www.medrxiv.org/) related to *Covid-19*.

R code and detailed examples are available here:

-   **Code**: <https://github.com/sdaume/srcquantcourse>
-   **Documentation**: <https://sdaume.github.io/srcquantcourse>

## Motivation

-   understand prevalent topics in preprints from
    [bioRxiv](https://www.biorxiv.org/) and
    [medRxiv](https://www.medrxiv.org/)
-   explore the effect of document metadata (covariates), such as:
    -   Which preprint server it was published on?
    -   When it was published?
    -   If it has been published after peer review?

## Getting data

Preprint data on [bioRxiv](https://www.biorxiv.org/) and
[medRxiv](https://www.medrxiv.org/) can be retrieved via a **public
API** with the help of the
[`medrxivr`](https://docs.ropensci.org/medrxivr/) R package.

## Preparing preprint metadata

``` r
library(dplyr)
library(medrxivr)

# get publications from medRxiv and bioRxiv
pubs_biorxiv_raw <- medrxivr::mx_api_content(server = "biorxiv",
                                             #from_date = "2019-01-01",
                                             to_date = "2023-12-31")

pubs_medrxiv_raw <- medrxivr::mx_api_content(server = "medrxiv",
                                             #from_date = "2019-01-01",
                                             to_date = "2023-12-31")

pubs_biorxiv_raw <- pubs_biorxiv_raw %>%
  mutate(server = "biorxiv")

pubs_medrxiv_raw <- pubs_medrxiv_raw %>%
  mutate(server = "medrxiv")

preprints_raw <- dplyr::bind_rows(pubs_biorxiv_raw, pubs_medrxiv_raw)

save(preprints_raw, file = "./data-raw/preprints_raw.Rdata")
```

## Preprint metadata

    glimpse(preprints_raw)

    Rows: 365,526
    Columns: 16
    $ doi                              <chr> "10.1101/001891", "10.1101/001867", "10.1101…
    $ title                            <chr> "Population genomics of Saccharomyces cerevi…
    $ authors                          <chr> "Carlotta De Filippo;Monica Di Paola;Irene S…
    $ author_corresponding             <chr> "Duccio  Cavalieri", "David  Morrison", "Dav…
    $ author_corresponding_institution <chr> "Fondazione E. Mach (FEM)", "Swedish Univers…
    $ date                             <chr> "2014-01-17", "2014-01-17", "2014-01-17", "2…
    $ version                          <chr> "1", "1", "1", "2", "1", "1", "1", "1", "2",…
    $ license                          <chr> "cc_by_nc_nd", "cc_by_nc", "cc_by_nc", "cc_b…
    $ category                         <chr> "Evolutionary Biology ", "Ecology ", "Molecu…
    $ jatsxml                          <chr> "https://www.biorxiv.org/content/early/2014/…
    $ abstract                         <chr> "The quest for the ecological niches of Sacc…
    $ published                        <chr> "NA", "NA", "NA", "NA", "10.1093/bioinformat…
    $ node                             <int> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 1…
    $ link_page                        <chr> "https://www.biorxiv.org/content/10.1101/001…
    $ link_pdf                         <chr> "https://www.biorxiv.org/content/10.1101/001…
    $ server                           <chr> "biorxiv", "biorxiv", "biorxiv", "biorxiv", …

## Cleaning, filtering and annotating

``` r
library(dplyr)

preprints_cleaned <- preprints_raw %>%
  group_by(doi) %>%
  filter(version == max(version)) %>%
  ungroup() %>%
  distinct(doi, .keep_all = TRUE)
```

## Cleaning, filtering and annotating

``` r
preprints <- preprints_cleaned %>%
  mutate(published = stringr::str_trim(published)) %>%
  mutate(published = na_if(published, "NA")) %>%
  mutate(is_published = as.numeric(!is.na(published))) %>%
  mutate(is_published = case_when(is_published == 1 ~ "published",
                                  is_published == 0 ~ "not published",
                                  TRUE ~ "undefined")) %>%
  mutate(year = lubridate::year(date)) %>%
  filter(year >= 2020 & year <= 2023) %>% 
  select(doi, server, title, abstract, date, year, version, is_published)
```

## Cleaning, filtering and annotating

``` r
library(stringr)

keywords <- c("sars-cov", "covid")

search_pattern <- stringr::regex(paste(keywords, collapse = "|"), 
                                 ignore_case = TRUE)

covid_preprints <- preprints %>%
  filter(stringr::str_detect(title, pattern = search_pattern) |
           stringr::str_detect(abstract, pattern = search_pattern))
```

## Preprocessing the documents for text analysis

From text to data:

-   create a corpus
-   tokenize and preprocess
-   create a document-feature matrix

## Preprocessing the documents for text analysis

Text preprocessing choices could strongly influence the results of a
text analysis!

 

Choices need to be:

-   thoroughly explained,
-   carefully evaluated and
-   ideally be based on theory (see [@DennySpirling_2018_PA_26])

## Create a corpus

``` r
library(quanteda)

pubs_corpus <- covid_preprints %>%
  quanteda::corpus(docid_field = "doi", text_field = "abstract")

# pubs_corpus
# Corpus consisting of 29,692 documents and 6 docvars.
```

```{=html}
<aside class="notes">
```
First, we create a **corpus** object from the dataframe of preprints.
The corpus is essentially a library of documents that will be used for
the next steps. It specifies which variable should be used to uniquely
identify documents and which variable holds the textual content (here
the preprint *abstracts*) that should be processed.

Echoing the corpus will provide some basic information. All other
variables in the original dataframe will be interpreted and included as
document metadata (*'docvars'*), which could later be included in the
STM topic modelling process.
```{=html}
</aside>
```
## Tokenize and preprocess

``` r
pubs_tokens <- pubs_corpus %>%
  quanteda::tokens(remove_punct = TRUE,
                   remove_symbols = TRUE,
                   remove_numbers = TRUE,
                   remove_url = TRUE,
                   remove_separators = TRUE,
                   split_hyphens = TRUE) 
```

```{=html}
<aside class="notes">
```
For further analysis the corpus documents have to be **tokenized**,
i.e. further processing the texts have to be broken into semantic units
that are relevant for our analysis. The most common approach is to
interpret each *word* (typically designated by whitespaces or
punctuation) as a token. This is applied here as well. `quanteda` offers
several alternative approaches. Instead of individual words, sequences
of words (*n-grams*) could for example be used.

The tokenization method also provides several options for preprocessing
and filtering the tokens. Here for example, while tokenizing, we will
simultaneously remove punctuation, numbers, special symbols and URLs.
Furthermore, we split words containing hyphens, a word like
*social-ecological* will thus be split into two individual tokens
(*social* and *ecological*).

The text preprocessing choices could strongly influence the results of a
text analysis and should be thoroughly explained, carefully evaluated
and ideally be based on theory (see [@DennySpirling_2018_PA_26]).
```{=html}
</aside>
```
## Create a Document-feature matrix

``` r
pubs_dfm <- pubs_tokens %>%
  quanteda::dfm()
```

```{=html}
<aside class="notes">
```
The **tokens** object is then used to create a *document-feature
matrix*. For further statistical analysis this reduces the tokens to a
matrix of documents (rows) and unique **terms** (columns) that counts
the number of occurrences for each term in each document. `quanteda`
captures this as *features* which supports more general options than
**terms** (see the `quanteda` documentation for details).
```{=html}
</aside>
```
## Filter terms and documents

``` r
pubs_dfm <- pubs_dfm %>%
  quanteda::dfm_remove(pattern = quanteda::stopwords("english")) #%>%
  #quanteda::dfm_wordstem()
```

    # echo the result
    > pubs_dfm

    Document-feature matrix of: 29,692 documents, 82,472 features (99.87% sparse) and 6 docvars.
                    features
    docs             nitric oxide synthesised three isoforms synthases viz nnos neurons enos
      10.1101/038398      6     6           1     1        1         1   1    1       2    1
      10.1101/058511      0     0           0     0        0         0   0    0       0    0
      10.1101/292979      0     0           0     2        0         0   0    0       0    0
      10.1101/402370      0     0           0     0        0         0   0    0       0    0
      10.1101/420737      0     0           0     0        0         0   0    0       0    0
      10.1101/596700      0     0           0     0        0         0   0    0       0    0
    [ reached max_ndoc ... 29,686 more documents, reached max_nfeat ... 82,462 more features ]

```{=html}
<aside class="notes">
```
This is followed by other (optional) processing and filtering steps. A
common option for example --- to reduce the size of the data or assist
in the interpretation --- is the removal of so-called **stopwords**
(e.g. *"the", "and", "or"* etc).

A step omitted here is reducing words (terms) to their word stem. The
stemming algorithm (several are available) reduces words to its word
stem. The terms "universal", "university" and "universe" would for
example be reduced to the same word stem of "univers"; this example
indicates that this approach may require careful consideration.

Stemming has the advantage that it could potentially reduce the size of
the matrix substantially.
```{=html}
</aside>
```
## Stemming

*"Stemming"* will reduce the matrix, but could result in loosing
semantic information.

For example: **"universal"**, **"university"** and **"universe"** all
have the stem **"univers"**!

## More filtering

``` r
pubs_dfm <- pubs_dfm %>%
  quanteda::dfm_remove(min_nchar = 2) %>%
  quanteda::dfm_trim(min_docfreq = 2, docfreq_type = "count") %>%
  quanteda::dfm_subset(quanteda::ntoken(.) > 4)
```

    # echo the result
    > pubs_dfm

    Document-feature matrix of: 29,691 documents, 37,093 features (99.72% sparse) and 6 docvars.
                    features
    docs             nitric oxide synthesised three isoforms synthases viz neurons enos endothelial
      10.1101/038398      6     6           1     1        1         1   1       2    1           2
      10.1101/058511      0     0           0     0        0         0   0       0    0           0
      10.1101/292979      0     0           0     2        0         0   0       0    0           0
      10.1101/402370      0     0           0     0        0         0   0       0    0           0
      10.1101/420737      0     0           0     0        0         0   0       0    0           0
      10.1101/596700      0     0           0     0        0         0   0       0    0           0
    [ reached max_ndoc ... 29,685 more documents, reached max_nfeat ... 37,083 more features ]

```{=html}
<aside class="notes">
```
Further options may be considered to reduce noise and/or the size of the
matrix. The following code removes for example terms (or features) that
consist only of one character, terms that do not appear in at least two
different documents, and furthermore would remove documents that do not
contain at least 5 tokens. In our example this drops one document and
reduces the number of retained features by more than half.
```{=html}
</aside>
```
## Fitting the STM topic model

``` r
library(stm)

covid_stm_docs <- quanteda::convert(pubs_dfm, to = "stm")

covid_model_K20 <- stm(documents = covid_stm_docs$documents,
                       vocab = covid_stm_docs$vocab,
                       data = covid_stm_docs$meta,
                       prevalence = ~ server * s(year),
                       K = 20,
                       verbose = TRUE,
                       seed = 9868467)
```

```{=html}
<aside class="notes">
```
The key input to any topic modelling algorithm is the number of topics
(`K`) that the model should be fit to, which we here set to 20 (see the
separate document for a discussion on suitable choices for the number of
topics).

Before fitting the topic model we convert the document-feature matrix
into the native STM format. In order to fit a topic model with the
`stm()` function we need the set of `documents`, the `vocabulary` of
which these documents are composed and a dataframe specifying the values
of all document meta-data variables (`data`) which can be used in the
process as "covariates" that might influence the prevalence of topics in
a document.

In the example below, we ask `stm` to incorporate the origin of the
document (`server`) and the publication `year` when fitting the topic
model. The argument `prevalence = ~ server * s(year)` expresses that we
assume that the prevalence of topics in a document is influenced by
these two variables, and that they also interact, i.e. we work with the
hypothesis that different temporal trends could be expected for
documents published on either of the two preprint servers[^1].

The consideration of covariates is optional. If omitted the model
reduces to a *Correlated Topic Model*
[@BleiLafferty2007_AAS_1; @RobertsStewart_et_2019_JSTATS_91].

We also supply a `seed`, which allows to replicate the results of the
topic modeling.
```{=html}
</aside>
```
## Choosing 'K'

`<img src="figures/unnamed-chunk-12-1.png" width="80%" />`{=html}

## Choosing 'K'

`<img src="figures/unnamed-chunk-13-1.png" width="80%" />`{=html}

## Estimating the effect of document covariates

``` r
covid_effect_K20 <- estimateEffect(1:20 ~ server * s(year),
                                   stmobj = covid_model_K20,
                                   metadata = covid_stm_docs$meta)
```

```{=html}
<aside class="notes">
```
Once the model has converged we can estimate the effect of document
covariates on the topic prevalence. The `estimateEffect()` function
allows to run regressions based on the formula specified as the first
argument. It is here identical to the formula used when fitting the
topic model, and regressions are run for all 20 topics. The same
metadata as used previously needs to be supplied for this function in
addition to the topic model object.

This concludes fitting the model. The following sections step through a
sample exploration of this topic model.
```{=html}
</aside>
```
## Basic topic model information

``` r

plot(covid_model_K20, n = 5)
```

`<img src="figures/unnamed-chunk-15-1.png" width="70%" />`{=html}

```{=html}
<aside class="notes">
```
The topic model is defined by two matrices that capture probability
distributions of topics over documents (*gamma* matrix) and words (or
terms) over topics (*beta* matrix). We can start exploring these with
some of the built-in functions of `stm`.

The `plot()` function plots a chart showing topic proportions for all
topics in the model. A topic is identified by a unique ID (1-20) and in
the plot below the five words (or terms) that have the highest
probability of being associated with the given topic. This gives an
early indication of the distinct latent topics in the analysed subset of
preprints.
```{=html}
</aside>
```
## Topic words

``` r
summary(covid_model_K20)
># A topic model with 20 topics, 29691 documents and a 37093 word dictionary.
># Topic 1 Top Words:
>#       Highest Prob: model, can, covid, transmission, epidemic, data, disease 
>#       FREX: npis, mathematical, compartmental, scenarios, seir, reproduction, sir 
>#       Lift: 1we, abms, ao_scplowbstractc_scplowas, apt, artefact, asilv, asymptotically 
>#       Score: distancing, social, epidemic, reproduction, npis, model, r0 
># Topic 2 Top Words:
>#       Highest Prob: cov, sars, drug, antiviral, activity, drugs, covid 
>#       FREX: src, figdir, o_linksmallfig, c_fig, m_fig, o_fig, gif 
>#       Lift: k777, gif, pmmov, wwtps, 13k, 17k, 18k 
>#       Score: mpro, antiviral, drug, inhibitors, protease, drugs, compounds 
># Topic 3 Top Words:
>#       Highest Prob: covid, risk, age, mortality, ci, associated, years 
>#       FREX: hispanic, ethnicity, pregnant, racial, black, smoking, preterm 
>#       Lift: 65s, asmr, assault, backgroundethnic, backgroundracial, backgroundsocio, brunt 
>#       Score: ci, age, women, mortality, ethnicity, aor, hispanic 
># Topic 4 Top Words:
>#       Highest Prob: covid, health, pandemic, mental, social, study, survey 
>#       FREX: loneliness, emotional, attitude, depression, insecurity, mental, anxiety 
>#       Lift: insecurity, accelerometers, amhara, angry, anovas, asd, asleep 
>#       Score: mental, anxiety, depression, respondents, social, psychological, students 
># Topic 5 Top Words:
>#       Highest Prob: sars, cov, infection, testing, transmission, cases, children 
>#       FREX: ifr, seroprevalence, schools, school, contacts, household, attack 
>#       Lift: inmates, 19y, 35y, 39y, 9a, abidjan, addscovid 
>#       Score: school, seroprevalence, children, schools, household, transmission, testing 
># Topic 6 Top Words:
>#       Highest Prob: cov, sars, virus, viral, coronavirus, respiratory, infection 
>#       FREX: bats, cats, deer, animals, covs, wildlife, hcov 
>#       Lift: cats, 5x106, aav6, aegyptiacus, aethiops, affinis, agm 
>#       Score: cov, sars, mice, rna, viruses, coronaviruses, animals 
># Topic 7 Top Words:
>#       Highest Prob: patients, covid, hospital, disease, clinical, severe, admission 
>#       FREX: acei, admission, arbs, admitted, icu, aki, aceis 
>#       Lift: 1.1x109, 2020r1g1a1a01006229, 2l, 4.0x109, 40y, ahmad, ahrq 
>#       Score: patients, admission, icu, hospital, admitted, ci, hospitalized 
># Topic 8 Top Words:
>#       Highest Prob: covid, cases, countries, number, deaths, data, pandemic 
>#       FREX: cfr, italy, cities, country, countries, fatality, china 
>#       Lift: 1000m, 1th, 55th, abysmally, abyss, adhanom, adminstat 
>#       Score: countries, cases, lockdown, deaths, country, cfr, daily 
># Topic 9 Top Words:
>#       Highest Prob: protein, binding, spike, sars, cov, ace2, rbd 
>#       FREX: conformational, cryo, conformation, glycans, conformations, nanobodies, residues 
>#       Lift: 13c, 6lzg, 6m0j, 6vw1, 6vxx, aabpu, abdab 
>#       Score: binding, rbd, protein, spike, ace2, proteins, epitopes 
># Topic 10 Top Words:
>#       Highest Prob: data, can, learning, covid, using, model, based 
>#       FREX: aerosol, n95, aerosols, respirators, decontamination, airborne, machine 
>#       Lift: elastomeric, forehead, papr, radiomics, exhaled, singing, 0.3m 
>#       Score: learning, masks, aerosol, machine, respirators, n95, mask 
># Topic 11 Top Words:
>#       Highest Prob: vaccine, vaccination, covid, middle, vaccines, dot, dose 
>#       FREX: hesitancy, dot, vaccinate, middle, hesitant, rollout, ve 
>#       Lift: #949850, acceptant, adjrr, aesis, amparo, analysesthe, andersen 
>#       Score: vaccination, vaccine, dot, booster, dose, vaccinated, middle 
># Topic 12 Top Words:
>#       Highest Prob: studies, care, covid, health, research, data, pandemic 
>#       FREX: reviews, telemedicine, preprints, scoping, articles, blacksquare, publications 
>#       Lift: preprints, 1.2m, aas, abbreviating, accustomed, activists, advisor 
>#       Score: review, care, services, articles, reviews, pubmed, service 
># Topic 13 Top Words:
>#       Highest Prob: sars, cov, genome, mutations, sequencing, viral, variants 
>#       FREX: phylogenetic, gisaid, clades, wgs, genomes, genomic, haplotype 
>#       Lift: clades, snvs, 1.1.7s, 11083g, 14408c, 17del, 20a 
>#       Score: mutations, genome, wastewater, genomes, sequences, sequencing, genomic 
># Topic 14 Top Words:
>#       Highest Prob: cells, cell, sars, cov, expression, infection, ace2 
>#       FREX: autophagy, mirnas, mirna, at2, ifns, ciliated, scrna 
>#       Lift: 25hc, angiotensinogen, antagonizes, apcs, arf6, asgr1, at2s 
>#       Score: cells, expression, ace2, cell, genes, epithelial, tmprss2 
># Topic 15 Top Words:
>#       Highest Prob: antibody, sars, cov, antibodies, igg, responses, vaccine 
>#       FREX: iga, bau, igg, humoral, immunogenicity, as03, reactogenicity 
>#       Lift: 1x1011, 28d, 30ug, ad26cov2, addas03, adhu5, atellica 
>#       Score: igg, antibody, antibodies, neutralizing, rbd, vaccine, spike 
># Topic 16 Top Words:
>#       Highest Prob: sars, cov, pcr, samples, rt, test, testing 
>#       FREX: ag, rdt, rdts, lod, rt, panbio, kits 
>#       Lift: poct, cobas, panbio, #yomecorono, 1.6x104, 10min, 15min 
>#       Score: rt, pcr, assay, samples, saliva, detection, assays 
># Topic 17 Top Words:
>#       Highest Prob: variants, omicron, variant, delta, ba, cov, sars 
>#       FREX: omicron, ba, xbb, subvariants, delta, bq, voc 
>#       Lift: 1.5s, 129s2, 1f11, 2.86s, 3b8, 417n, 75d30121c11061 
>#       Score: omicron, ba, variants, variant, delta, mutations, voc 
># Topic 18 Top Words:
>#       Highest Prob: covid, patients, disease, severe, immune, inflammatory, associated 
>#       FREX: autoantibodies, ipf, balf, neutrophils, il, fibrosis, autoantibody 
>#       Lift: 18f, 24hr, a2ar, aab, actinobacteria, activin, adiponectin 
>#       Score: inflammatory, il, patients, cytokine, inflammation, cytokines, endothelial 
># Topic 19 Top Words:
>#       Highest Prob: patients, treatment, covid, group, days, day, trial 
>#       FREX: placebo, randomized, hcq, soc, azithromycin, arm, tocilizumab 
>#       Lift: 200mg, 400mg, 500mg, 600mg, 800mg, aureobasidium, ayush 
>#       Score: placebo, hcq, trial, patients, randomized, tocilizumab, hydroxychloroquine 
># Topic 20 Top Words:
>#       Highest Prob: covid, symptoms, long, workers, infection, participants, study 
>#       FREX: hcws, taste, smell, hcw, fatigue, workers, headache 
>#       Lift: chemesthetic, dirty, eyewear, firefighters, ohs, principality, psychophysical 
>#       Score: symptoms, hcws, workers, participants, symptom, hcw, fatigue
```

```{=html}
<aside class="notes">
```
The `summary()` function provides a more detailed view of the topics and
can help to begin interpreting and labeling the 20 topics. Specifically,
the output shows four different sets of words associated with a topic.
*'Highest Prob'* lists the words that have the highest probability of
being associated with a topic. A comparison of different topics
highlights that a term such as *covid* has a high probability for
several topics. The list of *'FREX'* words summarizes words that are
frequent and exclusive in a topic, i.e. characterize a topic in
comparison to other topics (consult `stm::labelTopics()` for details as
well as *Lift* and *Score* word sets).
```{=html}
</aside>
```
## Topic-document ('gamma') distribution

``` r
# retrieve the 'gamma' matrix
gamma <- tidytext::tidy(covid_model_K20, matrix = "gamma")

glimpse(gamma)
># Rows: 593,820
># Columns: 3
># $ document <int> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18…
># $ topic    <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
># $ gamma    <dbl> 0.001283143, 0.003547179, 0.003745510, 0.005495076, 0.0630417…
```

```{=html}
<aside class="notes">
```
As mentioned, the topic model is defined by the *gamma* (distribution of
topics over words) and *beta* (distribution of terms over topics)
matrices. With the help of the `tidytext` package we can extract those
into dataframes for a more detailed analysis.

Each row in the following dataframe lists the probability (`gamma`) of a
given `topic` occurring in a given `document`[^2].
```{=html}
</aside>
```
## Term-topic ('beta') distribution

``` r
# retrieve the 'beta' matrix
beta <- tidytext::tidy(covid_model_K20, matrix = "beta")

glimpse(beta)
># Rows: 741,860
># Columns: 3
># $ topic <int> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 1…
># $ term  <chr> "#1", "#1", "#1", "#1", "#1", "#1", "#1", "#1", "#1", "#1", "#1"…
># $ beta  <dbl> 1.874650e-112, 2.519509e-119, 1.248970e-118, 6.665355e-160, 3.21…
```

```{=html}
<aside class="notes">
```
Similarly, the *beta* matrix (extracted into a dataframe) lists for each
row the probability (`beta`) of a given `term` occurring in a given
`topic`.

Starting with the *beta* matrix we can create word clouds to explore
useful semantic labels for each topic.
```{=html}
</aside>
```
## Understanding and labeling topics

::: figure
`<img src="figures/unnamed-chunk-19-1.png" alt="**Word clouds showing the 50 most probable terms for selected topics.** *FREX* terms are highlighted in orange. Words are scaled by normalized probability." width="80%" />`{=html}
```{=html}
<p class="caption">
```
**Word clouds showing the 50 most probable terms for selected topics.**
*FREX* terms are highlighted in orange. Words are scaled by normalized
probability.
```{=html}
</p>
```
:::

```{=html}
<aside class="notes">
```
As mentioned previously `stm` can use the word probabilities to also
compute *FREX* (frequent and exclusive) words per topic. Those can be
retrieved with the `stm::labelTopics()` function, which returns ordered
lists of the different word sets characterizing a topic. We can combine
the information about *high probability* and *FREX* words to create word
clouds for each topic, which might help to assign a summary label for
each topic.

From the review of this combination of *FREX* and *high probability*
terms distinct topics are emerging, such as: "epidemic models" (Topic
1), "vaccines" (Topic 11), "testing" (Topic 16), "virus variants" (Topic
17), "treatments" (Topic 2), "mortality risks" (Topic 3), "mental
health" (Topic 4), "country-wise case reports" (Topic 8), "virus
molecular structure" (Topic 9).

Deriving semantic labels will also benefit from a review of sample
documents that are representative for certain topics, i.e. where the
topic model assigns a high topic proportion of a given topic to the
document. Furthermore, the consistency of assigned semantic labels
should be checked prior to further analysis (see for example the
[`oolong` package](https://github.com/gesistsa/oolong) for a systematic
approach).
```{=html}
</aside>
```
## Covariate effects

``` r

summary(covid_effect_K20)
># 
># Call:
># estimateEffect(formula = 1:20 ~ server * s(year), stmobj = covid_model_K20, 
>#     metadata = covid_stm_docs$meta)
># 
># 
># Topic 1:
># 
># Coefficients:
>#                          Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.0234515  0.0036964   6.344 2.27e-10 ***
># servermedrxiv           0.1239364  0.0043129  28.736  < 2e-16 ***
># s(year)1               -0.0019176  0.0147550  -0.130    0.897    
># s(year)2               -0.0007684  0.0153892  -0.050    0.960    
># s(year)3                0.0084132  0.0066881   1.258    0.208    
># servermedrxiv:s(year)1 -0.0695085  0.0173024  -4.017 5.90e-05 ***
># servermedrxiv:s(year)2 -0.0965498  0.0188849  -5.113 3.20e-07 ***
># servermedrxiv:s(year)3 -0.0705657  0.0084431  -8.358  < 2e-16 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 2:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.098665   0.002880  34.262  < 2e-16 ***
># servermedrxiv          -0.085926   0.003158 -27.212  < 2e-16 ***
># s(year)1               -0.019958   0.011371  -1.755   0.0792 .  
># s(year)2               -0.011330   0.013466  -0.841   0.4002    
># s(year)3               -0.028581   0.004509  -6.338 2.36e-10 ***
># servermedrxiv:s(year)1  0.021636   0.012575   1.721   0.0853 .  
># servermedrxiv:s(year)2  0.008216   0.014417   0.570   0.5688    
># servermedrxiv:s(year)3  0.030329   0.005231   5.797 6.81e-09 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 3:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.011092   0.002813   3.943 8.06e-05 ***
># servermedrxiv           0.053932   0.003297  16.356  < 2e-16 ***
># s(year)1               -0.002642   0.011400  -0.232    0.817    
># s(year)2               -0.001958   0.011826  -0.166    0.868    
># s(year)3                0.001212   0.004877   0.248    0.804    
># servermedrxiv:s(year)1  0.015020   0.013729   1.094    0.274    
># servermedrxiv:s(year)2  0.014190   0.014918   0.951    0.341    
># servermedrxiv:s(year)3  0.029833   0.006503   4.588 4.50e-06 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 4:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.008823   0.003238   2.724  0.00644 ** 
># servermedrxiv           0.057738   0.003798  15.203  < 2e-16 ***
># s(year)1                0.004814   0.013529   0.356  0.72200    
># s(year)2               -0.005213   0.014162  -0.368  0.71282    
># s(year)3                0.004560   0.005826   0.783  0.43375    
># servermedrxiv:s(year)1  0.020339   0.016434   1.238  0.21587    
># servermedrxiv:s(year)2 -0.004031   0.018172  -0.222  0.82445    
># servermedrxiv:s(year)3  0.020310   0.007672   2.647  0.00812 ** 
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 5:
># 
># Coefficients:
>#                          Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.0049430  0.0023398   2.113   0.0346 *  
># servermedrxiv           0.0542764  0.0027865  19.479   <2e-16 ***
># s(year)1               -0.0008134  0.0094139  -0.086   0.9311    
># s(year)2                0.0001471  0.0099193   0.015   0.9882    
># s(year)3                0.0010546  0.0041428   0.255   0.7991    
># servermedrxiv:s(year)1  0.0260782  0.0114114   2.285   0.0223 *  
># servermedrxiv:s(year)2 -0.0018302  0.0120509  -0.152   0.8793    
># servermedrxiv:s(year)3 -0.0084726  0.0053670  -1.579   0.1144    
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 6:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.148602   0.003866  38.434  < 2e-16 ***
># servermedrxiv          -0.115782   0.004229 -27.376  < 2e-16 ***
># s(year)1               -0.021101   0.013517  -1.561   0.1185    
># s(year)2               -0.049243   0.012155  -4.051 5.11e-05 ***
># s(year)3               -0.043708   0.006071  -7.200 6.18e-13 ***
># servermedrxiv:s(year)1  0.005903   0.015136   0.390   0.6965    
># servermedrxiv:s(year)2  0.035413   0.013879   2.552   0.0107 *  
># servermedrxiv:s(year)3  0.031026   0.006946   4.467 7.97e-06 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 7:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.010755   0.002934   3.665 0.000247 ***
># servermedrxiv           0.085991   0.003494  24.613  < 2e-16 ***
># s(year)1               -0.004033   0.011512  -0.350 0.726124    
># s(year)2               -0.007886   0.012201  -0.646 0.518060    
># s(year)3               -0.003443   0.005144  -0.669 0.503331    
># servermedrxiv:s(year)1 -0.049305   0.014424  -3.418 0.000631 ***
># servermedrxiv:s(year)2 -0.019589   0.015580  -1.257 0.208630    
># servermedrxiv:s(year)3 -0.038387   0.006513  -5.894 3.82e-09 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 8:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.027280   0.003058   8.922  < 2e-16 ***
># servermedrxiv           0.108710   0.003615  30.070  < 2e-16 ***
># s(year)1               -0.012889   0.012357  -1.043  0.29692    
># s(year)2               -0.018333   0.012554  -1.460  0.14423    
># s(year)3               -0.017113   0.005274  -3.245  0.00118 ** 
># servermedrxiv:s(year)1 -0.088615   0.014896  -5.949 2.73e-09 ***
># servermedrxiv:s(year)2 -0.046434   0.015515  -2.993  0.00277 ** 
># servermedrxiv:s(year)3 -0.060223   0.006653  -9.052  < 2e-16 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 9:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.170474   0.004565  37.348  < 2e-16 ***
># servermedrxiv          -0.163920   0.004774 -34.337  < 2e-16 ***
># s(year)1                0.018139   0.018989   0.955 0.339489    
># s(year)2               -0.034923   0.019954  -1.750 0.080097 .  
># s(year)3               -0.027951   0.006600  -4.235 2.29e-05 ***
># servermedrxiv:s(year)1 -0.010980   0.020160  -0.545 0.585981    
># servermedrxiv:s(year)2  0.033233   0.021775   1.526 0.126979    
># servermedrxiv:s(year)3  0.027871   0.007250   3.844 0.000121 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 10:
># 
># Coefficients:
>#                          Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.0447574  0.0033294  13.443  < 2e-16 ***
># servermedrxiv           0.0117705  0.0036073   3.263   0.0011 ** 
># s(year)1                0.0040479  0.0146668   0.276   0.7826    
># s(year)2                0.0002623  0.0132770   0.020   0.9842    
># s(year)3                0.0261219  0.0058535   4.463 8.13e-06 ***
># servermedrxiv:s(year)1 -0.0176944  0.0162961  -1.086   0.2776    
># servermedrxiv:s(year)2 -0.0303798  0.0153824  -1.975   0.0483 *  
># servermedrxiv:s(year)3 -0.0408835  0.0069903  -5.849 5.01e-09 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 11:
># 
># Coefficients:
>#                        Estimate Std. Error t value Pr(>|t|)    
># (Intercept)            0.005048   0.002350   2.148  0.03172 *  
># servermedrxiv          0.008220   0.002685   3.061  0.00221 ** 
># s(year)1               0.010261   0.009886   1.038  0.29933    
># s(year)2               0.009911   0.010201   0.972  0.33129    
># s(year)3               0.006487   0.004252   1.525  0.12717    
># servermedrxiv:s(year)1 0.056818   0.011643   4.880 1.07e-06 ***
># servermedrxiv:s(year)2 0.073874   0.012513   5.904 3.59e-09 ***
># servermedrxiv:s(year)3 0.046904   0.005889   7.964 1.72e-15 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 12:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.022004   0.002821   7.799 6.44e-15 ***
># servermedrxiv           0.041906   0.003351  12.505  < 2e-16 ***
># s(year)1               -0.008612   0.011290  -0.763    0.446    
># s(year)2               -0.005776   0.012238  -0.472    0.637    
># s(year)3               -0.002634   0.004890  -0.539    0.590    
># servermedrxiv:s(year)1 -0.006542   0.013997  -0.467    0.640    
># servermedrxiv:s(year)2  0.009470   0.015896   0.596    0.551    
># servermedrxiv:s(year)3  0.034847   0.006471   5.385 7.30e-08 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 13:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.104347   0.003136  33.278  < 2e-16 ***
># servermedrxiv          -0.086326   0.003442 -25.084  < 2e-16 ***
># s(year)1               -0.031507   0.015444  -2.040   0.0414 *  
># s(year)2               -0.027982   0.015186  -1.843   0.0654 .  
># s(year)3               -0.023283   0.005574  -4.177 2.96e-05 ***
># servermedrxiv:s(year)1  0.077694   0.018009   4.314 1.61e-05 ***
># servermedrxiv:s(year)2  0.028379   0.017050   1.664   0.0960 .  
># servermedrxiv:s(year)3  0.041046   0.006634   6.187 6.21e-10 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 14:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.124590   0.003384  36.820   <2e-16 ***
># servermedrxiv          -0.112726   0.003591 -31.387   <2e-16 ***
># s(year)1                0.004251   0.015015   0.283    0.777    
># s(year)2               -0.007534   0.015561  -0.484    0.628    
># s(year)3                0.007579   0.006327   1.198    0.231    
># servermedrxiv:s(year)1 -0.003159   0.015996  -0.198    0.843    
># servermedrxiv:s(year)2  0.005290   0.016662   0.317    0.751    
># servermedrxiv:s(year)3 -0.005121   0.007090  -0.722    0.470    
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 15:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.053500   0.003506  15.260  < 2e-16 ***
># servermedrxiv          -0.027398   0.003954  -6.930  4.3e-12 ***
># s(year)1                0.044569   0.014766   3.018  0.00254 ** 
># s(year)2                0.024796   0.015595   1.590  0.11185    
># s(year)3                0.017761   0.006468   2.746  0.00604 ** 
># servermedrxiv:s(year)1  0.003689   0.017297   0.213  0.83112    
># servermedrxiv:s(year)2  0.033607   0.017897   1.878  0.06042 .  
># servermedrxiv:s(year)3 -0.003409   0.007628  -0.447  0.65498    
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 16:
># 
># Coefficients:
>#                          Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.0531712  0.0034678  15.333  < 2e-16 ***
># servermedrxiv           0.0176174  0.0040551   4.344 1.40e-05 ***
># s(year)1               -0.0494979  0.0130158  -3.803 0.000143 ***
># s(year)2               -0.0294507  0.0131905  -2.233 0.025574 *  
># s(year)3               -0.0279314  0.0057186  -4.884 1.04e-06 ***
># servermedrxiv:s(year)1  0.0608908  0.0150385   4.049 5.16e-05 ***
># servermedrxiv:s(year)2  0.0011834  0.0159698   0.074 0.940929    
># servermedrxiv:s(year)3 -0.0007032  0.0072105  -0.098 0.922307    
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 17:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.012520   0.002371   5.280 1.30e-07 ***
># servermedrxiv          -0.010867   0.002660  -4.086 4.40e-05 ***
># s(year)1                0.062508   0.012011   5.204 1.96e-07 ***
># s(year)2                0.167150   0.016081  10.394  < 2e-16 ***
># s(year)3                0.074767   0.005337  14.010  < 2e-16 ***
># servermedrxiv:s(year)1 -0.043602   0.013428  -3.247  0.00117 ** 
># servermedrxiv:s(year)2 -0.080085   0.017937  -4.465 8.05e-06 ***
># servermedrxiv:s(year)3 -0.037938   0.006115  -6.204 5.58e-10 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 18:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.055671   0.003054  18.226  < 2e-16 ***
># servermedrxiv          -0.019875   0.003469  -5.730 1.02e-08 ***
># s(year)1                0.005595   0.011997   0.466  0.64098    
># s(year)2                0.004178   0.012679   0.330  0.74178    
># s(year)3                0.029362   0.005773   5.086 3.67e-07 ***
># servermedrxiv:s(year)1 -0.004546   0.014663  -0.310  0.75652    
># servermedrxiv:s(year)2 -0.004705   0.015357  -0.306  0.75934    
># servermedrxiv:s(year)3 -0.020633   0.006881  -2.998  0.00272 ** 
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 19:
># 
># Coefficients:
>#                          Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.0135420  0.0025816   5.246 1.57e-07 ***
># servermedrxiv           0.0273553  0.0030260   9.040  < 2e-16 ***
># s(year)1                0.0005638  0.0100195   0.056   0.9551    
># s(year)2               -0.0062746  0.0106155  -0.591   0.5545    
># s(year)3               -0.0030674  0.0043700  -0.702   0.4827    
># servermedrxiv:s(year)1 -0.0031003  0.0122137  -0.254   0.7996    
># servermedrxiv:s(year)2  0.0280690  0.0131424   2.136   0.0327 *  
># servermedrxiv:s(year)3  0.0027473  0.0057495   0.478   0.6328    
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 20:
># 
># Coefficients:
>#                          Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.0067098  0.0019459   3.448 0.000565 ***
># servermedrxiv           0.0314496  0.0021906  14.357  < 2e-16 ***
># s(year)1               -0.0013966  0.0077057  -0.181 0.856184    
># s(year)2               -0.0001134  0.0081834  -0.014 0.988945    
># s(year)3                0.0005030  0.0033764   0.149 0.881568    
># servermedrxiv:s(year)1  0.0085872  0.0096124   0.893 0.371678    
># servermedrxiv:s(year)2  0.0129469  0.0106830   1.212 0.225552    
># servermedrxiv:s(year)3  0.0212786  0.0045697   4.656 3.23e-06 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

```{=html}
<aside class="notes">
```
A key feature of STM is the incorporation of document covariates into
the topic model. In our example we considered the publication year and
the preprint server as covariates that might influence the prevalence of
a topic in a document. We also applied a regression for these covariates
to the fit model, which were extracted with `stm::estimateEffect()`.

As a first exploration we can print the regression tables for all or
selected topics.
```{=html}
</aside>
```
## Publication year

`<img src="figures/unnamed-chunk-22-1.png" width="70%" />`{=html}

```{=html}
<aside class="notes">
```
`stm` offers several built-in methods to explore the covariate effects
visually. The visualization of the effect of preprint *publication year*
on *expected topic proportions* confirm some trends that appear to match
intuitively with different phases of the Covid-19 pandemic. Modelling
the spread of infections (Topic 1) had a high relevance initially, but
declined later, the same applies to (PCR-)testing (Topic 16), while
vaccines (Topic 11) received limited coverage in earlier preprints, but
became more important in later years as they were developed and
distributed.
```{=html}
</aside>
```
## Plotting with `stm`

``` r
plot(covid_effect_K20,
     covariate = "year",
     method = "continuous",
     model = covid_model_K20,
     topics = c(1, 16, 11),
     xaxt = "n",
     main = 'Effect of publication year on prevalence of Topic 1 ("epidemic \nmodels"), Topic 16 ("testing") and Topic 11 ("vaccines")',
     labeltype = "prob",
     xlab = "Publication year")
axis(1, at = c("2020","2021","2022","2023"), labels = c(2020, 2021, 2022, 2023))
```

## Plotting with `stminsights`

`<img src="figures/unnamed-chunk-24-1.png" width="80%" />`{=html}

```{=html}
<aside class="notes">
```
Alternatively, the `stminsights` package could be used to extract the
same regression information from the `stm` effects object and create
customized charts.
```{=html}
</aside>
```
## 'Treatment' effect: preprint server

![](figures/unnamed-chunk-25-1.png)

```{=html}
<aside class="notes">
```
The model also incorporated the preprint server (*bioRxiv* and
*medRxiv*) as a covariate. We hypothesized that the prevalence of
certain topics will be influenced by this covariate, i.e. that we are
more likely to see certain topics on either *bioRxiv* and *medRxiv*. STM
interprets this as a *treatment* (see [@RobertsStewart_et_2014_AJPS_58]
for background and examples) and we can extract the effect of this
treatment from the regression object returned by `estimateEffect()`.

The `stm::plot()` offers different methods to explore those effects. The
figure below lists the effect of *'treatment medrxiv'* for all topics in
the model. The treatment can have a positive or negative effect. Here we
can for example see that Topic 4 ("mental health") can be expected with
higher prevalence in *medRxiv* preprints, whereas Topic 9 ("virus
molecular structure") will have a much lower prevalence in *medRxiv*
preprints, i.e. should be expected with higher prevalence in *bioRxiv*
preprints.
```{=html}
</aside>
```
## 'Treatment' effect: preprint server

![](figures/unnamed-chunk-26-1.png)

```{=html}
<aside class="notes">
```
We can also compare the topical prevalence effect of covariate values
for a single topic. The figure below confirms the previous observation
for Topic 9 ("virus molecular structure") which has a prevalence close
to zero in *medRxiv* preprints but a prevalence of approximately 0.17
for *bioRxiv* preprints, i.e. it seems to appear almost exclusively in
the latter.
```{=html}
</aside>
```
## Combination of preprint server and publication year

`<img src="figures/unnamed-chunk-27-1.png" width="70%" />`{=html}

```{=html}
<aside class="notes">
```
Finally, we can also explore the combined effect of covariates; we
assumed an interacting effect of the two covariates `server` and `year`.
The plot below visualizes this for Topic 17 ("virus variants") and
illustrates that the topical prevalence increased throughout the
pandemic in all preprints but that the topic apparently received more
coverage in *bioRxiv* preprints.
```{=html}
</aside>
```
## Using `stminsight`

`<img src="figures/unnamed-chunk-28-1.png" width="80%" />`{=html}

```{=html}
<aside class="notes">
```
Again, `stminsights` can be used to retrieve this information and create
customized visualizations for the combined covariate effect.
```{=html}
</aside>
```
## Exploring the topic structure

## Topic correlations

``` r
covid_topic_correlations <- topicCorr(covid_model_K20)
plot(covid_topic_correlations)
```

`<img src="figures/unnamed-chunk-29-1.png" width="80%" />`{=html}

```{=html}
<aside class="notes">
```
Finally, considering that STM is extending
[@RobertsStewart_et_2019_JSTATS_91] a correlated topic model
[@BleiLafferty2007_AAS_1] we may also explore if topics are frequently
cooccuring. A a topic correlation matrix is retrieved with
`stm::topicCorr()` which can then be plotted. The resulting figure below
indicates at least two clusters of topics.
```{=html}
</aside>
```
## Network analysis of topics

::: {.fig-container data-file="topic_correlation.html"}
:::

```{=html}
<aside class="notes">
```
The correlation matrix can be used for further analysis (e.g. networks
and clusters) or alternative visualizations. Both are outside the scope
of this example and the course module. For illustration, the following
figure creates an alternative network visualization, with nodes colored
according to a community analysis of the topical network, which here
reveals four distinct topical clusters.
```{=html}
</aside>
```
# Exercises

## Exploring biodiversity preprints

-   Create a subset of preprints referencing "biodiversity"; fit a topic
    model with 10 topics and explore the interacting effect of
    covariates `is_published` and `year` (not `s(year)`).

# Thank You!

## Key Resources

-   [quanteda R package](http://quanteda.io/)
-   [stm: An R Package for Structural Topic
    Models](https://www.jstatsoft.org/article/view/v091i02)
    [@RobertsStewart_et_2019_JSTATS_91]
-   [oolong R package](https://github.com/chainsawriot/oolong)

## References {#references .top-aligned-slide}

::: {#refs}
:::

## Colophon {#colophon .colophon}

**"Structural Topic Modeling with R"** by *Stefan Daume*

 

Presented at DS4SD SRC R course on 11. April 2025.

 

This presentation can be cited using: *doi:...*

 

**PRESENTATION DETAILS**

**Author/Affiliation:** Stefan Daume, Stockholm Resilience Centre,
Stockholm University

**Presentation URL:**
<https://sdaume.github.io/ds4sd-2024-modules/topicmodels/slides/>

**Presentation Source:** \[TBD\]

**Presentation PDF:** \[TBD\]

 

**CREDITS & LICENSES**

This presentation is delivered with the help of several free and open
source tools and libraries. It utilises the
[reveal.js](https://revealjs.com/) presentation framework and has been
created using [RMarkdown](https://rmarkdown.rstudio.com),
[knitr](https://yihui.name/knitr/), [RStudio](https://www.rstudio.com)
and [Pandoc](https://pandoc.org/).
[highlight.js](https://highlightjs.org) provides syntax highlighting for
code sections. [MathJax](https://www.mathjax.org) supports the rendering
of mathematical notations. PDF and JPG copies of this presentation were
generated with [DeckTape](https://github.com/astefanutti/decktape).
Please note the respective licenses of these tools and libraries.

 

If not noted and attributed otherwise, the contents (text, charts,
images) of this presentation are **Copyright © 2025 of the Author** and
provided under a *CC BY 4.0* public domain license.

[^1]: NOTE we use the recommended spline function for the `year`
    variable. Consult the STM documentation for details on this.

[^2]: NOTE that for each document a non-zero probability for all topics
    is assigned.
