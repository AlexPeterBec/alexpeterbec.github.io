---
published: true
title: "R for machine learning"
excerpt: "Toolbox for starting a data science project"
toc: true
toc_sticky: true
toc_label: "R "
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
my_var <- 54 # Create new variables
my_var = c(1, 4, 8, 2, 4) # The = also works

# Delete any object in memory
my_var <- NULL
```

## Create a function

```r
prod_age <- function(creation_date) {
  if (is.na(creation_date)) {return(as.numeric(-1))}
  else { return(age_calc(as.Date(creation_date), units='years'))}
}
```

# Working with dataframes

## Load data, read files

The [read_delim](https://www.rdocumentation.org/packages/readr/versions/1.3.1/topics/read_delim) function, from the readr library offers a lot of tools to read most of filetypes.

In the example below, we specify the data type of each column. The file has 56 columns, and we want all of them to be read as characters, so we use the col_types argument with "c...c", each character corresponding to a column.

```r
library(readr)
non_conformites <- read_delim("C:/path/to/file.csv",
                                delim = "|",
                                escape_double = FALSE,
                                col_types = paste(rep("c", 56), collapse = ''))
```

## Working with columns

When a dataframe object is created, we access specific columns with the $ operator.

```r
# Filtering rows based on a specific column value
my_datarame <- subset(my_dataframe, COLNAME != 'str_value')

# Assign 0 where column values match condition
non_conformites$REGUL_DAYS[non_conformites$REGUL_DAYS_NUM < 0] <- 0

# Create new column from existing columns
table$AMOUNT <- table$Q_LITIG * table$PRICE

# Delete a column
my_dataframe$COLNAME <- NULL
```

Once we have a dataframe and functions ready, we often need to apply functions on columns :

```r
# Product age function
prod_age <- function(creation_date) {
  if (xxx) {return(as.numeric(-1))}
  else { return(as.Date(creation_date))}
}

# Apply function on column
mytable$PRODUCT_AGE <-
  apply(mytable[,c('DATE_CREA'), drop=F], 1, function(x) prod_age(x))
```

## Working with dates

```r
# Convert a column into date format
ventes$date_f <- as.Date(ventes$date, format = '%d/%m/%Y')

# Create column from time difference
mytable$REGUL_DAYS = as.numeric(difftime(strptime(mytable$closing, "%Y-%m-%d"), strptime(mytable$opening, "%Y-%m-%d"), unit="days"))
```

## Export dataframe as CSV

```r
write.csv(non_conformites,'C:\\Users\\path\\export.csv', row.names = FALSE)
```

# Plotting

Just like Python, R comes with several libraries for plotting data. The **plot** function is actually similar to plt.plot with pyhton.

## Line chart

```r
plot(
  ref_sales$Date,
  ref_sales$Sales,
  type = 'l',
  xlab = "Date",
  ylab = "Sales",
  main = paste('Sales evolution over time for article : ', article_ref)
)
```

## Various charts

R being a statistician language, it comes with various charts for plotting distribution,

```r
values <- c(1, 4, 8, 2, 4)
barplot(values)
hist(values)
pie(values)
boxplot(values)
```


# Sources

- [Rdocumentation](https://www.rdocumentation.org)
- [Lots of research](https://www.ecosia.org/)
- [An introduction to R](https://cran.r-project.org/)
