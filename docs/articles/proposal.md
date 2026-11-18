# BST260 Final Project Proposal: Homicide and Firearm Mortality in the United States

To: BST260 Teaching Team, Fall 2026

## Project overview

For my final project, I plan to examine how homicide and firearm
mortality rates vary across U.S. states and over time. I am interested
in whether states differ only in their mortality rates or also in how
those rates change from year to year. The two measures are related but
not identical, so studying them side by side may help put their
geographic and temporal patterns into context. The project will focus on
describing these patterns and their limitations rather than drawing
causal conclusions.

## Data and research questions

I will use two datasets provided with the BST260 project template:
`cdcmurd`, which contains homicide mortality data, and `cdcfiremort`,
which contains firearm mortality data. Both are described in the package
documentation as state-level data from the CDC’s National Center for
Health Statistics (NCHS). The relevant CDC *Stats of the States* pages
are [Homicide
Mortality](https://www.cdc.gov/nchs/state-stats/deaths/homicide.html)
and [Firearm
Mortality](https://www.cdc.gov/nchs/state-stats/deaths/firearms.html).
These pages identify CDC WONDER and National Vital Statistics System
mortality data as their underlying sources. I will use the versions
bundled in `finalproject` and document their actual year ranges,
variable definitions, and coverage, rather than assume that the packaged
data contain all years shown on the current CDC pages.

I plan to address two questions:

1.  How is calendar year associated with the age-adjusted homicide
    mortality rate across U.S. states, and how do these trends differ by
    state?
2.  How is calendar year associated with the age-adjusted firearm
    mortality rate across U.S. states, and how do these trends differ by
    state?

The population of interest is residents of the U.S. states and District
of Columbia represented in the data. The planned unit of analysis is a
state-year, subject to confirming that each dataset has one record per
state and year. In each analysis, the main exposure is calendar year,
which I will treat as a numeric variable to summarize changes over time
and as a categorical variable for comparisons between individual years.
The outcome is a continuous age-adjusted mortality rate expressed as
deaths per 100,000 population. State will be treated as a categorical
grouping variable. In `cdcmurd`, the course materials identify `YEAR`,
`Location`, and `Death.Rate` as the relevant columns; I will inspect
`cdcfiremort` before deciding whether any variable names need to be
harmonized.

## Planned analysis

I will begin by inspecting the structure of each dataset and checking
which states and years are represented, whether there are duplicate
state-year records, and where important values are missing. I will
report the number of available observations and the number of missing
mortality rates by state and year. Records without a usable year or
state identifier cannot be included in state-year comparisons. For
summaries of mortality rates, I will exclude observations with missing
rates and report those exclusions rather than treating missing values as
zero. Because the CDC cautions that rates based on small numbers of
deaths can be unstable or unavailable, I will check the documentation
and any available death counts before interpreting missing or extreme
rates.

For each dataset, I plan to summarize the distribution of state
mortality rates by year using medians, quartiles, and ranges. Boxplots
or dot plots will show how states compare in the same year, while line
plots will show trends for individual states over time. I will also look
at whether differences between states have narrowed or widened over the
available years. These summaries will describe the distribution across
states; for example, an unweighted average of state rates should not be
interpreted as the U.S. national mortality rate.

If there are enough repeated observations across states and years, I
also plan to fit an exploratory linear regression of the mortality rate
on calendar year, with state indicators to account for relatively stable
differences between states. I will check whether a straight-line trend
is a reasonable summary and rely on year-specific plots when the pattern
is not approximately linear. If I report model-based uncertainty, I will
account for repeated observations from the same state. I chose state as
an adjustment factor because differences in baseline conditions across
states could otherwise obscure temporal comparisons. Other potentially
important factors include socioeconomic conditions, firearm legislation,
and changes in population composition. The packaged datasets do not
necessarily measure these factors, so I will not claim that the model
adjusts for them. Age adjustment helps with differences in age
structure, but neither age adjustment nor state indicators remove all
sources of confounding.

After analyzing the two outcomes separately, I will compare their
patterns only for states and years available in both datasets. Homicide
mortality includes deaths involving methods other than firearms, while
firearm mortality includes suicides and other firearm-related deaths in
addition to firearm homicides. Since the categories overlap, I will not
add the rates or interpret their difference as a count of any particular
type of death. Instead, I will describe where their overall patterns
appear similar or different and consider possible explanations without
treating those comparisons as causal evidence.

## Planned final deliverables

I will prepare two Quarto vignettes in the `finalproject` R package: one
analyzing `cdcmurd` and the other analyzing `cdcfiremort`. Each vignette
will include the data source and provenance, any cleaning decisions,
descriptive statistics and visualizations, an interpretation of the
findings, and a discussion of uncertainty and limitations. I also plan
to write small reusable R functions for checks and summaries that apply
to both datasets. The code and vignettes will be available in the public
GitHub repository, and the completed reports will be published through
the package’s pkgdown website.
