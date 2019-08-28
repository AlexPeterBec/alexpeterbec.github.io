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

I recently joined a data science team using R, and coming from Python, I had to struggle for a few days around R documentation. In this article I will try to cover the basics of data handling and machine learning libraries and tasks with code snippets.

The R documentation is not as friendly as Python for beginners, and putting all together may be painful at first.

Anecdotes :
- The "." can be used inside variable names.
- The "$" is used to access columns of a table.
- To assign a variable, we can use either = or <-

# Workspace

## Getting started

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

# Load a list of Libraries
p.names <- c('xgboost', 'caret', 'dplyr', 'e1071')
lapply(p.names, library, character.only = TRUE)

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
my_var <- NULL # Delete any object in memory
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
mytable$REGUL_DAYS = as.numeric(difftime(
  strptime(mytable$closing, "%Y-%m-%d"),
  strptime(mytable$opening, "%Y-%m-%d"),
  unit="days"))
```

## Export dataframe

Several built-in functions allow to write dataframes as files. A very common format is CSV. However, the RDS format is optimized (serialized + Gzip compression) to store any R objects.

```r
# Write to CSV
write.csv(non_conformites,
  'C:\\Users\\path\\export.csv',
  row.names = FALSE)

# Write to RDS
saveRDS(
  feature_importance_values,
  file="c:/path/folder/feature_importance.RDS")
```

# Plotting

Just like Python, R comes with several libraries for plotting data. The **plot** function is actually similar to plt.plot with pyhton.

## Line charts

```r
plot(
  ref_sales$Date, ref_sales$Sales,
  type = 'l',
  xlab = "Date", ylab = "Sales",
  main = paste('Sales evolution over time for : ', article_ref)
)
```

## Various charts

R being the language of statisticians, it comes with various charts for plotting data distributions.

```r
values <- c(1, 4, 8, 2, 4)
barplot(values)
hist(values)
pie(values)
boxplot(values)
```

# Machine learning

For this part, we need those specific libraries :
- **xgboost** : Let's work around XGB famous algorithm.
- **caret** : Classification And REgression Training, includes lots of data processing functions
- **dplyr** : A fast, consistent tool for working with data frame like objects, both in memory and out of memory.

## Train-Test split

Once the dataframe is prepared, we split it into train and test sets, using an index (inTrain) :

```r
set.seed(1337)
inTrain <- createDataPartition(y = my.dataframe$label, p = 0.85, list = FALSE)

X_train = xgb.DMatrix(as.matrix(my.dataframe[inTrain, ] %>% select(-label)))
y_train = my.dataframe[inTrain, ]$label
X_test = xgb.DMatrix(as.matrix(my.dataframe[-inTrain, ] %>% select(-label)))
y_test = my.dataframe[-inTrain, ]$label
```

## Parameter search for XGBoost

What the following function does :
- Take our train/test sets as input.
- Define a trainControl for cross validation .
- Define a grid for parameters.
- Setup a XGB model including the parameter search.
- Evaluate the model's accuracy
- Return the set of best parameters


```r
param_search <- function(xtrain, ytrain, xtest, ytest) {

  # Cross validation init
  xgb_trcontrol = trainControl(method = "cv", number = 5, allowParallel = TRUE,
                               verboseIter = T, returnData = FALSE)

  # Param grid
  xgbGrid <- expand.grid(nrounds = 60, #nrounds = c(10,20,30,40),
                         max_depth = 20, #max_depth = c(3, 5, 10, 15, 20, 30),
                         colsample_bytree = 0.6,#colsample_bytree = seq(0.5, 0.9, length.out = 5),
                         eta = 0.005, #eta = c(0.001, 0.0015, 0.005, 0.1),
                         gamma=0, min_child_weight = 1, subsample = 1
  )

  # Model and parameter search
  xgb_model = train(xtrain, ytrain, trControl = xgb_trcontrol,
                    tuneGrid = xgbGrid, method = "xgbTree",
                    verbose=2,
                    #objective="multi:softprob",
                    eval_metric="mlogloss")
                    #num_class=3)

  # Evaluate du model
  xgb.pred = predict(xgb_model, xtest, reshape=T)
  xgb.pred = as.data.frame(xgb.pred, col.names=c("pred"))
  result = sum(xgb.pred$xgb.pred==ytest) / nrow(xgb.pred)
  print(paste("Final Accuracy =",sprintf("%1.2f%%", 100*result)))

  return(xgb_model)
}
```

Once the parameter search is done, we can use it directly to define our working model, we access each element with the $ operator :

```r
best.model  <- xgboost(
  data = as.matrix(my.dataframe[inTrain, ] %>% select(-IMPORTANCE)),
  label = as.matrix(as.numeric(my.dataframe[inTrain, ]$IMPORTANCE)-1),
  nrounds = xgb_model$bestTune$nrounds,
  max_depth = xgb_model$bestTune$max_depth,
  eta = xgb_model$bestTune$eta,
  gamma = xgb_model$bestTune$gamma,
  colsample_bytree = xgb_model$bestTune$colsample_bytree,
  min_child_weight = xgb_model$bestTune$min_child_weight,
  subsample = xgb_model$bestTune$subsample,
  objective = "multi:softprob",
  num_class=3)
```

## Compute and plot feature importance

Here again, a lot of functions are ready to use in the xgboost package. The [documentation](https://xgboost.readthedocs.io/en/latest/R-package/xgboostPresentation.html) presents most of them.

```r
xgb_feature_imp <- xgb.importance(
  colnames(donnees[inTrain, ] %>% select(-label)), model = best.model)

gg <- xgb.ggplot.importance(xgb_feature_imp, 40); gg
```

# Sources

- [Rdocumentation](https://www.rdocumentation.org)
- [Lots of research](https://www.ecosia.org/)
- [An introduction to R](https://cran.r-project.org/)
- [Getting started with XGBoost (R API)](https://xgboost.readthedocs.io/en/latest/R-package/xgboostPresentation.html)
