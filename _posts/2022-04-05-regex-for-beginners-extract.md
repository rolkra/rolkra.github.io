---
layout: post
title: Regex for beginners: extract!
---

Introduction to Regular Expressions (regex) in R: how to extract patterns

## Intro

As a Data Scientist you should know how to use regular expressions (regex). 

You can use regex to detect, locate and extract patterns.

```str_extract``` can be used to extract patterns:


```R
> library(stringr)
> string <- c("apple", "orange", "apple+orange")
> str_extract(string, "a.*e")
[1] "apple"  "ange"  "apple+orange"
```

So we are searching for strings that starts with "a" and end with "e". 

* "apple" in "apple"
* "ange" in "orange"
* "apple+orange" in "apple+orange"

But wait, why not "apple" in "apple+orange" (as it starts with "a" and ends with "e" too)?

## Greedy Matching

By default the asterisk * is greedy, i.e. it always matches the longest possible string. Thats why str_extract() returns "apple+orange" and not just "apple".

If you want get the shortest match:

```R
> library(stringr)
> string <- c("apple", "orange", "apple+orange")
> str_extract(string, "a.*?e")
[1] "apple"  "ange"  "apple"
```

By adding a "?" after "*" in a regex the asterisk * is not greedy any more

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