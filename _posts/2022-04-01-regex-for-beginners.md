---
layout: post
title: Regular Expressions for beginners
---

Introduction to Regular Expressions (regex) in R

## Intro

As a Data Scientist you will work with regular expressions (regex). 

There are several ways how to use regex to search for patterns in a text-vector:

```grep``` is a base-R function and returns a vector containing the (integer) indices of the matches. So in this case it returns 2.

```R
> grep("Orange", c("Apple", "Orange", "Lemon"))
[1] 2
```

```grepl``` returns a locial vector

```R
> grepl("Orange", c("Apple", "Orange", "Lemon"))
[1] FALSE  TRUE FALSE
```

To return the value instead of the index use parameter ```value = TRUE```

```R
> grep("a", c("Apple", "Orange", "Lemon"), value = TRUE)
[1] Orange
```

If you want to use {tidyverse} you can use {stringr}:

```R
> stringr::str_detect(c("Apple", "Orange", "Lemon"), "Orange")
[1] FALSE  TRUE FALSE
```

## Basic Examples

* ```grep("Lemon", c("Apple", "Orange", "Lemon"))``` <br>returns ```3```
* ```grep("e", c("Apple", "Orange", "Lemon"))``` <br>returns ```1 2 3```
* ```grep("a", c("Apple", "Orange", "Lemon"))``` <br>returns ```2``` because it is case sensitive by default

## Case Sensitive

```grep``` is case sensitive by default.
To switch off case sensitivity you can use the parameter ```ignore.case = TRUE```

* ```grep("a", c("Apple", "Orange", "Lemon"), ignore.case = TRUE)``` <br>now returns ```1 2```
* ```grep("ORANGE", c("Apple", "Orange", "Lemon"), ignore.case = TRUE)``` <br>returns ```2```
* ```grep("orange", c("Apple", "Orange", "Lemon"), ignore.case = TRUE)``` <br>returns ```2```

## Starts With

To search for a pattern at the beginning of a string you can use ```^```:

* ```grep("^A", c("Apple", "Orange", "Lemon"))``` <br>returns ```1```
* ```grep("^p", c("Apple", "Orange", "Lemon"))``` <br>has no matach

## Ends With

To search for a pattern at the end of a string you can use ```$```:

* ```grep("e$", c("Apple", "Orange", "Lemon"))``` <br>returns ```1 2```
* ```grep("n$", c("Apple", "Orange", "Lemon"))``` <br>returns ```3```

## Starts & Ends With

To combine both:

```R
> grep("^A.*e$", c("Apple", "Orange", "Lemon"))
[1] 1
```

* ```^A``` = beginning with "A"
* ```.*``` = any string
* ```e$``` = ends with "e"

To control the number of characters between start and end:

```R
> str = c("Apple", "Ape", "Ae")
```

* ```grep("^A.*e$", str)``` <br>returns ```1 2 3``` <br>(Starts with "A" and ends with "e")
* ```grep("^A.+e$", str)``` <br>returns ```1 2``` <br>(Starts with "A" and ends with "e", between at least ONE character)
* ```grep("^A.{3}e$", str)``` <br>returns ```1``` <br>(Starts with "A" and ends with "e", between at EXACTLY 3 character)
* ```grep("^A.{2,}e$", str)``` <br>returns ```1``` <br>(Starts with "A" and ends with "e", between at 2 or more character)
* ```grep("^A.{1,3}e$", str)``` <br>returns ```1 2``` <br>(Starts with "A" and ends with "e", between at min 1 max 3 character)


## Escaping

```R
> grep("*.txt", c("f1.txt", "f2.txt", "f3-txt"))
[1] 1 2 3
```

This result may surprise you if you are not used regex. Here "." is not the character ".", but means "any character". To search for the character ".", we need to "excape" it:

```R
> grep("*\\.txt", c("f1.txt", "f2.txt", "f3-txt"))
[1] 1 2
```

In they same way you need to escape:

* ```+``` =  ```\\+```
* ```*``` =  ```\\*```
