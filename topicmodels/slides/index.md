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

# "Text as data" - Basic text mining

## Getting and exploring text

Basic packages:

-   tidytext
-   stringr
-   dplyr
-   tidyr
-   (SnowballC)
-   (spacyr)
-   (textdata)

## Basic and common steps

1.  get text (e.g., via gutenbergr)
2.  tidy
3.  tokenize
4.  transform
5.  (annotate)
6.  analyze

## Basic analysis: get text, tidy, count

``` r
library(gutenbergr)
library(dplyr)
library(tidytext)

# get "mystery" text
book <- gutenberg_download(c(244))

# tidy the text into individual words
# also lowercases and remove punctuation
tidy_book <- book %>%
  unnest_tokens(output = word, input = text)

# count the word/term frequency
word_count <- tidy_book %>%
  count(word, sort = TRUE)
```

## Most frequent words

::: {style="display:table;width:100%;table-layout:fixed;"}
::: {style="display:table-cell;width:60%;padding-right:5%;text-align:left;vertical-align:top;"}
``` r
library(gutenbergr)
library(dplyr)
library(tidytext)

# get "mystery" text
book <- gutenberg_download(c(244))

# tidy the text into individual words
# also lowercases and removes punctuation
tidy_book <- book %>%
  unnest_tokens(output = word, input = text)

# count the word/term frequency
word_count <- tidy_book %>%
  count(word, sort = TRUE)
```
:::

::: {style="display:table-cell;width:40%;padding-left:5%;text-align:left;vertical-align:top;"}
```{=html}
<div id="hzfgjmkqnx" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>#hzfgjmkqnx table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#hzfgjmkqnx thead, #hzfgjmkqnx tbody, #hzfgjmkqnx tfoot, #hzfgjmkqnx tr, #hzfgjmkqnx td, #hzfgjmkqnx th {
  border-style: none;
}

#hzfgjmkqnx p {
  margin: 0;
  padding: 0;
}

#hzfgjmkqnx .gt_table {
  display: table;
  border-collapse: collapse;
  line-height: normal;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #A8A8A8;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #A8A8A8;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}

#hzfgjmkqnx .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#hzfgjmkqnx .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#hzfgjmkqnx .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 3px;
  padding-bottom: 5px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#hzfgjmkqnx .gt_heading {
  background-color: #FFFFFF;
  text-align: center;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#hzfgjmkqnx .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#hzfgjmkqnx .gt_col_headings {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#hzfgjmkqnx .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}

#hzfgjmkqnx .gt_column_spanner_outer {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}

#hzfgjmkqnx .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#hzfgjmkqnx .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#hzfgjmkqnx .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}

#hzfgjmkqnx .gt_spanner_row {
  border-bottom-style: hidden;
}

#hzfgjmkqnx .gt_group_heading {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  text-align: left;
}

#hzfgjmkqnx .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: middle;
}

#hzfgjmkqnx .gt_from_md > :first-child {
  margin-top: 0;
}

#hzfgjmkqnx .gt_from_md > :last-child {
  margin-bottom: 0;
}

#hzfgjmkqnx .gt_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#hzfgjmkqnx .gt_stub {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
}

#hzfgjmkqnx .gt_stub_row_group {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
  vertical-align: top;
}

#hzfgjmkqnx .gt_row_group_first td {
  border-top-width: 2px;
}

#hzfgjmkqnx .gt_row_group_first th {
  border-top-width: 2px;
}

#hzfgjmkqnx .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#hzfgjmkqnx .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#hzfgjmkqnx .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#hzfgjmkqnx .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#hzfgjmkqnx .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#hzfgjmkqnx .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#hzfgjmkqnx .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#hzfgjmkqnx .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#hzfgjmkqnx .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#hzfgjmkqnx .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#hzfgjmkqnx .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#hzfgjmkqnx .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#hzfgjmkqnx .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#hzfgjmkqnx .gt_left {
  text-align: left;
}

#hzfgjmkqnx .gt_center {
  text-align: center;
}

#hzfgjmkqnx .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#hzfgjmkqnx .gt_font_normal {
  font-weight: normal;
}

#hzfgjmkqnx .gt_font_bold {
  font-weight: bold;
}

#hzfgjmkqnx .gt_font_italic {
  font-style: italic;
}

#hzfgjmkqnx .gt_super {
  font-size: 65%;
}

#hzfgjmkqnx .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#hzfgjmkqnx .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#hzfgjmkqnx .gt_indent_1 {
  text-indent: 5px;
}

#hzfgjmkqnx .gt_indent_2 {
  text-indent: 10px;
}

#hzfgjmkqnx .gt_indent_3 {
  text-indent: 15px;
}

#hzfgjmkqnx .gt_indent_4 {
  text-indent: 20px;
}

#hzfgjmkqnx .gt_indent_5 {
  text-indent: 25px;
}

#hzfgjmkqnx .katex-display {
  display: inline-flex !important;
  margin-bottom: 0.75em !important;
}

#hzfgjmkqnx div.Reactable > div.rt-table > div.rt-thead > div.rt-tr.rt-tr-group-header > div.rt-th-group:after {
  height: 0px !important;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <thead>
    <tr class="gt_heading">
      <td colspan="2" class="gt_heading gt_title gt_font_normal" style>Mystery Book Word Count</td>
    </tr>
    <tr class="gt_heading">
      <td colspan="2" class="gt_heading gt_subtitle gt_font_normal gt_bottom_border" style><span class='gt_from_md'>(10 most frequent terms)</span></td>
    </tr>
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="word">word</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="n">n</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><td headers="word" class="gt_row gt_left">the</td>
<td headers="n" class="gt_row gt_right">2536</td></tr>
    <tr><td headers="word" class="gt_row gt_left">and</td>
<td headers="n" class="gt_row gt_right">1356</td></tr>
    <tr><td headers="word" class="gt_row gt_left">of</td>
<td headers="n" class="gt_row gt_right">1213</td></tr>
    <tr><td headers="word" class="gt_row gt_left">to</td>
<td headers="n" class="gt_row gt_right">1093</td></tr>
    <tr><td headers="word" class="gt_row gt_left">a</td>
<td headers="n" class="gt_row gt_right">1010</td></tr>
    <tr><td headers="word" class="gt_row gt_left">i</td>
<td headers="n" class="gt_row gt_right">904</td></tr>
    <tr><td headers="word" class="gt_row gt_left">he</td>
<td headers="n" class="gt_row gt_right">795</td></tr>
    <tr><td headers="word" class="gt_row gt_left">in</td>
<td headers="n" class="gt_row gt_right">727</td></tr>
    <tr><td headers="word" class="gt_row gt_left">that</td>
<td headers="n" class="gt_row gt_right">655</td></tr>
    <tr><td headers="word" class="gt_row gt_left">his</td>
<td headers="n" class="gt_row gt_right">652</td></tr>
  </tbody>
  
  
</table>
</div>
```
:::
:::

```{=html}
<aside class="notes">
```
-   you then point to the ".bib" file in the document's YAML header and
    include citations of your references as such `[@CitationKey]` in
    your text
-   and add a `# References` section at the end of your header

```{=html}
</aside>
```
## Exclude "stop words"

::: {style="display:table;width:100%;table-layout:fixed;"}
::: {style="display:table-cell;width:60%;padding-right:5%;text-align:left;vertical-align:top;"}
``` r
library(gutenbergr)
library(dplyr)
library(tidytext)

# get "mystery" text
book <- gutenberg_download(c(244))

# tidy the text into individual words
# also lowercases and removes punctuation
tidy_book <- book %>%
  unnest_tokens(output = word, input = text)

# remove stopwords 
# (lexicon provided with tidytext)
word_count_filtered <- tidy_book %>%
  anti_join(stop_words) %>%
  count(word, sort = TRUE)
```
:::

::: {style="display:table-cell;width:40%;padding-left:5%;text-align:left;vertical-align:top;"}
```{=html}
<div id="tgqkoolqnt" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>#tgqkoolqnt table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#tgqkoolqnt thead, #tgqkoolqnt tbody, #tgqkoolqnt tfoot, #tgqkoolqnt tr, #tgqkoolqnt td, #tgqkoolqnt th {
  border-style: none;
}

#tgqkoolqnt p {
  margin: 0;
  padding: 0;
}

#tgqkoolqnt .gt_table {
  display: table;
  border-collapse: collapse;
  line-height: normal;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #A8A8A8;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #A8A8A8;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}

#tgqkoolqnt .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#tgqkoolqnt .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#tgqkoolqnt .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 3px;
  padding-bottom: 5px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#tgqkoolqnt .gt_heading {
  background-color: #FFFFFF;
  text-align: center;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#tgqkoolqnt .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#tgqkoolqnt .gt_col_headings {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#tgqkoolqnt .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}

#tgqkoolqnt .gt_column_spanner_outer {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}

#tgqkoolqnt .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#tgqkoolqnt .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#tgqkoolqnt .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}

#tgqkoolqnt .gt_spanner_row {
  border-bottom-style: hidden;
}

#tgqkoolqnt .gt_group_heading {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  text-align: left;
}

#tgqkoolqnt .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: middle;
}

#tgqkoolqnt .gt_from_md > :first-child {
  margin-top: 0;
}

#tgqkoolqnt .gt_from_md > :last-child {
  margin-bottom: 0;
}

#tgqkoolqnt .gt_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#tgqkoolqnt .gt_stub {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
}

#tgqkoolqnt .gt_stub_row_group {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
  vertical-align: top;
}

#tgqkoolqnt .gt_row_group_first td {
  border-top-width: 2px;
}

#tgqkoolqnt .gt_row_group_first th {
  border-top-width: 2px;
}

#tgqkoolqnt .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#tgqkoolqnt .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#tgqkoolqnt .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#tgqkoolqnt .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#tgqkoolqnt .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#tgqkoolqnt .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#tgqkoolqnt .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#tgqkoolqnt .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#tgqkoolqnt .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#tgqkoolqnt .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#tgqkoolqnt .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#tgqkoolqnt .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#tgqkoolqnt .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#tgqkoolqnt .gt_left {
  text-align: left;
}

#tgqkoolqnt .gt_center {
  text-align: center;
}

#tgqkoolqnt .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#tgqkoolqnt .gt_font_normal {
  font-weight: normal;
}

#tgqkoolqnt .gt_font_bold {
  font-weight: bold;
}

#tgqkoolqnt .gt_font_italic {
  font-style: italic;
}

#tgqkoolqnt .gt_super {
  font-size: 65%;
}

#tgqkoolqnt .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#tgqkoolqnt .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#tgqkoolqnt .gt_indent_1 {
  text-indent: 5px;
}

#tgqkoolqnt .gt_indent_2 {
  text-indent: 10px;
}

#tgqkoolqnt .gt_indent_3 {
  text-indent: 15px;
}

#tgqkoolqnt .gt_indent_4 {
  text-indent: 20px;
}

#tgqkoolqnt .gt_indent_5 {
  text-indent: 25px;
}

#tgqkoolqnt .katex-display {
  display: inline-flex !important;
  margin-bottom: 0.75em !important;
}

#tgqkoolqnt div.Reactable > div.rt-table > div.rt-thead > div.rt-tr.rt-tr-group-header > div.rt-th-group:after {
  height: 0px !important;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <thead>
    <tr class="gt_heading">
      <td colspan="2" class="gt_heading gt_title gt_font_normal" style>Sample Stop Words</td>
    </tr>
    <tr class="gt_heading">
      <td colspan="2" class="gt_heading gt_subtitle gt_font_normal gt_bottom_border" style><span class='gt_from_md'>(dataset included in <code>tidytext</code>)</span></td>
    </tr>
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="word">word</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="lexicon">lexicon</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><td headers="word" class="gt_row gt_left">a</td>
<td headers="lexicon" class="gt_row gt_left">SMART</td></tr>
    <tr><td headers="word" class="gt_row gt_left">a's</td>
<td headers="lexicon" class="gt_row gt_left">SMART</td></tr>
    <tr><td headers="word" class="gt_row gt_left">able</td>
<td headers="lexicon" class="gt_row gt_left">SMART</td></tr>
    <tr><td headers="word" class="gt_row gt_left">about</td>
<td headers="lexicon" class="gt_row gt_left">SMART</td></tr>
    <tr><td headers="word" class="gt_row gt_left">above</td>
<td headers="lexicon" class="gt_row gt_left">SMART</td></tr>
    <tr><td headers="word" class="gt_row gt_left">according</td>
<td headers="lexicon" class="gt_row gt_left">SMART</td></tr>
    <tr><td headers="word" class="gt_row gt_left">accordingly</td>
<td headers="lexicon" class="gt_row gt_left">SMART</td></tr>
    <tr><td headers="word" class="gt_row gt_left">across</td>
<td headers="lexicon" class="gt_row gt_left">SMART</td></tr>
    <tr><td headers="word" class="gt_row gt_left">actually</td>
<td headers="lexicon" class="gt_row gt_left">SMART</td></tr>
    <tr><td headers="word" class="gt_row gt_left">after</td>
<td headers="lexicon" class="gt_row gt_left">SMART</td></tr>
  </tbody>
  
  
</table>
</div>
```
:::
:::

```{=html}
<aside class="notes">
```
-   TBD

```{=html}
</aside>
```
## Filtered word count

::: {style="display:table;width:100%;table-layout:fixed;"}
::: {style="display:table-cell;width:60%;padding-right:5%;text-align:left;vertical-align:top;"}
``` r
library(gutenbergr)
library(dplyr)
library(tidytext)

# get "mystery" text
book <- gutenberg_download(c(244))

# tidy the text into individual words
# also lowercases and removes punctuation
tidy_book <- book %>%
  unnest_tokens(output = word, input = text)

# remove stopwords 
# (lexicon provided with tidytext)
word_count_filtered <- tidy_book %>%
  anti_join(stop_words) %>%
  count(word, sort = TRUE)
```
:::

::: {style="display:table-cell;width:40%;padding-left:5%;text-align:left;vertical-align:top;"}
```{=html}
<div id="clarrzzmgo" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>#clarrzzmgo table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#clarrzzmgo thead, #clarrzzmgo tbody, #clarrzzmgo tfoot, #clarrzzmgo tr, #clarrzzmgo td, #clarrzzmgo th {
  border-style: none;
}

#clarrzzmgo p {
  margin: 0;
  padding: 0;
}

#clarrzzmgo .gt_table {
  display: table;
  border-collapse: collapse;
  line-height: normal;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #A8A8A8;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #A8A8A8;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}

#clarrzzmgo .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#clarrzzmgo .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#clarrzzmgo .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 3px;
  padding-bottom: 5px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#clarrzzmgo .gt_heading {
  background-color: #FFFFFF;
  text-align: center;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#clarrzzmgo .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#clarrzzmgo .gt_col_headings {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#clarrzzmgo .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}

#clarrzzmgo .gt_column_spanner_outer {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}

#clarrzzmgo .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#clarrzzmgo .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#clarrzzmgo .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}

#clarrzzmgo .gt_spanner_row {
  border-bottom-style: hidden;
}

#clarrzzmgo .gt_group_heading {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  text-align: left;
}

#clarrzzmgo .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: middle;
}

#clarrzzmgo .gt_from_md > :first-child {
  margin-top: 0;
}

#clarrzzmgo .gt_from_md > :last-child {
  margin-bottom: 0;
}

#clarrzzmgo .gt_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#clarrzzmgo .gt_stub {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
}

#clarrzzmgo .gt_stub_row_group {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
  vertical-align: top;
}

#clarrzzmgo .gt_row_group_first td {
  border-top-width: 2px;
}

#clarrzzmgo .gt_row_group_first th {
  border-top-width: 2px;
}

#clarrzzmgo .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#clarrzzmgo .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#clarrzzmgo .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#clarrzzmgo .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#clarrzzmgo .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#clarrzzmgo .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#clarrzzmgo .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#clarrzzmgo .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#clarrzzmgo .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#clarrzzmgo .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#clarrzzmgo .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#clarrzzmgo .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#clarrzzmgo .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#clarrzzmgo .gt_left {
  text-align: left;
}

#clarrzzmgo .gt_center {
  text-align: center;
}

#clarrzzmgo .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#clarrzzmgo .gt_font_normal {
  font-weight: normal;
}

#clarrzzmgo .gt_font_bold {
  font-weight: bold;
}

#clarrzzmgo .gt_font_italic {
  font-style: italic;
}

#clarrzzmgo .gt_super {
  font-size: 65%;
}

#clarrzzmgo .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#clarrzzmgo .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#clarrzzmgo .gt_indent_1 {
  text-indent: 5px;
}

#clarrzzmgo .gt_indent_2 {
  text-indent: 10px;
}

#clarrzzmgo .gt_indent_3 {
  text-indent: 15px;
}

#clarrzzmgo .gt_indent_4 {
  text-indent: 20px;
}

#clarrzzmgo .gt_indent_5 {
  text-indent: 25px;
}

#clarrzzmgo .katex-display {
  display: inline-flex !important;
  margin-bottom: 0.75em !important;
}

#clarrzzmgo div.Reactable > div.rt-table > div.rt-thead > div.rt-tr.rt-tr-group-header > div.rt-th-group:after {
  height: 0px !important;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <thead>
    <tr class="gt_heading">
      <td colspan="2" class="gt_heading gt_title gt_font_normal" style>Mystery Book Word Count</td>
    </tr>
    <tr class="gt_heading">
      <td colspan="2" class="gt_heading gt_subtitle gt_font_normal gt_bottom_border" style><span class='gt_from_md'>(10 most frequent terms <strong>without stopwords</strong>)</span></td>
    </tr>
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="word">word</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="n">n</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><td headers="word" class="gt_row gt_left">holmes</td>
<td headers="n" class="gt_row gt_right">97</td></tr>
    <tr><td headers="word" class="gt_row gt_left">time</td>
<td headers="n" class="gt_row gt_right">77</td></tr>
    <tr><td headers="word" class="gt_row gt_left">answered</td>
<td headers="n" class="gt_row gt_right">59</td></tr>
    <tr><td headers="word" class="gt_row gt_left">eyes</td>
<td headers="n" class="gt_row gt_right">59</td></tr>
    <tr><td headers="word" class="gt_row gt_left">hand</td>
<td headers="n" class="gt_row gt_right">57</td></tr>
    <tr><td headers="word" class="gt_row gt_left">ferrier</td>
<td headers="n" class="gt_row gt_right">56</td></tr>
    <tr><td headers="word" class="gt_row gt_left">found</td>
<td headers="n" class="gt_row gt_right">55</td></tr>
    <tr><td headers="word" class="gt_row gt_left">hope</td>
<td headers="n" class="gt_row gt_right">55</td></tr>
    <tr><td headers="word" class="gt_row gt_left">drebber</td>
<td headers="n" class="gt_row gt_right">53</td></tr>
    <tr><td headers="word" class="gt_row gt_left">sherlock</td>
<td headers="n" class="gt_row gt_right">52</td></tr>
  </tbody>
  
  
</table>
</div>
```
:::
:::

## Tokens can be more than words

::: {style="display:table;width:100%;table-layout:fixed;"}
::: {style="display:table-cell;width:70%;padding-right:5%;text-align:left;vertical-align:top;"}
``` r
library(gutenbergr)
library(dplyr)
library(tidytext)

# get "mystery" text
book <- gutenberg_download(c(244))

# ngrams as tokens
tidy_ngrams <- book %>%
  unnest_tokens(bigram, text, token = "ngrams", n = 2) %>%
  filter(!is.na(bigram)) %>%
  count(bigram, sort = TRUE)
```
:::

::: {style="display:table-cell;width:30%;padding-left:5%;text-align:left;vertical-align:top;"}
```{=html}
<div id="kevmdiwshv" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>#kevmdiwshv table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#kevmdiwshv thead, #kevmdiwshv tbody, #kevmdiwshv tfoot, #kevmdiwshv tr, #kevmdiwshv td, #kevmdiwshv th {
  border-style: none;
}

#kevmdiwshv p {
  margin: 0;
  padding: 0;
}

#kevmdiwshv .gt_table {
  display: table;
  border-collapse: collapse;
  line-height: normal;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #A8A8A8;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #A8A8A8;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}

#kevmdiwshv .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#kevmdiwshv .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#kevmdiwshv .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 3px;
  padding-bottom: 5px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#kevmdiwshv .gt_heading {
  background-color: #FFFFFF;
  text-align: center;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#kevmdiwshv .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#kevmdiwshv .gt_col_headings {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#kevmdiwshv .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}

#kevmdiwshv .gt_column_spanner_outer {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}

#kevmdiwshv .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#kevmdiwshv .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#kevmdiwshv .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}

#kevmdiwshv .gt_spanner_row {
  border-bottom-style: hidden;
}

#kevmdiwshv .gt_group_heading {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  text-align: left;
}

#kevmdiwshv .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: middle;
}

#kevmdiwshv .gt_from_md > :first-child {
  margin-top: 0;
}

#kevmdiwshv .gt_from_md > :last-child {
  margin-bottom: 0;
}

#kevmdiwshv .gt_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#kevmdiwshv .gt_stub {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
}

#kevmdiwshv .gt_stub_row_group {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
  vertical-align: top;
}

#kevmdiwshv .gt_row_group_first td {
  border-top-width: 2px;
}

#kevmdiwshv .gt_row_group_first th {
  border-top-width: 2px;
}

#kevmdiwshv .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#kevmdiwshv .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#kevmdiwshv .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#kevmdiwshv .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#kevmdiwshv .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#kevmdiwshv .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#kevmdiwshv .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#kevmdiwshv .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#kevmdiwshv .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#kevmdiwshv .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#kevmdiwshv .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#kevmdiwshv .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#kevmdiwshv .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#kevmdiwshv .gt_left {
  text-align: left;
}

#kevmdiwshv .gt_center {
  text-align: center;
}

#kevmdiwshv .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#kevmdiwshv .gt_font_normal {
  font-weight: normal;
}

#kevmdiwshv .gt_font_bold {
  font-weight: bold;
}

#kevmdiwshv .gt_font_italic {
  font-style: italic;
}

#kevmdiwshv .gt_super {
  font-size: 65%;
}

#kevmdiwshv .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#kevmdiwshv .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#kevmdiwshv .gt_indent_1 {
  text-indent: 5px;
}

#kevmdiwshv .gt_indent_2 {
  text-indent: 10px;
}

#kevmdiwshv .gt_indent_3 {
  text-indent: 15px;
}

#kevmdiwshv .gt_indent_4 {
  text-indent: 20px;
}

#kevmdiwshv .gt_indent_5 {
  text-indent: 25px;
}

#kevmdiwshv .katex-display {
  display: inline-flex !important;
  margin-bottom: 0.75em !important;
}

#kevmdiwshv div.Reactable > div.rt-table > div.rt-thead > div.rt-tr.rt-tr-group-header > div.rt-th-group:after {
  height: 0px !important;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <thead>
    <tr class="gt_heading">
      <td colspan="2" class="gt_heading gt_title gt_font_normal" style><span class='gt_from_md'>Mystery Book <em>n-gram</em> Count</span></td>
    </tr>
    <tr class="gt_heading">
      <td colspan="2" class="gt_heading gt_subtitle gt_font_normal gt_bottom_border" style><span class='gt_from_md'>(10 most frequent terms)</span></td>
    </tr>
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="bigram">bigram</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="n">n</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><td headers="bigram" class="gt_row gt_left">of the</td>
<td headers="n" class="gt_row gt_right">294</td></tr>
    <tr><td headers="bigram" class="gt_row gt_left">in the</td>
<td headers="n" class="gt_row gt_right">200</td></tr>
    <tr><td headers="bigram" class="gt_row gt_left">to the</td>
<td headers="n" class="gt_row gt_right">125</td></tr>
    <tr><td headers="bigram" class="gt_row gt_left">to be</td>
<td headers="n" class="gt_row gt_right">92</td></tr>
    <tr><td headers="bigram" class="gt_row gt_left">it was</td>
<td headers="n" class="gt_row gt_right">91</td></tr>
    <tr><td headers="bigram" class="gt_row gt_left">he had</td>
<td headers="n" class="gt_row gt_right">87</td></tr>
    <tr><td headers="bigram" class="gt_row gt_left">and the</td>
<td headers="n" class="gt_row gt_right">84</td></tr>
    <tr><td headers="bigram" class="gt_row gt_left">upon the</td>
<td headers="n" class="gt_row gt_right">80</td></tr>
    <tr><td headers="bigram" class="gt_row gt_left">at the</td>
<td headers="n" class="gt_row gt_right">79</td></tr>
    <tr><td headers="bigram" class="gt_row gt_left">he was</td>
<td headers="n" class="gt_row gt_right">79</td></tr>
  </tbody>
  
  
</table>
</div>
```
:::
:::

```{=html}
<aside class="notes">
```
-   typically, in text analysis, individual words are used as tokens
-   but what constitutes a relevant basic unit of information can vary
-   sometimes, n-grams (multiple successive words) could be the tokens
    to analyse

```{=html}
</aside>
```
## "The game's afoot ..."

::: {style="display:table;width:100%;table-layout:fixed;"}
::: {style="display:table-cell;width:70%;padding-right:5%;text-align:left;vertical-align:top;"}
``` r
library(gutenbergr)
library(dplyr)
library(tidytext)

# get "mystery" text
book <- gutenberg_download(c(244))

# ngrams as tokens (stop words filtered)
tidy_ngrams_filtered <- book %>%
  unnest_tokens(bigram, text, token = "ngrams", n = 2) %>%
  filter(!is.na(bigram)) %>%
  tidyr::separate(bigram, c("token1", "token2"), sep = " ") %>%
  anti_join(by = c("token1" = "word"), stop_words) %>%
  anti_join(by = c("token2" = "word"), stop_words) %>%
  tidyr::unite(bigram, token1, token2, sep = " ")

bigram_count <- tidy_ngrams_filtered %>%
  count(bigram, sort = TRUE)
```
:::

::: {style="display:table-cell;width:30%;padding-left:5%;text-align:left;vertical-align:top;"}
```{=html}
<div id="orxoytghzr" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>#orxoytghzr table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#orxoytghzr thead, #orxoytghzr tbody, #orxoytghzr tfoot, #orxoytghzr tr, #orxoytghzr td, #orxoytghzr th {
  border-style: none;
}

#orxoytghzr p {
  margin: 0;
  padding: 0;
}

#orxoytghzr .gt_table {
  display: table;
  border-collapse: collapse;
  line-height: normal;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #A8A8A8;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #A8A8A8;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}

#orxoytghzr .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#orxoytghzr .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#orxoytghzr .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 3px;
  padding-bottom: 5px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#orxoytghzr .gt_heading {
  background-color: #FFFFFF;
  text-align: center;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#orxoytghzr .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#orxoytghzr .gt_col_headings {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#orxoytghzr .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}

#orxoytghzr .gt_column_spanner_outer {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}

#orxoytghzr .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#orxoytghzr .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#orxoytghzr .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}

#orxoytghzr .gt_spanner_row {
  border-bottom-style: hidden;
}

#orxoytghzr .gt_group_heading {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  text-align: left;
}

#orxoytghzr .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: middle;
}

#orxoytghzr .gt_from_md > :first-child {
  margin-top: 0;
}

#orxoytghzr .gt_from_md > :last-child {
  margin-bottom: 0;
}

#orxoytghzr .gt_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#orxoytghzr .gt_stub {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
}

#orxoytghzr .gt_stub_row_group {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
  vertical-align: top;
}

#orxoytghzr .gt_row_group_first td {
  border-top-width: 2px;
}

#orxoytghzr .gt_row_group_first th {
  border-top-width: 2px;
}

#orxoytghzr .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#orxoytghzr .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#orxoytghzr .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#orxoytghzr .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#orxoytghzr .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#orxoytghzr .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#orxoytghzr .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#orxoytghzr .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#orxoytghzr .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#orxoytghzr .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#orxoytghzr .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#orxoytghzr .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#orxoytghzr .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#orxoytghzr .gt_left {
  text-align: left;
}

#orxoytghzr .gt_center {
  text-align: center;
}

#orxoytghzr .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#orxoytghzr .gt_font_normal {
  font-weight: normal;
}

#orxoytghzr .gt_font_bold {
  font-weight: bold;
}

#orxoytghzr .gt_font_italic {
  font-style: italic;
}

#orxoytghzr .gt_super {
  font-size: 65%;
}

#orxoytghzr .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#orxoytghzr .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#orxoytghzr .gt_indent_1 {
  text-indent: 5px;
}

#orxoytghzr .gt_indent_2 {
  text-indent: 10px;
}

#orxoytghzr .gt_indent_3 {
  text-indent: 15px;
}

#orxoytghzr .gt_indent_4 {
  text-indent: 20px;
}

#orxoytghzr .gt_indent_5 {
  text-indent: 25px;
}

#orxoytghzr .katex-display {
  display: inline-flex !important;
  margin-bottom: 0.75em !important;
}

#orxoytghzr div.Reactable > div.rt-table > div.rt-thead > div.rt-tr.rt-tr-group-header > div.rt-th-group:after {
  height: 0px !important;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <thead>
    <tr class="gt_heading">
      <td colspan="2" class="gt_heading gt_title gt_font_normal" style><span class='gt_from_md'>Mystery Book <em>n-gram</em> Count</span></td>
    </tr>
    <tr class="gt_heading">
      <td colspan="2" class="gt_heading gt_subtitle gt_font_normal gt_bottom_border" style><span class='gt_from_md'>(10 most frequent n-grams <br> <strong>without items containing a stop word</strong>)</span></td>
    </tr>
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="bigram">bigram</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="n">n</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><td headers="bigram" class="gt_row gt_left">sherlock holmes</td>
<td headers="n" class="gt_row gt_right">46</td></tr>
    <tr><td headers="bigram" class="gt_row gt_left">jefferson hope</td>
<td headers="n" class="gt_row gt_right">31</td></tr>
    <tr><td headers="bigram" class="gt_row gt_left">john ferrier</td>
<td headers="n" class="gt_row gt_right">23</td></tr>
    <tr><td headers="bigram" class="gt_row gt_left">brixton road</td>
<td headers="n" class="gt_row gt_right">11</td></tr>
    <tr><td headers="bigram" class="gt_row gt_left">salt lake</td>
<td headers="n" class="gt_row gt_right">10</td></tr>
    <tr><td headers="bigram" class="gt_row gt_left">lake city</td>
<td headers="n" class="gt_row gt_right">9</td></tr>
    <tr><td headers="bigram" class="gt_row gt_left">joseph stangerson</td>
<td headers="n" class="gt_row gt_right">7</td></tr>
    <tr><td headers="bigram" class="gt_row gt_left">lucy ferrier</td>
<td headers="n" class="gt_row gt_right">7</td></tr>
    <tr><td headers="bigram" class="gt_row gt_left">baker street</td>
<td headers="n" class="gt_row gt_right">6</td></tr>
    <tr><td headers="bigram" class="gt_row gt_left">private hotel</td>
<td headers="n" class="gt_row gt_right">6</td></tr>
  </tbody>
  
  
</table>
</div>
```
:::
:::

```{=html}
<aside class="notes">
```
-   typically, in text analysis, individual words are used as tokens
-   but what constitutes a relevant basic unit of information can vary
-   sometimes, n-grams (multiple successive words) could be the tokens
    to analyse

```{=html}
</aside>
```
## Further options: Sentiment Analysis

```{=html}
<div id="odxatltlbl" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>#odxatltlbl table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#odxatltlbl thead, #odxatltlbl tbody, #odxatltlbl tfoot, #odxatltlbl tr, #odxatltlbl td, #odxatltlbl th {
  border-style: none;
}

#odxatltlbl p {
  margin: 0;
  padding: 0;
}

#odxatltlbl .gt_table {
  display: table;
  border-collapse: collapse;
  line-height: normal;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #A8A8A8;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #A8A8A8;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}

#odxatltlbl .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#odxatltlbl .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#odxatltlbl .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 3px;
  padding-bottom: 5px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#odxatltlbl .gt_heading {
  background-color: #FFFFFF;
  text-align: center;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#odxatltlbl .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#odxatltlbl .gt_col_headings {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#odxatltlbl .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}

#odxatltlbl .gt_column_spanner_outer {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}

#odxatltlbl .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#odxatltlbl .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#odxatltlbl .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}

#odxatltlbl .gt_spanner_row {
  border-bottom-style: hidden;
}

#odxatltlbl .gt_group_heading {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  text-align: left;
}

#odxatltlbl .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: middle;
}

#odxatltlbl .gt_from_md > :first-child {
  margin-top: 0;
}

#odxatltlbl .gt_from_md > :last-child {
  margin-bottom: 0;
}

#odxatltlbl .gt_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#odxatltlbl .gt_stub {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
}

#odxatltlbl .gt_stub_row_group {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
  vertical-align: top;
}

#odxatltlbl .gt_row_group_first td {
  border-top-width: 2px;
}

#odxatltlbl .gt_row_group_first th {
  border-top-width: 2px;
}

#odxatltlbl .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#odxatltlbl .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#odxatltlbl .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#odxatltlbl .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#odxatltlbl .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#odxatltlbl .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#odxatltlbl .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#odxatltlbl .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#odxatltlbl .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#odxatltlbl .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#odxatltlbl .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#odxatltlbl .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#odxatltlbl .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#odxatltlbl .gt_left {
  text-align: left;
}

#odxatltlbl .gt_center {
  text-align: center;
}

#odxatltlbl .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#odxatltlbl .gt_font_normal {
  font-weight: normal;
}

#odxatltlbl .gt_font_bold {
  font-weight: bold;
}

#odxatltlbl .gt_font_italic {
  font-style: italic;
}

#odxatltlbl .gt_super {
  font-size: 65%;
}

#odxatltlbl .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#odxatltlbl .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#odxatltlbl .gt_indent_1 {
  text-indent: 5px;
}

#odxatltlbl .gt_indent_2 {
  text-indent: 10px;
}

#odxatltlbl .gt_indent_3 {
  text-indent: 15px;
}

#odxatltlbl .gt_indent_4 {
  text-indent: 20px;
}

#odxatltlbl .gt_indent_5 {
  text-indent: 25px;
}

#odxatltlbl .katex-display {
  display: inline-flex !important;
  margin-bottom: 0.75em !important;
}

#odxatltlbl div.Reactable > div.rt-table > div.rt-thead > div.rt-tr.rt-tr-group-header > div.rt-th-group:after {
  height: 0px !important;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <thead>
    <tr class="gt_heading">
      <td colspan="2" class="gt_heading gt_title gt_font_normal" style><span class='gt_from_md'>Sentiment words and valence</span></td>
    </tr>
    <tr class="gt_heading">
      <td colspan="2" class="gt_heading gt_subtitle gt_font_normal gt_bottom_border" style><span class='gt_from_md'><em>AFINN sentiment dictionary</em></span></td>
    </tr>
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="word">word</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="value">value</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><td headers="word" class="gt_row gt_left">supports</td>
<td headers="value" class="gt_row gt_right">2</td></tr>
    <tr><td headers="word" class="gt_row gt_left">encouraged</td>
<td headers="value" class="gt_row gt_right">2</td></tr>
    <tr><td headers="word" class="gt_row gt_left">lurk</td>
<td headers="value" class="gt_row gt_right">-1</td></tr>
    <tr><td headers="word" class="gt_row gt_left">irritating</td>
<td headers="value" class="gt_row gt_right">-3</td></tr>
    <tr><td headers="word" class="gt_row gt_left">woo</td>
<td headers="value" class="gt_row gt_right">3</td></tr>
    <tr><td headers="word" class="gt_row gt_left">medal</td>
<td headers="value" class="gt_row gt_right">3</td></tr>
    <tr><td headers="word" class="gt_row gt_left">sincere</td>
<td headers="value" class="gt_row gt_right">2</td></tr>
    <tr><td headers="word" class="gt_row gt_left">invincible</td>
<td headers="value" class="gt_row gt_right">2</td></tr>
    <tr><td headers="word" class="gt_row gt_left">sorrow</td>
<td headers="value" class="gt_row gt_right">-2</td></tr>
    <tr><td headers="word" class="gt_row gt_left">lovelies</td>
<td headers="value" class="gt_row gt_right">3</td></tr>
  </tbody>
  
  
</table>
</div>
```
## Frequent sentiment words

::: {style="display:table;width:100%;table-layout:fixed;"}
::: {style="display:table-cell;width:70%;padding-right:5%;text-align:left;vertical-align:top;"}
``` r
library(gutenbergr)
library(dplyr)
library(tidytext)

# get text
book <- gutenberg_download(c(244))

# index line numbers and tidy
tidy_book_indexed <- book %>%
  mutate(line = row_number()) %>%
  unnest_tokens(word, text)

# get a sentiment dictionary
afinn_dict <- get_sentiments("afinn")

# most frequent words that overlap
# with the AFINN sentiment dictionary
sentiment_count <- tidy_book_indexed %>%
  anti_join(stop_words) %>%
  count(word, sort = TRUE) %>%
  inner_join(afinn_dict)
```
:::

::: {style="display:table-cell;width:30%;padding-left:5%;text-align:left;vertical-align:top;"}
```{=html}
<div id="wsbrzycwlg" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>#wsbrzycwlg table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#wsbrzycwlg thead, #wsbrzycwlg tbody, #wsbrzycwlg tfoot, #wsbrzycwlg tr, #wsbrzycwlg td, #wsbrzycwlg th {
  border-style: none;
}

#wsbrzycwlg p {
  margin: 0;
  padding: 0;
}

#wsbrzycwlg .gt_table {
  display: table;
  border-collapse: collapse;
  line-height: normal;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #A8A8A8;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #A8A8A8;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}

#wsbrzycwlg .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#wsbrzycwlg .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#wsbrzycwlg .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 3px;
  padding-bottom: 5px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#wsbrzycwlg .gt_heading {
  background-color: #FFFFFF;
  text-align: center;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#wsbrzycwlg .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#wsbrzycwlg .gt_col_headings {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#wsbrzycwlg .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}

#wsbrzycwlg .gt_column_spanner_outer {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}

#wsbrzycwlg .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#wsbrzycwlg .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#wsbrzycwlg .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}

#wsbrzycwlg .gt_spanner_row {
  border-bottom-style: hidden;
}

#wsbrzycwlg .gt_group_heading {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  text-align: left;
}

#wsbrzycwlg .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: middle;
}

#wsbrzycwlg .gt_from_md > :first-child {
  margin-top: 0;
}

#wsbrzycwlg .gt_from_md > :last-child {
  margin-bottom: 0;
}

#wsbrzycwlg .gt_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#wsbrzycwlg .gt_stub {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
}

#wsbrzycwlg .gt_stub_row_group {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
  vertical-align: top;
}

#wsbrzycwlg .gt_row_group_first td {
  border-top-width: 2px;
}

#wsbrzycwlg .gt_row_group_first th {
  border-top-width: 2px;
}

#wsbrzycwlg .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#wsbrzycwlg .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#wsbrzycwlg .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#wsbrzycwlg .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#wsbrzycwlg .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#wsbrzycwlg .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#wsbrzycwlg .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#wsbrzycwlg .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#wsbrzycwlg .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#wsbrzycwlg .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#wsbrzycwlg .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#wsbrzycwlg .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#wsbrzycwlg .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#wsbrzycwlg .gt_left {
  text-align: left;
}

#wsbrzycwlg .gt_center {
  text-align: center;
}

#wsbrzycwlg .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#wsbrzycwlg .gt_font_normal {
  font-weight: normal;
}

#wsbrzycwlg .gt_font_bold {
  font-weight: bold;
}

#wsbrzycwlg .gt_font_italic {
  font-style: italic;
}

#wsbrzycwlg .gt_super {
  font-size: 65%;
}

#wsbrzycwlg .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#wsbrzycwlg .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#wsbrzycwlg .gt_indent_1 {
  text-indent: 5px;
}

#wsbrzycwlg .gt_indent_2 {
  text-indent: 10px;
}

#wsbrzycwlg .gt_indent_3 {
  text-indent: 15px;
}

#wsbrzycwlg .gt_indent_4 {
  text-indent: 20px;
}

#wsbrzycwlg .gt_indent_5 {
  text-indent: 25px;
}

#wsbrzycwlg .katex-display {
  display: inline-flex !important;
  margin-bottom: 0.75em !important;
}

#wsbrzycwlg div.Reactable > div.rt-table > div.rt-thead > div.rt-tr.rt-tr-group-header > div.rt-th-group:after {
  height: 0px !important;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <thead>
    <tr class="gt_heading">
      <td colspan="3" class="gt_heading gt_title gt_font_normal" style><span class='gt_from_md'>Sentiment word count</span></td>
    </tr>
    <tr class="gt_heading">
      <td colspan="3" class="gt_heading gt_subtitle gt_font_normal gt_bottom_border" style><span class='gt_from_md'>(10 most frequent words overlapping <br> with the AFINN dictionary)</span></td>
    </tr>
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="word">word</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="n">n</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="value">value</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><td headers="word" class="gt_row gt_left">hope</td>
<td headers="n" class="gt_row gt_right">55</td>
<td headers="value" class="gt_row gt_right">2</td></tr>
    <tr><td headers="word" class="gt_row gt_left">cried</td>
<td headers="n" class="gt_row gt_right">49</td>
<td headers="value" class="gt_row gt_right">-2</td></tr>
    <tr><td headers="word" class="gt_row gt_left">death</td>
<td headers="n" class="gt_row gt_right">29</td>
<td headers="value" class="gt_row gt_right">-2</td></tr>
    <tr><td headers="word" class="gt_row gt_left">matter</td>
<td headers="n" class="gt_row gt_right">29</td>
<td headers="value" class="gt_row gt_right">1</td></tr>
    <tr><td headers="word" class="gt_row gt_left">doubt</td>
<td headers="n" class="gt_row gt_right">19</td>
<td headers="value" class="gt_row gt_right">-1</td></tr>
    <tr><td headers="word" class="gt_row gt_left">terrible</td>
<td headers="n" class="gt_row gt_right">19</td>
<td headers="value" class="gt_row gt_right">-3</td></tr>
    <tr><td headers="word" class="gt_row gt_left">murder</td>
<td headers="n" class="gt_row gt_right">18</td>
<td headers="value" class="gt_row gt_right">-2</td></tr>
    <tr><td headers="word" class="gt_row gt_left">chance</td>
<td headers="n" class="gt_row gt_right">16</td>
<td headers="value" class="gt_row gt_right">2</td></tr>
    <tr><td headers="word" class="gt_row gt_left">leave</td>
<td headers="n" class="gt_row gt_right">16</td>
<td headers="value" class="gt_row gt_right">-1</td></tr>
    <tr><td headers="word" class="gt_row gt_left">crime</td>
<td headers="n" class="gt_row gt_right">15</td>
<td headers="value" class="gt_row gt_right">-3</td></tr>
  </tbody>
  
  
</table>
</div>
```
:::
:::

```{=html}
<aside class="notes">
```
-   typically, in text analysis, individual words are used as tokens
-   but what constitutes a relevant basic unit of information can vary
-   sometimes, n-grams (multiple successive words) could be the tokens
    to analyse

```{=html}
</aside>
```
## Sentiment trend

::: {style="display:table;width:100%;table-layout:fixed;"}
::: {style="display:table-cell;width:50%;padding-right:5%;text-align:left;vertical-align:top;"}
``` r
library(gutenbergr)
library(dplyr)
library(tidytext)

# get text
book <- gutenberg_download(c(244))

# index line numbers and tidy
tidy_book_indexed <- book %>%
  mutate(line = row_number()) %>%
  unnest_tokens(word, text)

# get a sentiment dictionary
afinn_dict <- get_sentiments("afinn")

# mean sentiment summarized for 
# blocks of 50 consecutive lines
sentiment_trend <- tidy_book_indexed %>%
  inner_join(afinn_dict) %>%
  group_by(index = line %/% 50) %>%
  summarise(mean_sentiment = mean(value)) %>%
  ungroup()

ggplot(sentiment_trend, 
       aes(x = index, 
           y = mean_sentiment)) +
  geom_point() +
  geom_smooth()
```
:::

::: {style="display:table-cell;width:50%;padding-left:5%;text-align:left;vertical-align:top;"}
![](figures/unnamed-chunk-16-1.png)
:::
:::

```{=html}
<aside class="notes">
```
-   typically, in text analysis, individual words are used as tokens
-   but what constitutes a relevant basic unit of information can vary
-   sometimes, n-grams (multiple successive words) could be the tokens
    to analyse

```{=html}
</aside>
```
# "Text as data" - Topic modeling

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

`<img src="figures/unnamed-chunk-28-1.png" width="80%" />`{=html}

## Choosing 'K'

`<img src="figures/unnamed-chunk-29-1.png" width="80%" />`{=html}

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

`<img src="figures/unnamed-chunk-31-1.png" width="70%" />`{=html}

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
`<img src="figures/unnamed-chunk-35-1.png" alt="**Word clouds showing the 50 most probable terms for selected topics.** *FREX* terms are highlighted in orange. Words are scaled by normalized probability." width="80%" />`{=html}
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
># (Intercept)             0.0234407  0.0036645   6.397 1.61e-10 ***
># servermedrxiv           0.1239526  0.0043286  28.635  < 2e-16 ***
># s(year)1               -0.0019515  0.0145159  -0.134    0.893    
># s(year)2               -0.0004803  0.0152775  -0.031    0.975    
># s(year)3                0.0083860  0.0066687   1.258    0.209    
># servermedrxiv:s(year)1 -0.0694334  0.0171247  -4.055 5.04e-05 ***
># servermedrxiv:s(year)2 -0.0969833  0.0188123  -5.155 2.55e-07 ***
># servermedrxiv:s(year)3 -0.0705812  0.0084963  -8.307  < 2e-16 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 2:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.098648   0.002868  34.397  < 2e-16 ***
># servermedrxiv          -0.085921   0.003141 -27.358  < 2e-16 ***
># s(year)1               -0.019924   0.011309  -1.762   0.0781 .  
># s(year)2               -0.011289   0.013474  -0.838   0.4022    
># s(year)3               -0.028559   0.004504  -6.341 2.31e-10 ***
># servermedrxiv:s(year)1  0.021647   0.012499   1.732   0.0833 .  
># servermedrxiv:s(year)2  0.008165   0.014540   0.562   0.5744    
># servermedrxiv:s(year)3  0.030352   0.005207   5.829 5.65e-09 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 3:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.011078   0.002826   3.920 8.88e-05 ***
># servermedrxiv           0.053936   0.003332  16.185  < 2e-16 ***
># s(year)1               -0.002506   0.011439  -0.219    0.827    
># s(year)2               -0.002071   0.011922  -0.174    0.862    
># s(year)3                0.001256   0.004921   0.255    0.799    
># servermedrxiv:s(year)1  0.014927   0.013813   1.081    0.280    
># servermedrxiv:s(year)2  0.014336   0.014996   0.956    0.339    
># servermedrxiv:s(year)3  0.029807   0.006580   4.530 5.92e-06 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 4:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.008830   0.003289   2.685  0.00726 ** 
># servermedrxiv           0.057751   0.003863  14.950  < 2e-16 ***
># s(year)1                0.004718   0.013405   0.352  0.72485    
># s(year)2               -0.005143   0.013937  -0.369  0.71212    
># s(year)3                0.004633   0.005840   0.793  0.42767    
># servermedrxiv:s(year)1  0.020380   0.016313   1.249  0.21155    
># servermedrxiv:s(year)2 -0.004009   0.017930  -0.224  0.82309    
># servermedrxiv:s(year)3  0.020160   0.007702   2.618  0.00886 ** 
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 5:
># 
># Coefficients:
>#                          Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.0049035  0.0023144   2.119   0.0341 *  
># servermedrxiv           0.0542977  0.0027664  19.628   <2e-16 ***
># s(year)1               -0.0006503  0.0094722  -0.069   0.9453    
># s(year)2                0.0001151  0.0099293   0.012   0.9908    
># s(year)3                0.0011266  0.0041297   0.273   0.7850    
># servermedrxiv:s(year)1  0.0259652  0.0115442   2.249   0.0245 *  
># servermedrxiv:s(year)2 -0.0017200  0.0121248  -0.142   0.8872    
># servermedrxiv:s(year)3 -0.0085353  0.0053101  -1.607   0.1080    
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 6:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.148624   0.003882  38.288  < 2e-16 ***
># servermedrxiv          -0.115790   0.004235 -27.340  < 2e-16 ***
># s(year)1               -0.021056   0.013387  -1.573    0.116    
># s(year)2               -0.049226   0.012216  -4.030 5.60e-05 ***
># s(year)3               -0.043747   0.006073  -7.204 6.00e-13 ***
># servermedrxiv:s(year)1  0.005838   0.014896   0.392    0.695    
># servermedrxiv:s(year)2  0.035441   0.013933   2.544    0.011 *  
># servermedrxiv:s(year)3  0.031012   0.007015   4.421 9.86e-06 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 7:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.010680   0.002926   3.650 0.000263 ***
># servermedrxiv           0.086062   0.003487  24.679  < 2e-16 ***
># s(year)1               -0.003909   0.011506  -0.340 0.734080    
># s(year)2               -0.007867   0.012217  -0.644 0.519618    
># s(year)3               -0.003318   0.005168  -0.642 0.520792    
># servermedrxiv:s(year)1 -0.049582   0.014410  -3.441 0.000581 ***
># servermedrxiv:s(year)2 -0.019418   0.015706  -1.236 0.216350    
># servermedrxiv:s(year)3 -0.038507   0.006511  -5.914 3.37e-09 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 8:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.027267   0.003029   9.002  < 2e-16 ***
># servermedrxiv           0.108677   0.003552  30.596  < 2e-16 ***
># s(year)1               -0.012967   0.012368  -1.048  0.29445    
># s(year)2               -0.018262   0.012496  -1.461  0.14389    
># s(year)3               -0.017113   0.005249  -3.260  0.00111 ** 
># servermedrxiv:s(year)1 -0.088311   0.014847  -5.948 2.74e-09 ***
># servermedrxiv:s(year)2 -0.046603   0.015412  -3.024  0.00250 ** 
># servermedrxiv:s(year)3 -0.060168   0.006563  -9.168  < 2e-16 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 9:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.170542   0.004583  37.214  < 2e-16 ***
># servermedrxiv          -0.164013   0.004822 -34.014  < 2e-16 ***
># s(year)1                0.017956   0.019097   0.940 0.347101    
># s(year)2               -0.034858   0.020080  -1.736 0.082589 .  
># s(year)3               -0.027961   0.006605  -4.234 2.31e-05 ***
># servermedrxiv:s(year)1 -0.010777   0.020193  -0.534 0.593547    
># servermedrxiv:s(year)2  0.033174   0.021835   1.519 0.128699    
># servermedrxiv:s(year)3  0.027934   0.007253   3.851 0.000118 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 10:
># 
># Coefficients:
>#                          Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.0447448  0.0033792  13.241  < 2e-16 ***
># servermedrxiv           0.0117800  0.0036441   3.233  0.00123 ** 
># s(year)1                0.0040881  0.0146475   0.279  0.78017    
># s(year)2                0.0002791  0.0132220   0.021  0.98316    
># s(year)3                0.0261924  0.0058626   4.468 7.94e-06 ***
># servermedrxiv:s(year)1 -0.0176398  0.0162261  -1.087  0.27699    
># servermedrxiv:s(year)2 -0.0305656  0.0153125  -1.996  0.04593 *  
># servermedrxiv:s(year)3 -0.0409802  0.0069928  -5.860 4.67e-09 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 11:
># 
># Coefficients:
>#                        Estimate Std. Error t value Pr(>|t|)    
># (Intercept)            0.005012   0.002335   2.146  0.03186 *  
># servermedrxiv          0.008240   0.002678   3.077  0.00209 ** 
># s(year)1               0.010115   0.009880   1.024  0.30594    
># s(year)2               0.010067   0.010118   0.995  0.31975    
># s(year)3               0.006453   0.004241   1.522  0.12812    
># servermedrxiv:s(year)1 0.056972   0.011657   4.887 1.03e-06 ***
># servermedrxiv:s(year)2 0.073704   0.012492   5.900 3.67e-09 ***
># servermedrxiv:s(year)3 0.047006   0.005929   7.928 2.31e-15 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 12:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.022052   0.002819   7.824 5.29e-15 ***
># servermedrxiv           0.041881   0.003371  12.426  < 2e-16 ***
># s(year)1               -0.008842   0.011210  -0.789    0.430    
># s(year)2               -0.005622   0.012082  -0.465    0.642    
># s(year)3               -0.002616   0.004868  -0.537    0.591    
># servermedrxiv:s(year)1 -0.006348   0.013943  -0.455    0.649    
># servermedrxiv:s(year)2  0.009307   0.015635   0.595    0.552    
># servermedrxiv:s(year)3  0.034816   0.006426   5.418 6.08e-08 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 13:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.104398   0.003117  33.496  < 2e-16 ***
># servermedrxiv          -0.086378   0.003397 -25.430  < 2e-16 ***
># s(year)1               -0.031523   0.015607  -2.020   0.0434 *  
># s(year)2               -0.028037   0.015271  -1.836   0.0664 .  
># s(year)3               -0.023362   0.005592  -4.178 2.95e-05 ***
># servermedrxiv:s(year)1  0.077683   0.018049   4.304 1.68e-05 ***
># servermedrxiv:s(year)2  0.028375   0.017039   1.665   0.0959 .  
># servermedrxiv:s(year)3  0.041145   0.006631   6.204 5.56e-10 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 14:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.124607   0.003412  36.517   <2e-16 ***
># servermedrxiv          -0.112711   0.003599 -31.314   <2e-16 ***
># s(year)1                0.004369   0.015197   0.287    0.774    
># s(year)2               -0.007735   0.015798  -0.490    0.624    
># s(year)3                0.007561   0.006391   1.183    0.237    
># servermedrxiv:s(year)1 -0.003295   0.016140  -0.204    0.838    
># servermedrxiv:s(year)2  0.005502   0.016927   0.325    0.745    
># servermedrxiv:s(year)3 -0.005135   0.007157  -0.717    0.473    
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 15:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.053486   0.003532  15.142  < 2e-16 ***
># servermedrxiv          -0.027430   0.004006  -6.847 7.67e-12 ***
># s(year)1                0.044430   0.014779   3.006  0.00265 ** 
># s(year)2                0.025174   0.015518   1.622  0.10475    
># s(year)3                0.017638   0.006515   2.707  0.00679 ** 
># servermedrxiv:s(year)1  0.003994   0.017358   0.230  0.81802    
># servermedrxiv:s(year)2  0.033148   0.017899   1.852  0.06404 .  
># servermedrxiv:s(year)3 -0.003244   0.007668  -0.423  0.67230    
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 16:
># 
># Coefficients:
>#                          Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.0531870  0.0034347  15.485  < 2e-16 ***
># servermedrxiv           0.0176184  0.0040149   4.388 1.15e-05 ***
># s(year)1               -0.0495144  0.0128988  -3.839 0.000124 ***
># s(year)2               -0.0295330  0.0132221  -2.234 0.025517 *  
># s(year)3               -0.0278692  0.0057471  -4.849 1.25e-06 ***
># servermedrxiv:s(year)1  0.0608967  0.0150494   4.046 5.21e-05 ***
># servermedrxiv:s(year)2  0.0011950  0.0159536   0.075 0.940291    
># servermedrxiv:s(year)3 -0.0007849  0.0072576  -0.108 0.913883    
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 17:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.012531   0.002374   5.278 1.32e-07 ***
># servermedrxiv          -0.010883   0.002662  -4.088 4.36e-05 ***
># s(year)1                0.062589   0.012022   5.206 1.94e-07 ***
># s(year)2                0.167240   0.016196  10.326  < 2e-16 ***
># s(year)3                0.074715   0.005313  14.063  < 2e-16 ***
># servermedrxiv:s(year)1 -0.043751   0.013524  -3.235  0.00122 ** 
># servermedrxiv:s(year)2 -0.080087   0.018163  -4.409 1.04e-05 ***
># servermedrxiv:s(year)3 -0.037854   0.006094  -6.212 5.30e-10 ***
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 18:
># 
># Coefficients:
>#                         Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.055699   0.003032  18.373  < 2e-16 ***
># servermedrxiv          -0.019893   0.003435  -5.792 7.03e-09 ***
># s(year)1                0.005625   0.012116   0.464   0.6425    
># s(year)2                0.004145   0.012803   0.324   0.7461    
># s(year)3                0.029398   0.005876   5.003 5.68e-07 ***
># servermedrxiv:s(year)1 -0.004554   0.014820  -0.307   0.7586    
># servermedrxiv:s(year)2 -0.004699   0.015468  -0.304   0.7613    
># servermedrxiv:s(year)3 -0.020694   0.006924  -2.989   0.0028 ** 
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 19:
># 
># Coefficients:
>#                          Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             0.0135210  0.0025707   5.260 1.45e-07 ***
># servermedrxiv           0.0273743  0.0030026   9.117  < 2e-16 ***
># s(year)1                0.0005909  0.0099153   0.060   0.9525    
># s(year)2               -0.0064213  0.0106165  -0.605   0.5453    
># s(year)3               -0.0030061  0.0043967  -0.684   0.4942    
># servermedrxiv:s(year)1 -0.0032021  0.0121320  -0.264   0.7918    
># servermedrxiv:s(year)2  0.0283350  0.0132190   2.144   0.0321 *  
># servermedrxiv:s(year)3  0.0026954  0.0057449   0.469   0.6389    
># ---
># Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
># 
># 
># Topic 20:
># 
># Coefficients:
>#                          Estimate Std. Error t value Pr(>|t|)    
># (Intercept)             6.731e-03  1.940e-03   3.470 0.000522 ***
># servermedrxiv           3.143e-02  2.200e-03  14.285  < 2e-16 ***
># s(year)1               -1.624e-03  7.666e-03  -0.212 0.832207    
># s(year)2               -1.816e-05  8.095e-03  -0.002 0.998210    
># s(year)3                4.609e-04  3.432e-03   0.134 0.893157    
># servermedrxiv:s(year)1  8.930e-03  9.542e-03   0.936 0.349355    
># servermedrxiv:s(year)2  1.271e-02  1.061e-02   1.199 0.230623    
># servermedrxiv:s(year)3  2.134e-02  4.632e-03   4.607 4.11e-06 ***
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

`<img src="figures/unnamed-chunk-38-1.png" width="70%" />`{=html}

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

`<img src="figures/unnamed-chunk-40-1.png" width="80%" />`{=html}

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

![](figures/unnamed-chunk-41-1.png)

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

![](figures/unnamed-chunk-42-1.png)

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

`<img src="figures/unnamed-chunk-43-1.png" width="70%" />`{=html}

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

`<img src="figures/unnamed-chunk-44-1.png" width="80%" />`{=html}

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

`<img src="figures/unnamed-chunk-45-1.png" width="80%" />`{=html}

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
