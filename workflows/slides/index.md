##   {#section .hideslideheader data-background="#061C30"}

::: {style="display:table;width:100%;table-layout: fixed;"}
::: {.title-without-logo style="display:table-cell;width:100%;padding-right:3%;padding-left:3%;vertical-align:middle;"}
SRC 2024 PhD course 'Data Science for Sustainable Development'

Reproducible Workflows using R Markdown, git and GitHub

 

 

 

 
:::
:::

::: {style="display:table;width:100%;table-layout: fixed;"}
::: {.mytitlepage .linksection style="display:table-cell;width:30%;padding-left:3%;vertical-align:bottom;"}
*[\@stefandaume](https://twitter.com/stefandaume)*

*<https://scitingly.net/>*

*<stefan.daume@su.se>*
:::

::: {.mytitlepage .authorsection style="display:table-cell;width:70%;padding-right:3%;"}
  **Stefan Daume**

*[Stockholm Resilience Centre, Stockholm
University](https://www.stockholmresilience.org/meet-our-team/staff/2021-01-27-daume.html)*

& *[Beijer Institute of Ecological
Economics](https://beijer.kva.se/programmes/complexity/)*

 

*22. November 2024*
:::
:::

```{=html}
<aside class="notes">
```
-   focus of this module is on two technologies and recipes for those
    that can be applied to data analysis, documentation and publishing
-   split in two parts: 1) providing an introduction to R Markdown
    and 2) an introduction to git/Github
-   an exercise to test the two together

```{=html}
</aside>
```
# Why learn R Markdown & git/Github?

## Key motivation

**Document** your analysis and enable **reproducibility** to follow
**Open Science** principles.

Avoid repetitive and error-prone tasks.

```{=html}
<aside class="notes">
```
-   you are the primary audience and beneficiary of these approaches,

-   but will at the same time adhere to principles of **open science**

-   two tools that allow to share your research in a transparent and
    reproducible way,

-   and make your life easier by structuring your research in a
    transparent and reproducible way

-   the combination of **R Markdown** and **git/GitHub** allows you to
    achieve these goals

```{=html}
</aside>
```
# (R) Markdown

## You should use R Markdown if you want to ...

> -   integrate and document your data analysis dynamically, not
>     statically
> -   concentrate on content rather than formatting
> -   share one document in many different formats (Markdown, PDF, Word,
>     HTML)
> -   ensure correct citations and bibliographies
> -   switch between different citation formats
> -   ... and much more

```{=html}
<aside class="notes">
```
-   the primary usecases for using R Markdown are:
    -   document your data science projects
    -   write publications based on the results of those projects

```{=html}
</aside>
```
## Markdown vs markup

**Markdown** allows us to concentrate on document structure and content.
We can then worry about styling and presentation later.

**Markdown** is a type of **markup language** (like HTML), but it is
lightweight and more readable.

```{=html}
<aside class="notes">
```
-   readability is key for markdown
-   there are different flavors of markdown but they largely share the
    same syntax
-   this presentation is in fact also based on a markdown document

```{=html}
</aside>
```
## Some text with simple formatting {#some-text-with-simple-formatting .left-aligned-slide}

This is a list:

-   with some **bold** and
-   some *italic* text.

And a [hyperlink](https://bookdown.org/yihui/rmarkdown/) for good
measure.

## Markup samples

::: {style="display:table;width:100%;table-layout:fixed;"}
::: {style="display:table-cell;width:50%;padding-left:1%;vertical-align:top;"}
**HTML**

    <p>This is a list:</p>
    <ul>
    <li>with some <strong>bold</strong> and</li>
    <li>some <em>italic</em> text.</li>
    </ul>
    <p>And a <a href="https://bookdown.org/yihui/rmarkdown/">hyperlink</a>
    for good measure.</p>
:::

::: {style="display:table-cell;width:50%;padding-right:1%;vertical-align:top;"}
**LaTeX**

    This is a list:

    \begin{itemize}
    \tightlist
    \item
      with some \textbf{bold} and
    \item
      some \emph{italic} text.
    \end{itemize}

    And a \href{https://bookdown.org/yihui/rmarkdown/}{hyperlink} for good
    measure.
:::
:::

```{=html}
<aside class="notes">
```
-   achieves the goal of separating content from presentation (although
    HTML is geared to jsut one presentation format),
-   but it is not very readable for a human reader (and thus editor)

```{=html}
</aside>
```
## The same with Markdown

```{=html}
<div style="display:table;width:100%;table-layout:fixed;">
```
::: {style="display:table-cell;width:50%;padding-left:1%;vertical-align:top;"}
**Basic Markdown**

    This is a list:

    * with some **bold** and 
    * some *italic* text.

    And a [hyperlink](https://bookdown.org/yihui/rmarkdown/) for good measure.
:::

## Typical workflow with markdown:

1.  **write** content as a Markdown document,
2.  **generate** the final document in a suitable output format
    (commonly HTML, PDF, Word)
3.  **publish**

```{=html}
<aside class="notes">
```
-   we will learn to use R Studio (1), R package knitr (2), and
    Github (3) to implement those steps

```{=html}
</aside>
```
# Essential markdown syntax

## File structure and conventions

-   Markdown files are **simple text files** and can be created with any
    text editor.
-   Markdown files typically end with the file extension **`.md`**

## Basic formatting and structuring

`<img src="./images/markdown_basic.jpg" width="1301" />`{=html}

## Lists and links

`<img src="./images/markdown_lists_links.jpg" width="1304" />`{=html}

## Even tables

`<img src="./images/markdown_tables.jpg" width="1302" />`{=html}

An overview of core markdown syntax can be found in [this R Markdown
book chapter](https://bookdown.org/yihui/rmarkdown/markdown-syntax.html)
and even more options in a condensed form as an [R Markdown cheat
sheet](https://raw.githubusercontent.com/rstudio/cheatsheets/main/rmarkdown.pdf).

```{=html}
<aside class="notes">
```
-   Tables (but now it gets complicated); show but then lead to R
    Markdown; use mtcars or similar
-   often table content is the result of data analysis, it could thus be
    dynamic and we may want to create it programmatically; this is where
    R Markdown makes an entry

```{=html}
</aside>
```
## 'R Markdown' vs 'Markdown'

-   Purpose: dynamically weave together text, data and analysis
    workflows.
-   This is accomplished with the [`knitr`](https://yihui.org/knitr/)
    package, an R package conveniently integrated into the R Studio UI.

## Differences to basic Markdown

-   R Markdown files use the file extension **`.Rmd`** instead of
    **`.md`**.
-   R Markdown files must start with a so-called **YAML header**
    section.
-   R Markdown files are still text files but R Studio should be used to
    work with those files efficiently.

## YAML - Yet Another Markup Language?

The **YAML header** must be placed at the beginning of a document and is
enclosed by three dashes `---`.

``` default
---
title: "Untitled"
output: html_document
date: '2024-11-22'
---
```

Above is the default *YAML header* when creating a new `R Markdown` file
in R Studio.

```{=html}
<aside class="notes">
```
-   see RMarkdown book for details
-   show the YAML header and explain; output format (default HTML,
    others are possible)

```{=html}
</aside>
```
## YAML Ain't Markup Language!

The **YAML header** contains meta-data (e.g. title, date, author(s) etc)
as well as information about the output format and style.

A YAML header with more options might look like this:

``` default
---
title: "R Course SRC"
subtitle: "Module 3"
date: "`r Sys.Date()`"
author: 'Stefan Daume' 
output: 
  html_document:
    toc: yes
bibliography: references.bib 
link-citations: yes
---
```

## Exercise

::: {style="display:table;width:100%;table-layout:fixed;"}
::: {style="display:table-cell;width:50%;padding-left:1%;text-align:left;vertical-align:middle;"}
1.  Create a default 'R Markdown' document in R Studio.
2.  "knit" the document to HTML and view the result.
3.  Use the **Knit** button to select different output formats and check
    the YAML header afterwards.
:::

::: {style="display:table-cell;width:50%;padding-right:1%;vertical-align:middle;"}
`<img src="./images/rstudio_knit.jpg" width="399" />`{=html}
:::
:::

```{=html}
<aside class="notes">
```
-   may have to [install
    TinyTeX](https://bookdown.org/yihui/rmarkdown-cookbook/install-latex.html)
    to get PDF to work #tinytex::install_tinytex()

-   pandoc is bundled, but may not be the latest; hence may need to
    install pandoc [see
    here](https://bookdown.org/yihui/rmarkdown-cookbook/install-pandoc.html)

-   check installed version #rmarkdown::find_pandoc()

```{=html}
</aside>
```
## R Markdown: data-driven documents

-   R Markdown allows to integrate your analysis as **R code** into the
    document
-   The analysis (i.e. the R code) is executed and the results updated
    when you **`knit`** the document.
-   Text and code are **interspersed**.
-   Code sections are included in **code chunks** like this.

```` default

```{r some-explanatory-label, eval=TRUE, echo=FALSE}
# here goes your R code
```
````

```{=html}
<aside class="notes">
```
`knitr`ing an R Markdown document means interpreting and executing the
included R code and generating an output document (in a chosen format)
that combines the text and results of the R computations.

Chunk options include, for example:

-   an **optional** label (can be used for references),
-   options controlling the output, such as figure size, caption,
    resolution
-   options controlling the execution of the output (you can disable the
    code chunk with `eval=FALSE` for example)

```{=html}
</aside>
```
## An example from the previous sessions

```` default
```{r life-expectancy, echo=FALSE, fig.cap="A figure caption."}
library(gapminder)

gapminder %>% 
    group_by(year) %>%
    summarise(ale = mean(lifeExp)) %>%
      ggplot(aes(x = year, y = ale)) +
        geom_line(color = "orange") +
        labs(x = "Year", 
             y = "Average life expectancy") +
        theme_classic(base_size = 16)
```
````

## Plots in R Markdown

::: {style="display:table;width:100%;table-layout:fixed;"}
::: {style="display:table-cell;width:50%;padding-left:1%;vertical-align:middle;"}
```` default
```{r life-expectancy, echo=FALSE}
library(gapminder)

gapminder %>% 
    group_by(year) %>%
    summarise(ale = mean(lifeExp)) %>%
    ggplot(aes(x = year, y = ale)) +
    geom_line(color = "orange") +
    labs(x = "Year", 
         y = "Average life expectancy") +
    theme_classic(base_size = 16)
```
````
:::

::: {style="display:table-cell;width:50%;padding-right:1%;vertical-align:middle;"}
![](index_files/figure-markdown/life-expectancy-1.png)
:::
:::

## Remember the Markdown table format?

`<img src="./images/markdown_tables.jpg" width="1302" />`{=html}

## Dynamic tables with R Markdown

::: {style="display:table;width:100%;table-layout:fixed;"}
::: {style="display:table-cell;width:50%;padding-right:5%;vertical-align:top;"}
**This code ...**

```` default
```{r}
# summarize gapminder data by continent
gapminder_latest <- gapminder %>% 
  filter(year == year_of_interest) %>%
  group_by(continent) %>%
  summarise(avrg_le = mean(lifeExp),
            avrg_gdp = mean(gdpPercap))
              
# print the results as a table
gapminder_latest %>%
  knitr::kable()
```
````
:::

::: {style="display:table-cell;width:50%;padding-left:5%;vertical-align:top;"}
**... creates this table:**

  continent      avrg_le    avrg_gdp
  ----------- ---------- -----------
  Africa        54.80604    3089.033
  Americas      73.60812   11003.032
  Asia          70.72848   12473.027
  Europe        77.64860   25054.482
  Oceania       80.71950   29810.188
:::
:::

## Customizing `kable` tables

::: {style="display:table;width:100%;table-layout:fixed;"}
::: {style="display:table-cell;width:50%;padding-right:5%;vertical-align:top;"}
**This code ...**

```` default
```{r}
# summarize gapminder data by continent
gapminder_latest <- gapminder %>% 
  filter(year == year_of_interest) %>%
  group_by(continent) %>%
  summarise(avrg_le = mean(lifeExp),
            avrg_gdp = mean(gdpPercap))
              
# print the results as a table
gapminder_latest %>%
  knitr::kable(digits = c(0,1,2))
```
````
:::

::: {style="display:table-cell;width:50%;padding-left:5%;vertical-align:top;"}
**... creates this table:**

  continent     avrg_le   avrg_gdp
  ----------- --------- ----------
  Africa           54.8    3089.03
  Americas         73.6   11003.03
  Asia             70.7   12473.03
  Europe           77.6   25054.48
  Oceania          80.7   29810.19
:::
:::

## More expressive tables with `kableExtra` or `gt`

The
[`kableExtra`](https://cran.r-project.org/web/packages/kableExtra/vignettes/awesome_table_in_html.html)
and [`gt`](https://gt.rstudio.com/index.html) packages offer even more
options:

-   data-driven colouring
-   interactive tables
-   grouped headers
-   tables with (interactive) sparklines
-   and more ...

## `kableExtra` example

```{=html}
<table class="table lightable-paper" style="font-size: 10px; color: black; margin-left: auto; margin-right: auto; color: black; font-family: &quot;Arial Narrow&quot;, arial, helvetica, sans-serif; width: auto !important; margin-left: auto; margin-right: auto;">
```
```{=html}
<caption style="font-size: initial !important;">
```
Table caption: Dynamic formatting with the the help of `kableExtra`.
This example shows Gapminder data summarised by continent for the year
2007.
```{=html}
</caption>
```
```{=html}
<thead>
```
```{=html}
<tr>
```
```{=html}
<th style="text-align:left;">
```
Continent
```{=html}
</th>
```
```{=html}
<th style="text-align:right;">
```
Mean life expectancy
```{=html}
</th>
```
```{=html}
<th style="text-align:right;">
```
Mean GDP
```{=html}
</th>
```
```{=html}
</tr>
```
```{=html}
</thead>
```
```{=html}
<tbody>
```
```{=html}
<tr>
```
```{=html}
<td style="text-align:left;">
```
Africa
```{=html}
</td>
```
```{=html}
<td style="text-align:right;">
```
54.8
```{=html}
</td>
```
```{=html}
<td style="text-align:right;color: white !important;background-color: rgba(68, 1, 84, 255) !important;">
```
3089.03
```{=html}
</td>
```
```{=html}
</tr>
```
```{=html}
<tr>
```
```{=html}
<td style="text-align:left;">
```
Americas
```{=html}
</td>
```
```{=html}
<td style="text-align:right;">
```
73.6
```{=html}
</td>
```
```{=html}
<td style="text-align:right;color: white !important;background-color: rgba(53, 95, 141, 255) !important;">
```
11003.03
```{=html}
</td>
```
```{=html}
</tr>
```
```{=html}
<tr>
```
```{=html}
<td style="text-align:left;">
```
Asia
```{=html}
</td>
```
```{=html}
<td style="text-align:right;">
```
70.7
```{=html}
</td>
```
```{=html}
<td style="text-align:right;color: white !important;background-color: rgba(46, 109, 142, 255) !important;">
```
12473.03
```{=html}
</td>
```
```{=html}
</tr>
```
```{=html}
<tr>
```
```{=html}
<td style="text-align:left;">
```
Europe
```{=html}
</td>
```
```{=html}
<td style="text-align:right;">
```
77.6
```{=html}
</td>
```
```{=html}
<td style="text-align:right;color: white !important;background-color: rgba(137, 213, 72, 255) !important;">
```
25054.48
```{=html}
</td>
```
```{=html}
</tr>
```
```{=html}
<tr>
```
```{=html}
<td style="text-align:left;">
```
Oceania
```{=html}
</td>
```
```{=html}
<td style="text-align:right;">
```
80.7
```{=html}
</td>
```
```{=html}
<td style="text-align:right;color: white !important;background-color: rgba(253, 231, 37, 255) !important;">
```
29810.19
```{=html}
</td>
```
```{=html}
</tr>
```
```{=html}
</tbody>
```
```{=html}
</table>
```
```{=html}
<aside class="notes">
```
-   `kableExtra` extends `kable()`

```{=html}
</aside>
```
## `gt` example

```{=html}
<div id="ryjyqhgvij" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>#ryjyqhgvij table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#ryjyqhgvij thead, #ryjyqhgvij tbody, #ryjyqhgvij tfoot, #ryjyqhgvij tr, #ryjyqhgvij td, #ryjyqhgvij th {
  border-style: none;
}

#ryjyqhgvij p {
  margin: 0;
  padding: 0;
}

#ryjyqhgvij .gt_table {
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

#ryjyqhgvij .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#ryjyqhgvij .gt_title {
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

#ryjyqhgvij .gt_subtitle {
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

#ryjyqhgvij .gt_heading {
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

#ryjyqhgvij .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#ryjyqhgvij .gt_col_headings {
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

#ryjyqhgvij .gt_col_heading {
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

#ryjyqhgvij .gt_column_spanner_outer {
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

#ryjyqhgvij .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#ryjyqhgvij .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#ryjyqhgvij .gt_column_spanner {
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

#ryjyqhgvij .gt_spanner_row {
  border-bottom-style: hidden;
}

#ryjyqhgvij .gt_group_heading {
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

#ryjyqhgvij .gt_empty_group_heading {
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

#ryjyqhgvij .gt_from_md > :first-child {
  margin-top: 0;
}

#ryjyqhgvij .gt_from_md > :last-child {
  margin-bottom: 0;
}

#ryjyqhgvij .gt_row {
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

#ryjyqhgvij .gt_stub {
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

#ryjyqhgvij .gt_stub_row_group {
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

#ryjyqhgvij .gt_row_group_first td {
  border-top-width: 2px;
}

#ryjyqhgvij .gt_row_group_first th {
  border-top-width: 2px;
}

#ryjyqhgvij .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#ryjyqhgvij .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#ryjyqhgvij .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#ryjyqhgvij .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#ryjyqhgvij .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#ryjyqhgvij .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#ryjyqhgvij .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#ryjyqhgvij .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#ryjyqhgvij .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#ryjyqhgvij .gt_footnotes {
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

#ryjyqhgvij .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#ryjyqhgvij .gt_sourcenotes {
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

#ryjyqhgvij .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#ryjyqhgvij .gt_left {
  text-align: left;
}

#ryjyqhgvij .gt_center {
  text-align: center;
}

#ryjyqhgvij .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#ryjyqhgvij .gt_font_normal {
  font-weight: normal;
}

#ryjyqhgvij .gt_font_bold {
  font-weight: bold;
}

#ryjyqhgvij .gt_font_italic {
  font-style: italic;
}

#ryjyqhgvij .gt_super {
  font-size: 65%;
}

#ryjyqhgvij .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#ryjyqhgvij .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#ryjyqhgvij .gt_indent_1 {
  text-indent: 5px;
}

#ryjyqhgvij .gt_indent_2 {
  text-indent: 10px;
}

#ryjyqhgvij .gt_indent_3 {
  text-indent: 15px;
}

#ryjyqhgvij .gt_indent_4 {
  text-indent: 20px;
}

#ryjyqhgvij .gt_indent_5 {
  text-indent: 25px;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <caption>Table caption: Dynamic formatting with the the help of the <code>gt</code> package. This example shows Gapminder data summarised by continent for the year 2007.</caption>
  <thead>
    
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1" scope="col" id="Continent">Continent</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Mean life expectancy">Mean life expectancy</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Mean GDP">Mean GDP</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><td headers="continent" class="gt_row gt_center">Africa</td>
<td headers="avrg_le" class="gt_row gt_right">54.8</td>
<td headers="avrg_gdp" class="gt_row gt_right" style="background-color: #EBF5F7;">3,089.03</td></tr>
    <tr><td headers="continent" class="gt_row gt_center">Americas</td>
<td headers="avrg_le" class="gt_row gt_right">73.6</td>
<td headers="avrg_gdp" class="gt_row gt_right" style="background-color: #B8DDE2;">11,003.03</td></tr>
    <tr><td headers="continent" class="gt_row gt_center">Asia</td>
<td headers="avrg_le" class="gt_row gt_right">70.7</td>
<td headers="avrg_gdp" class="gt_row gt_right" style="background-color: #AED9DE;">12,473.03</td></tr>
    <tr><td headers="continent" class="gt_row gt_center">Europe</td>
<td headers="avrg_le" class="gt_row gt_right">77.6</td>
<td headers="avrg_gdp" class="gt_row gt_right" style="background-color: #50B2BE;">25,054.48</td></tr>
    <tr><td headers="continent" class="gt_row gt_center">Oceania</td>
<td headers="avrg_le" class="gt_row gt_right">80.7</td>
<td headers="avrg_gdp" class="gt_row gt_right" style="background-color: #00A4B2;">29,810.19</td></tr>
  </tbody>
  
  
</table>
</div>
```
```{=html}
<aside class="notes">
```
-   gt is a standalone package, i.e., independent of `kable()`

```{=html}
</aside>
```
## Central 'Setup' code section

```` default
```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = FALSE)

library(readr)
library(dplyr)
library(ggplot2)
library(gapminder)

year_of_interest <- 2007
```
````

Simplify library import and prepare datasets for reference in the whole
document.

```{=html}
<aside class="notes">
```
-   this sets options for knitr that apply to the whole document
-   and allows to define variables that are accessible for all code
    chunks in the document

```{=html}
</aside>
```
# Handling citations

## Citations and bibliographies

One of the most useful and powerful features for researchers using R
Markdown.

```{=html}
<aside class="notes">
```
-   code chunks that create text, tables and figures dynamically allow
    to create dynamic data-driven documents
-   the ability to handle references and control formatting of citations
    and bibliographies allows to use R Markdown for your scientific
    publications

```{=html}
</aside>
```
## Requires a BibTeX database

A **BibTeX** database is simply a text file with the extension
**`.bib`** and entries such as:

    @misc{XieAllaire_et_2022,
      author = {Xie, Yihui and Allaire, J. J. and Grolemund, Garrett},
      title = {{R Markdown: The Definitive Guide}},
      url = {https://bookdown.org/yihui/rmarkdown/},
      urldate = {2022-06-07},
      year = {2022}
    }

No need to write those. Export from your reference manager or journal
pages.

```{=html}
<aside class="notes">
```
-   requires a ".bib" (BibTeX format) file of citations;
-   looks like this: ...
-   easy to export from the reference manager of your choice

```{=html}
</aside>
```
## Include citations

::: {style="display:table;width:100%;table-layout:fixed;"}
::: {style="display:table-cell;width:50%;padding-right:5%;text-align:left;vertical-align:top;"}
**Point to the `.bib` file in the YAML header.**

    ---
    title: "R Course SRC"
    subtitle: "Module 3"
    date: "2024-11-21"
    author: 'Stefan Daume' 
    output: 
      html_document:
        toc: yes
    bibliography: references.bib 
    link-citations: yes
    ---
:::

::: {style="display:table-cell;width:50%;padding-left:5%;text-align:left;vertical-align:top;"}
And then include citations in the text with the format
**`[@CitationKey]`**, which in the previously shown example was
**`[@XieAllaire_et_2022]`**, which is a reference to
[@XieAllaire_et_2022].
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
## Include a bibliography

By default a bibliography is added to the end of the generated (i.e.,
`knitr`ed) document.

``` default
After presenting all results we have now reached the end of the document. Here should follow the bibliography.

# References
```

Add the header `# References` at the end of your document, `knit` and
the complete bibliography is added to the output document.

```{=html}
<aside class="notes">
```
-   if a resource is referenced that is missing in the ".bib" file you
    will get an error
-   and only referenced resources will be included in the bibliography,
    even if the ".bib" file contains more resources

```{=html}
</aside>
```
## Switch citation and bibliography styles dynamically

::: {style="display:table;width:100%;table-layout:fixed;"}
::: {style="display:table-cell;width:50%;padding-right:5%;text-align:left;vertical-align:top;"}
**Specify citation style in the YAML header.**

    ---
    title: "R Course SRC"
    subtitle: "Module 3"
    date: "2024-11-21"
    author: 'Stefan Daume' 
    output: 
      html_document:
        toc: yes
    bibliography: references.bib 
    link-citations: yes
    csl: ecology-and-society.csl
    ---
:::

::: {style="display:table-cell;width:50%;padding-left:5%;text-align:left;vertical-align:top;"}
The **[Citation Style Database](https://www.zotero.org/styles)**
database contains thousands of journal [citation
styles](https://citationstyles.org/). Download the relevant one,
reference in the YAML header and the output document will have the
required citation style.
:::
:::

```{=html}
<aside class="notes">
```
-   now you `knit` and get ... pure magic!
-   goodbye to: incorrect citations, missing citations, incorrect
    bibliographies and wasted time
-   even better: switch styles dynamically for the target journal

```{=html}
</aside>
```
## Easy sharing and online publishing

1.  `knit` your R Markdown document to HTML
2.  push the HTML to Github (next part of this module)
3.  enable sharing of **Github Pages**

This is how this presentation works (and the others before).

## "Continous Analysis" as the ultimate goal

## Key Resources

-   R Markdown
    -   [R Markdown: The Definitive
        Guide](https://bookdown.org/yihui/rmarkdown/)
        [@XieAllaire_et_2022]
    -   [R Markdown
        Cookbook](https://bookdown.org/yihui/rmarkdown-cookbook/)
        [@XieDervieux_et_2024_BOOK]
    -   [Cheatsheet: Dynamic documents with rmarkdown
        cheatsheet](https://raw.githubusercontent.com/rstudio/cheatsheets/main/rmarkdown.pdf)

```{=html}
<aside class="notes">
```
-   R Markdown is a rich tool that supports a broad range of output
    formats

-   including interactive websites (R shiny apps)

-   allows for numerous customizations

-   even if you do not want to produce your final publication manuscript
    in R Markdown, it is advisable to at least support the analysis
    process in an R Markdown document and only move to another format
    and export static charts and/or tables to another writing tool

```{=html}
</aside>
```
# git & GitHub

## You need git and Github if ... (non-exhaustive list)

-   ... you have files like this, but realise that this is not efficient
    -   my_paper_draft_2021_05_16.docx
    -   my_paper_draft_2021_05_18.docx
    -   my_paper_draft_2021_05_19.docx
    -   my_paper_draft_2021_05_19_v1.docx
    -   my_paper_draft_2021_05_19_v2.docx
    -   my_paper_draft_2021_05_19_v3_with_comments.docx
-   ... you are not creating regular backups of your work
-   ... you want to collaborate with others
-   ... you want to maintain projects rather than a single file (Google
    Doc)
-   ... you want to be able to easily revert back to previous versions
    of your work

```{=html}
<aside class="notes">
```
-   here we move to the second element for reproducible workflows
-   complex analysis may go through multiple iterations, that you might
    want to track
-   you may also want to share your resources with others, or even allow
    them to collaborate on an analysis
-   and eventually want to publish your results online
-   here git & GitHub come into play

```{=html}
</aside>
```
## Focus of this session

git & GitHub are extremely versatile, feature-rich tools that enable
collaboration on complex software projects.

## Focus of this session

We will only scratch the surface and focus on basic recipes and
elements, namely:

-   understanding the basic idea behind `git`
-   use GitHub as a repository/backup for your work
-   integrate git/GitHub into your workflow with R Studio
-   share and collaborate with others

```{=html}
<aside class="notes">
```
-   thus it is about organising and reproducibility (for yourself and
    others as a target audience)

```{=html}
</aside>
```
## Key Resources

-   Git/Github:
    -   [Happy Git and GitHub for the useR](https://happygitwithr.com/)
        [@Bryan2021]
    -   "Excuse me, do you have a moment to talk about version control?"
        [@Bryan2017]
    -   Advanced git use: [Pro Git](https://git-scm.com/book/en/v2) book
        [@Chacon_et_2014_Book]
    -   [How to write a great commit
        message](https://cbea.ms/git-commit/)

```{=html}
<aside class="notes">
```
-   the examples follow these resources
-   for different recipes and advanced usage consult the [Pro
    Git](https://git-scm.com/book/en/v2) book [@Chacon_et_2014_Book] and
    [Happy Git and GitHub for the useR](https://happygitwithr.com/)

```{=html}
</aside>
```
## git history

-   Linux development, started 2005
-   a version management system, i.e. tracks changes in project
    resources
-   git takes snapshots of a managed project (image)
-   distributed version control system (that means you always have a
    complete copy of your version history on your local computer)

## Version control

`<img src="./images/local_versions.png" width="50%" />`{=html}

::: {style="display:table;width:100%;margin-top:0%;table-layout:fixed;"}
::: {.attribution-dark style="display:table-cell;width:100%;vertical-align:bottom;"}
`<a href="https://git-scm.com/book/en/v2/images/local.png">`{=html}Local
version control diagram`</a>`{=html}, in
`<a href="https://git-scm.com/book/en/v2">`{=html}Pro Git`</a>`{=html}
by Scott Chacon and Ben Straub, licensed under
`<a href="https://creativecommons.org/licenses/by-nc-sa/3.0/">`{=html}CC
BY-NC-SA 3.0`</a>`{=html}
:::
:::

## Versions as snapshots

`<img src="./images/version_snapshots.png" width="1674" height="50%" />`{=html}

::: {style="display:table;width:100%;margin-top:0%;table-layout:fixed;"}
::: {.attribution-dark style="display:table-cell;width:100%;vertical-align:bottom;"}
`<a href="https://git-scm.com/book/en/v2/images/snapshots.png">`{=html}Versions
as snapshots diagram`</a>`{=html}, in
`<a href="https://git-scm.com/book/en/v2">`{=html}Pro Git`</a>`{=html}
by Scott Chacon and Ben Straub, licensed under
`<a href="https://creativecommons.org/licenses/by-nc-sa/3.0/">`{=html}CC
BY-NC-SA 3.0`</a>`{=html}
:::
:::

## Centralized version control

Examples: CVS, Subversion

`<img src="./images/central_vcs.png" width="1280" height="70%" />`{=html}

## Distributed Version Control

`<img src="./images/dvcs_git.png" width="1280" height="70%" />`{=html}

## Distributed Version Control

`<img src="./images/dvcs_git_usage.png" width="1280" height="70%" />`{=html}

## GitHub as a hosted git repo

`<img src="./images/dvcs_github.png" width="1280" height="70%" />`{=html}

## Focus for today

`<img src="./images/dvcs_todays_session_focus.png" width="1280" height="70%" />`{=html}

## A simple git/GitHub usage scenario

-   create a project and **enable versioning** with `git`
-   connect it with a **remote copy** (for sharing and backup)
-   do work locally and track (**commit**) versions of your files
-   **push** your changes (sync **to** the remote copy on GitHub)
-   **pull** other's changes (sync **from** the remote copy on GitHub)

## Integrated into R Studio

`<img src="./images/rstudio_git_tab.png" width="504" />`{=html}

## Key concepts

-   repo
-   cloning
-   staging
-   commit
-   diff
-   push
-   pull
-   branch (advanced)
-   merge (advanced)
-   remote origin

# Setting git/GitHub up with R Studio

## Do this once:

-   sign up for a Github account
-   install git locally (see [@Bryan2021])
-   create a personal access token
    -   either via Github (<https://github.com/settings/tokens>)
    -   or via R with: `usethis::create_github_token()`
    -   and then store it with `gitcreds::gitcreds_set()`

## Installing and configuring git

Select the installer for your OS: <https://git-scm.com/>

On the command line set:

``` shell
$ git config --global user.name "JohnDoe"
$ git config --global user.email johndoe@example.com
```

Use the same username/email you use for your GitHub account!

Check your settings:

``` shell
$ git config --list
```

## Create a PAT (Personal Access Token)

You can go to GitHub directly or trigger it from the command line:

``` shell
usethis::create_github_token()
```

## Create a PAT (Personal Access Token)

Configure and create PAT:

`<img src="./images/github_pat_creation.png" width="1134" />`{=html}

```{=html}
<aside class="notes">
```
-   leave the standard scopes that are already selected

```{=html}
</aside>
```
## Create a PAT (Personal Access Token)

Than copy it:

`<img src="./images/github_pat_copy.png" width="1111" />`{=html}

## Store the PAT for local use

Set the credentials from the command line in R Studio:

``` shell
gitcreds::gitcreds_set()
```

Follow instructions and finally provide the PAT:

``` shell
? Enter new password or token: ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
-> Adding new credentials...
-> Removing credentials from cache...
-> Done.
```

## Alternative to PATs

You can also configure **SSH keys** to connect to GitHub.

Consult **[Set up keys for SSH](https://happygitwithr.com/ssh-keys)**
[@Bryan2021] to explore this option.

## Do this for every new project:

-   create a Github repo first (follow the [New project, Github
    first](https://happygitwithr.com/new-github-first.html) workflow in
    [@Bryan2021])
    -   Why? Its easiest! You have everything in place to create remote
        backups!
-   say yes to creating a README
-   copy the HTTPS link of your new repo
-   then create an R Studio project with the option from "Version
    control \> git"

## Create a new GitHub repo

-   In your GitHub profile go to **Repositories**, and press **"New"**.
-   Provide the repo information and press **"Create Repository"**.

`<img src="./images/github_create_repo.png" width="50%" />`{=html}

## Copy the repo URL

-   Go to **Repositories** and select the new repo.
-   Copy the HTTPS repo URL.

`<img src="./images/github_copy_repo_url.png" width="1112" />`{=html}

## Create an R Studio project with the repo

Create a new project via *File \> New Project \> Version Control \> Git*

`<img src="./images/rstudio_create_github_project.png" width="537" />`{=html}

## New project tracked with git

`<img src="./images/rstudio_git_tab.png" width="504" />`{=html}

## When your new project is set up

-   make a change to the `README.md` (a useful project description)
-   `commit` the changes of the README file
-   and `push` to the remote Github repo
-   check the Github repo

```{=html}
<aside class="notes">
```
-   Show a basic workflow
-   screenshots

```{=html}
</aside>
```
## Commit changes

`<img src="./images/rstudio_git_commit.png" width="986" />`{=html}

```{=html}
<aside class="notes">
```
-   once you have made a commit the changes are tracked/recorded in your
    local git repository

```{=html}
</aside>
```
## Push changes to remote GitHub repo

`<img src="./images/rstudio_git_push.png" width="1277" />`{=html}

## Publish your content

Repo content can be hosted online via GitHub pages.

```{=html}
<aside class="notes">
```
-   GitHub has a builtin feature that allow to publish content in a repo
    online
-   its called GitHub Pages

```{=html}
</aside>
```
## Enable GitHub pages for a repo

Go to *Settings \> Pages* and select *Branch \> main*

`<img src="./images/github_pages_settings.png" width="65%" />`{=html}

## One GitHub page per repo

Once enabled a site becomes available with the format:

`https://[GITHUB_USER].github.io/[REPO_NAME]/`

`<img src="./images/github_pages_link.png" width="65%" />`{=html}

## Deployed GitHub page

`<img src="./images/github_pages_deployed.png" width="65%" />`{=html}

By default either the README is served or the content of a file called
*index.html*, if it is available.

Alternatively, provide the filename in the URL, e.g.,
<https://sdaume.github.io/ds4sd-test/default.html>

# Useful to know for commits

## Not tracking resources

`.gitignore` allows to exclude resources from being tracked.

You may have sensitive files (e.g., pass keys, private data) that should
not end up in a public repo.

`<img src="./images/rstudio_git_ignore.png" width="50%" />`{=html}

## How to write a great commit comment {#how-to-write-a-great-commit-comment .left-aligned-slide}

Most important:

-   Keep things atomic!

Document consistently:

-   Keep the subject line short.
-   Use the imperative mood in the subject line (Because a commit
    message should always complete the following line: "If applied, this
    commit will \[YOUR_SUBJECT_LINE\].")
-   Use the body to explain what and why vs. how (Because "the how" can
    be obtained from the *diff*. The commit message should provide the
    context for "the how".)

# Exercises

## Exercise 1: Setup git/GitHub with R Studio

-   Create a new repo on GitHub and
-   Clone it as a new project in R Studio
-   Edit the default README in your new R Studio project
-   Commit the changes
-   Push the changes to GitHub

## Exercise 2: Create an R Markdown document with different output formats

-   In your new project create an R Markdown file
-   Edit the file and insert
    -   a simple plot with your own or Gapminder data
    -   citation to references exported from your reference manager
-   `knit` to the default output format (HTML)
-   Try different output formats: PDF, Word

## Exercise 3: Publish an R Markdown document via GitHub

-   Use your earlier R Markdown document
-   `knit` to HTML, push to GitHub and **publish** the document
-   Extra: Try to create a presentation as output

## References

::: {#refs}
:::

## Colophon {#colophon .colophon}

**SRC 2024 PhD course 'Data Science for Sustainable Development' ---
Reproducible Workflows using R Markdown and GitHub** by *Stefan Daume*  

Presented on 22. November 2024.

 

**PRESENTATION DETAILS**

**Author/Affiliation:** Stefan Daume, Stockholm Resilience Centre,
Stockholm University

**Presentation URL:**
<https://sdaume.github.io/ds4sd-2024-modules/workflows/slides/>

**Presentation Source:** <https://github.com/sdaume/ds4sd-2024-modules>

**Presentation PDF:**
<https://github.com/sdaume/ds4sd-2024-modules/workflows/slides/2024-ds4sd-workflows.pdf>

 

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
images) of this presentation are **Copyright © 2024 of the Author** and
provided under a *CC BY 4.0* public domain license.
