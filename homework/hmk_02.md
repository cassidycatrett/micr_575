# hmk_2

## Homework 2

### Questions

What were the main issues in the Reinhard and Rogoff issue, and how best
could they have been avoided?

What key attributes make a piece of data analysis “reproducible”? Please
put those attributes in a prioritized list (i.e., for you, what is most
important, next most important, etc…)

Imagine that you are doing a piece of data analysis that only you will
ever see: perhaps you are shopping for a car and trying to determine
what will give you the best value for your money. Should you think about
making your data analysis reproducible? Why or why not?

### Responses

The main issue for Reinhard and Rogoff was the result of an error with
Excel. This computing/coding issue created a bigger issue in that wrong
results for a national economic study were shared and utilized around
the globe. They found that, on average, real econoic growth for a
country slows, a value of 0.1%, when a country’s debt grows to be
greater than 90% gross domestic product. However, when another group
tried to replicate this study with the same data set, the Excel error
was uncovered and the 0.1% value jumped up to 2.2%, completely changing
the result for the economic study. The Excel error was found years after
the initial study was published, meaning that incorrect results had been
shared and utilized for years. This entire situation could have been
avoided. Given that this study was a computational study, the data and
coding information could have been shared and reanalyzed prior to
publication to ensure the accuracy of the results. Accurate record
keeping and recording of coding/computational steps would have allowed
for this study to be done by others with computational knowledge and
aided in the ability to reanalyze this study.

In trying to make data analyses reproducible, several steps are
involved. For me, the first step is to create some notebook (R script, R
markdown, Quarto document, etc.) where code is written and annotated.
Annotating code, to me, might be the most important step in this
process. When we annotate our code, we are able to explain what this
line of code is doing and why we need this for our procedure. Within
this notebook/document, along with annotating our code, we also need to
make note of changes we make to the code. Personally, when I change a
piece of code within my notebook, I like to just make a new code block
and note it as being the final or updated piece and mark that line with
how it is different from my initial piece of code. Once a thorough and
easy to understand notebook has been developed, this document/notebook
needs to be made accessible to others. I have used GitHub for this for a
few years now and find this to be a very useful way to not only have a
record for myself, but to share my work with others doing similar
research.

I think that anytime we are working on some form of data analysis, we
should aim to make it reproducible. We may not be needing to share our
code/analyses with others, but we do need to remember what we did. I
recently defended my thesis and as I began to write my materials and
methods, I was thankful that I had been thorough two years ago with my R
markdown by noting code changes and reasoning for each line of code. If
I had not had the forethought to do that, I would, probably, still be
spinning my wheels trying to recall all the steps I took for data
cleaning and phenotype calculations. Beyond that, we never know when we
might lose our work. If we make our data reproducible and have our notes
stored and annotated, we can easily re-run analyses to get back the
results we might have lost.
