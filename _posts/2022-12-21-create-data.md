---
layout: post
title:  Create your own (synthetic) data!
---

You need sample data for learning/testing/teaching? 
Create your own ... using {explore}

## Prepared data

The R package {explore} offers prepared synthetic data. You can use ```create_data_*()``` functions to create this synthetic data.
The number of observations can be controlled by parameter obs. If you want to create reproducible synthetic data, use parameter seed (random seed number)

```R
library(explore)
library(dplyr)

data <- create_data_person(obs = 1000, seed = 10)
describe(data)
```
```
# A tibble: 15 x 8
   variable          type     na na_pct unique   min  mean   max
   <chr>             <chr> <int>  <dbl>  <int> <dbl> <dbl> <dbl>
 1 age               int       0      0     80  16   55.4   95  
 2 gender            chr       0      0      3  NA   NA     NA  
 3 eye_color         chr       0      0      3  NA   NA     NA  
 4 shoe_size         dbl       0      0     39  30.2 41.8   52.2
 5 iq                dbl       0      0    110  37   99.3  173  
 6 education         int       0      0    101   0   50.0  100  
 7 income            dbl       0      0    220   0   62.5  143  
 8 handset           chr       0      0      3  NA   NA     NA  
 9 pet               chr       0      0      4  NA   NA     NA  
10 favorite_pizza    chr       0      0      6  NA   NA     NA  
11 favorite_icecream chr       0      0      7  NA   NA     NA  
12 likes_garlic      int       0      0      2   0    0.6    1  
13 likes_sushi       int       0      0      2   0    0.32   1  
14 likes_beatles     int       0      0      2   0    0.5    1  
15 likes_beer        int       0      0      2   0    0.64   1  
```

We get a dataframe containing 1000 observations and 15 variables. Some of these variables have completely random values, some have build in correlations.

```R
data |> 
  select(age, gender, likes_beer) |> 
  explore_all(target = likes_beer)
```

![explore](../images/create-data-explore-likes-beer.png)

The pattern age/likes_beer is just a random noise, but gender/likes_beer is a build in correlation.
