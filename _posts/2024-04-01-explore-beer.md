---
layout: post
title:  Let's {explore} beer!
---

Let's dive into beer-data and build a beer-AI!

### Setup

If {explore} is not installed, install it from CRAN (you need explore 1.2.0 or higher)

```R
install.packages("explore") 
```

Then we simply load the package and use the beer data!

```R
library(explore)
data <- use_data_beer()
```

### Data understanding

Firest, we describe the table:

```R
data |> describe_tbl()
```

```
161 observations with 11 variables
19 observations containing missings (NA)
5 variables containing missings (NA)
1 variables with no variance
```

Then we describe all variables:

```R
data |> describe_all()
```

```
# A tibble: 11 x 8
   variable          type     na na_pct unique    min    mean    max
   <chr>             <chr> <int>  <dbl>  <int>  <dbl>   <dbl>  <dbl>
 1 name              chr       0    0      161   NA     NA      NA  
 2 brand             chr       0    0       29   NA     NA      NA  
 3 country           chr       0    0        3   NA     NA      NA  
 4 year              dbl       0    0        1 2023   2023    2023  
 5 type              chr       0    0        3   NA     NA      NA  
 6 color_dark        dbl       0    0        2    0      0.09    1  
 7 alcohol_vol_pct   dbl       2    1.2     35    0      4.32    8.4
 8 original_wort     dbl       5    3.1     54    5.1   11.3    18.3
 9 energy_kcal_100ml dbl      11    6.8     34   20     39.9    62  
10 carb_g_100ml      dbl      16    9.9     44    1.5    3.53    6.7
11 sugar_g_100ml     dbl      16    9.9     26    0      0.72    4.6
```

So we got 161 beers (29 different brands) from 3 countries. For most of the beers we got most common attributes like alcohol (in volumne percent), original wort, energy (in kcal per 100 ml), and so on. 
Let's take a closer look to some of the attributes (we will use "beer-like" golden color for the plots):

```R
library(dplyr)
data |> 
  select(country, year, type, color_dark) |> 
  explore_all(color = "gold")
```

![data-understanding-1](../images/explore-beer-understand1.png)

```R
data |> 
  select(alcohol_vol_pct, original_wort, energy_kcal_100ml, carb_g_100ml, sugar_g_100ml) |> 
  explore_all(color = "gold")
```

![data-understanding-2](../images/explore-beer-understand2.png)

Somme of the beers have unknown attributes (na values). The density-plot of alcolhol_vol_pct and original_wort look quite similar, there seems to be a strong relationship.

