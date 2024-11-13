---
layout: post
title:  {explore} 1.3.3 is here!
---

Introducing `use_data_wordle()` and `yyyymm_calc()'

### use_data_wordle()

```
With the release of {explore} 1.3.3
you can put to the test
the power of data
of my daily WORDLE quest
```

WORDLE is a popular word-puzzle game. A friend and I started playing it daily and comparing our results. 
I collected the data and made it available in {explore}

```R
library(explore)
wordle <- use_data_wordle()
wordle |> describe()
```

```
# A tibble: 10 x 8
   variable type     na na_pct unique   min  mean   max
   <chr>    <chr> <int>  <dbl>  <int> <dbl> <dbl> <dbl>
 1 round    int       0      0     60     1 30.5     60
 2 word     chr       0      0     60    NA NA       NA
 3 language chr       0      0      1    NA NA       NA
 4 noun     int       0      0      2     0  0.9      1
 5 player   chr       0      0      2    NA NA       NA
 6 try      int       0      0      6     2  3.96     7
 7 aeiou    int       0      0      3     1  2.15     3
 8 unique   int       0      0      3     3  4.55     5
 9 common   int       0      0      4     2  3.85     5
10 rare     int       0      0      3     0  0.58     2
```

Explore it by yourself or check my blog-post about my WORDLE journey


### yyyymm_calc()

```
{explore} 1.3.3 has a function new
yyyymm_calc(), a vision true?
Year and month, a swift command,
a calculated answer, close at hand.
```

In some datasets dates is stored in the format `yyyymm`(e.g. 202411 for November 2024).
Adding 6 month to it causes a lot of work - converting into a real date, adding month, reconvert.
Now there is an easy way to that:

Let's say we have a database with a collection of Austrian beers. The year and month of production is stored.

```R
library(tidyverse)
library(explore)

# use beer data with random year/month produced 
beer <- use_data_beer() |>
  add_var_random_cat(
    name = "produced",
    cat = c(202210, 202211, 202212, 202301))

beer |> select(name, produced) |> head(12)
```

```
# A tibble: 12 x 2
   name                  produced
   <chr>                    <dbl>
 1 Puntigamer Maerzen      202212
 2 Puntigamer PR0,0ST      202210
 3 Puntigamer Panther      202211
 4 Puntigamer Winterbier   202301
 5 Puntigamer Zwickl       202212
 6 Goesser Maerzen         202212
 7 Goesser Helles          202301
 8 Goesser Naturgold       202210
 9 Goesser Spezial         202211
10 Goesser Gold            202212
11 Goesser Bock            202210
12 Goesser Stiftsbraeu     202211
```

```R
# calculate produced + 6 month & produced + 1 year
beer |> 
  select(name, produced) |> 
  mutate(
    best = yyyymm_calc(produced, add_month = 6),
    check = yyyymm_calc(produced, add_year = 1)
  ) 
```

```
# A tibble: 12 x 4
   name                  produced   best  check
   <chr>                    <dbl>  <dbl>  <dbl>
 1 Puntigamer Maerzen      202212 202306 202312
 2 Puntigamer PR0,0ST      202210 202304 202310
 3 Puntigamer Panther      202211 202305 202311
 4 Puntigamer Winterbier   202301 202307 202401
 5 Puntigamer Zwickl       202212 202306 202312
 6 Goesser Maerzen         202212 202306 202312
 7 Goesser Helles          202301 202307 202401
 8 Goesser Naturgold       202210 202304 202310
 9 Goesser Spezial         202211 202305 202311
10 Goesser Gold            202212 202306 202312
11 Goesser Bock            202210 202304 202310
12 Goesser Stiftsbraeu     202211 202305 202311
```
