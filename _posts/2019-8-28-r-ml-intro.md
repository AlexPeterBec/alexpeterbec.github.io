---
published: true
title: "R for machine learning"
excerpt: "Toolbox for starting a data science project"
toc: true
toc_sticky: true
toc_label: ""
toc_icon: "microchip"
comments: true
author_profile: false
header:
  overlay_image: "assets/images/covers/cover6.png"
  teaser: "assets/images/covers/cover6.png"
categories: [machine-learning]
---

Coming from Python, I recently joined a data science team using R. In this article I will try to cover the basics of data handling and machine learning libraries and tasks with code snippets.

The R documentation is not as friendly as Python for beginners, and putting all together may be painful at first.

## The workspace

1. Install the [R language](https://cran.r-project.org/) on your computer.
2. Install a free and complete IDE : [RStudio](https://www.rstudio.com/products/rstudio/#Desktop).

Keep in mind that RStudio is not R : RStudio sends instructions to R. In RStudio you have access to the R console, it's a useful way to test commands and edit parameters.

## Libraries

The R basic install doesn't come with everything, just like with pip in Python, new libraries are installed with this command, in the R terminal :

```r
install.packages("thepackagename")
```

Then, in your code, use this to load the library :

```r
library(readr)
```

## Working with functions

```r
prod_age <- function(creation_date) {
  if (is.na(creation_date)) {return(as.numeric(-1))}
  else { return(as.numeric(format(age_calc(as.Date(creation_date), units='years'), digits = 5, nsmall=2)))}
}
```

## Sources

- [Lots of research](https://www.ecosia.org/)
- [An introduction to R](https://cran.r-project.org/)
