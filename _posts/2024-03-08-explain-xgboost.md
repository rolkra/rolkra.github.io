---
layout: post
title:  Explain XGBoost
---

Let's create a XGBoost model (the easy way)

### Setup

If {explore} is not installed, install it from CRAN (you need explore 1.2.0 or higher)

```R
install.packages("explore") 
```

Then we simply load the package and create some data

```R
library(explore)
data <- create_data_buy(obs = 1000)
```
### Data preparation

Let's take a look into the data

```R
data |> describe()
```
```
# A tibble: 13 x 8
   variable        type     na na_pct unique    min      mean    max
   <chr>           <chr> <int>  <dbl>  <int>  <dbl>     <dbl>  <dbl>
 1 period          int       0      0      1 202012 202012    202012
 2 buy             int       0      0      2      0      0.51      1
 3 age             int       0      0     66     17     52.3      88
 4 city_ind        int       0      0      2      0      0.5       1
 5 female_ind      int       0      0      2      0      0.5       1
 6 fixedvoice_ind  int       0      0      2      0      0.11      1
 7 fixeddata_ind   int       0      0      1      1      1         1
 8 fixedtv_ind     int       0      0      2      0      0.4       1
 9 mobilevoice_ind int       0      0      2      0      0.63      1
10 mobiledata_prd  chr       0      0      3     NA     NA        NA
11 bbi_speed_ind   int       0      0      2      0      0.61      1
12 bbi_usg_gb      int       0      0     83      9    164.   100000
13 hh_single       int       0      0      2      0      0.37      1
```
So we got a dataset with 13 variables. `buy` is a binary variable, 
containing only 2 unique values: 0 and 1. We will use `buy` as target.

For the XGBoost we just need numeric variables. Here we have a character variable. 
We could try to convert it into a meaningful numeric variable, but in this example we will simply
drop all variables that are not numeric or have no variance.

```R
data <- data |> 
  drop_var_no_variance() |> 
  drop_var_not_numeric()

data |> describe()
```
```
# A tibble: 10 x 8
   variable        type     na na_pct unique   min   mean    max
   <chr>           <chr> <int>  <dbl>  <int> <dbl>  <dbl>  <dbl>
 1 buy             int       0      0      2     0   0.51      1
 2 age             int       0      0     66    17  52.3      88
 3 city_ind        int       0      0      2     0   0.5       1
 4 female_ind      int       0      0      2     0   0.5       1
 5 fixedvoice_ind  int       0      0      2     0   0.11      1
 6 fixedtv_ind     int       0      0      2     0   0.4       1
 7 mobilevoice_ind int       0      0      2     0   0.63      1
 8 bbi_speed_ind   int       0      0      2     0   0.61      1
 9 bbi_usg_gb      int       0      0     83     9 164.   100000
10 hh_single       int       0      0      2     0   0.37      1
```
Now we have only 13 variables. `period` and `fixeddata_ind` are dropped because they contain only a constant value (no variance).
`mobiledata_prd` is dropped because it is not numeric.

### Create XGBoost

We are ready to create a XGBoost model. It is as simple as this:

```R
data |> explain_xgboost(target = buy)
```

We get the feature importance of a XGBoost model explaining the target `buy`: 

![explore_all](../images/xgboost-plot-feature-importance.png)

So the most important varaibles are 'age', `bbi_usg_gb`, `femaale_ind` and `fixed_tv_ind`

Let's take a closer look to their relationship with the target variable `buy`:

```R
library(dplyr)  # for select
data |> 
  select(buy, age, bbi_usg_gb, female_ind, fixedtv_ind) |> 
  explore_all(target = buy)
```

![explore_all](../images/xgboost-explore_all.png)

