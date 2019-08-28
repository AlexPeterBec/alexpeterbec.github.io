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
categories: [machine-learning, r]
---

Coming from Python, I recently joined a data science team using R. In this article I will try to cover the basics of data handling and machine learning libraries and tasks with code snippets.

The R documentation is not as friendly as Python for beginners, and putting all together may be painful at first.

# Workspace

## Rlang and RStudio

1. Install the [R language](https://cran.r-project.org/) on your computer.
2. Install a free and complete IDE : [RStudio](https://www.rstudio.com/products/rstudio/#Desktop).

Keep in mind that RStudio is not R : RStudio sends instructions to R. In RStudio you have access to the R console, it's a useful way to test commands and edit parameters.

## Libraries

The R basic install doesn't come with everything, just like with pip in Python, new libraries are installed with this command, in the R terminal :

```r
install.packages("thepackagename")
```

Once a package is installed :

```r
# Load readr in your code
library(readr)

# Manage libraries
installed.packages()
remove.packages("thepackagename")

# Getting help and documentation
?functionName
help(functionName)
example(functionName)
```

# Code

## Variables

```r
# Create new variables (both equivalent)
my_var <- 54
my_var = 54  

# Delete any object in memory
my_var <- NULL
```

## Using functions

```r
prod_age <- function(creation_date) {
  if (is.na(creation_date)) {return(as.numeric(-1))}
  else { return(as.numeric(format(age_calc(as.Date(creation_date), units='years'), digits = 5, nsmall=2)))}
}
```

# Working with dataframes

## Load data, read files

The [read_delim](https://www.rdocumentation.org/packages/readr/versions/1.3.1/topics/read_delim) function, from the readr library offers a lot of tools to read most of filetypes.

```r
library(readr)
non_conformites <- read_delim("C:/path/to/file.csv",
                                delim = "|",
                                escape_double = FALSE,
                                col_types = paste(rep("c", 56), collapse = ''))
```

## Working with columns

```r
# Filtering rows based on a specific column value
my_datarame <- subset(my_dataframe, COLNAME != 'str_value')

# Delete a column
my_dataframe$COLNAME <- NULL
```

## Export dataframe as CSV

```r
write.csv(non_conformites,'C:\\Users\\path\\export.csv', row.names = FALSE)
```

# Sources

- [Rdocumentation](https://www.rdocumentation.org)
- [Lots of research](https://www.ecosia.org/)
- [An introduction to R](https://cran.r-project.org/)
