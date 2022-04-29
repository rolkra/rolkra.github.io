---
layout: post
title: Regex for beginners - extract!
---

Introduction to Regular Expressions (regex) in R: how to extract patterns

## Intro

As a Data Scientist you should know how to use regular expressions (regex). 

You can use regex to detect, locate and extract patterns.

Check this [post] (https://rolkra.github.io/regex-for-beginners-detect/) on how to detect patterns.

```str_extract()``` can be used to extract patterns:


```R
> library(stringr)
> string <- c("apple", "orange", "apple+orange")
> str_extract(string, "a.*e")
[1] "apple"  "ange"  "apple+orange"
```

So we are searching for strings that starts with "a" and end with "e". We find:

* "apple" in "apple"
* "ange" in "orange"
* "apple+orange" in "apple+orange"

But wait, why not "apple" in "apple+orange" (as it starts with "a" and ends with "e" too)?

## Greedy Matching

By default the asterisk ```*``` is "greedy", i.e. it always matches the longest possible string. Thats why str_extract() returns "apple+orange" and not just "apple".

If you want get the shortest match:

```R
> library(stringr)
> string <- c("apple", "orange", "apple+orange")
> str_extract(string, "a.*?e")
[1] "apple"  "ange"  "apple"
```

By adding a ```?``` after ```*``` in a regex the asterisk ```*`` is not greedy any more

## All Matches

To get ALL matches you can use ```str_extract_all()``` from {stringr}:

```R
> library(stringr)
> string <- c("apple", "orange", "apple+orange")
> str_extract(string, "a.*?e")
[[1]]
[1] "apple"

[[2]]
[1] "ange"

[[3]]
[1] "apple" "ange" 
```

Now we find "apple" and "ange" in "apple+orange". After getting the first pattern match ("apple" in "apple+orange"), regex will search for the next pattern match in the REMAINING string ("+orange").

To get a matrix as result (instead of a list):

```R
> library(stringr)
> string <- c("apple", "orange", "apple+orange")
> str_extract(string, "a.*?e", simplify = TRUE)
     [,1]    [,2]  
[1,] "apple" ""    
[2,] "ange"  ""    
[3,] "apple" "ange"
```

## Replace

Use ```str_replace``` to replace a pattern in a string:

```R
> library(stringr)
> string <- c("apple", "orange", "apple+orange")
> str_replace(string, "a.*?e", "AE")
[1] "AE"        "orAE"      "AE+orange"
```

To replance ALL patterns:

```R
> library(stringr)
> string <- c("apple", "orange", "apple+orange")
> str_replace_all(string, "a.*?e", "AE")
[1] "AE"        "orAE"      "AE+orAE"
```

## Cheat Sheets

* [String manipulation with {stringr}] (https://raw.githubusercontent.com/rstudio/cheatsheets/main/strings.pdf)
* [Regex in R] (https://raw.githubusercontent.com/rstudio/cheatsheets/main/regex.pdf)
