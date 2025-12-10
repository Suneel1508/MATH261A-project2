# Engine Supplier and Constructor Experience as Predictors of Performance (Math 261A — Project 2)

**Author:** Suneel Chandra Vanamu
**Course:** MATH 261A

## Overview

This project investigates how much of the variation in Formula 1 constructor performance during the 2014–2020 Hybrid Turbo Era can be explained by engine supplier versus constructor experience. Using the public F1DB CSV release, I construct a season-level dataset and fit both ordinary least squares and LASSO models to quantify the relative contributions of these predictors. A train–test evaluation is used to assess how well the models generalize across constructors and seasons.

## Data

**Primary source:** F1DB (Formula 1 Database) — CSV release
GitHub: [https://github.com/f1db/f1db](https://github.com/f1db/f1db)
License: CC BY 4.0 (see F1DB repository for details)

Files used (placed in `f1db-csv/`):

* `f1db-races.csv`
* `f1db-races-constructor-standings.csv`
* `f1db-seasons-entrants-engines.csv`
* `f1db-engines.csv`
* `f1db-constructors.csv`
* `f1db-constructors-chronology.csv`

**Observational unit:** constructor–season.

**Variables used:**

* Constructor points (response)
* Engine supplier (categorical)
* Constructor experience (years since debut)

The response is modeled on the log scale as `log(points + 1)`.

## Research Questions

1. Does engine supplier explain systematic differences in constructor points during the Hybrid Turbo Era?
2. Does constructor experience add explanatory or predictive value once engine supplier is accounted for?
3. How do OLS and LASSO compare in identifying the strongest predictors?
4. Which model generalizes best to unseen constructor–seasons?

## Reproducibility & Setup

### Requirements

* R (4.3+ recommended)
* Quarto
* Packages: `tidyverse`, `janitor`, `ggplot2`, `broom`, `glmnet`, `caret`, `knitr`

### Install packages

```r
install.packages(c("tidyverse", "janitor", "ggplot2", "broom", "glmnet", "caret", "knitr"))
```

### Render the report

```bash
quarto render Math261A_Project2.qmd
```

or click **Render** in RStudio.

## Results (summary)

* Engine supplier is the dominant predictor of log-transformed points: Mercedes-powered teams score substantially more than Ferrari-, Renault-, Honda-, or Toro Rosso–powered teams.
* Constructor experience has only a small and borderline-significant effect in OLS and is removed entirely by the parsimonious LASSO model.
* The LASSO model using the one-standard-error penalty achieves the best predictive accuracy on the test set.
* Diagnostic checks show mild heteroskedasticity and heavy-tailed residuals but no issues that materially affect conclusions.

## External Resources

* F1DB documentation: [https://github.com/f1db/f1db](https://github.com/f1db/f1db)
* Stack Overflow (general R troubleshooting)
* ChatGPT Edu for brainstorming and code-formatting support

## Acknowledgments

* MATH 261A template: [https://github.com/peteragao/MATH261A-project-template](https://github.com/peteragao/MATH261A-project-template)
* Thanks to the F1DB community for maintaining a high-quality public dataset

## Citation

A `references.bib` file is included. Cite using keys such as `@f1db-github`, `@R-base-2024`, `@ggplot2-book-2016`, etc.

## Notes & Limitations

* Season-level points obscure within-season dynamics (drivers, reliability, development).
* Experience is an imperfect proxy for organizational strength.
* Engine supplier captures much of the predictable structure, but unobserved variables (budget, aero, strategy) remain important.
* Linear models provide associations, not causal effects.

