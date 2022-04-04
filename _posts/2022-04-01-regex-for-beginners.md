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

 ```R
> grep("Lemon", c("Apple", "Orange", "Lemon"))
[1] 3
``` 

 ```R
> grep("e", c("Apple", "Orange", "Lemon"))
[1] 1 2 3
``` 
Matches all tree, because all contain the character "e"

```R
> grep("a", c("Apple", "Orange", "Lemon"))
[1] 2
```
Matches "Orange" (but not "Apple"), because it is case sensitive by default

## Case Sensitive

```grep``` is case sensitive by default.
To switch off case sensitivity you can use the parameter ```ignore.case = TRUE```

```R
> grep("a", c("Apple", "Orange", "Lemon"), ignore.case = TRUE)
[1] 1 2
```
Now matches "Apple" and "Orange" as both contain "a" (ignoring upper/lower-case)

```R
> library(stringr)
> str_detect(c("Apple", "Orange", "Lemon"), regex("a", ignore_case = TRUE))
[1]  TRUE  TRUE FALSE
```
The same using {tidyverse} and {stringr}


## Starts With

To search for a pattern at the beginning of a string you can use ```^```:

```R
> grep("^a", c("Apple", "Orange", "Lemon"), ignore.case = TRUE)
[1] 1
```
Now only "Apple" matches, because the "a" in "Orange" is in the middle.

## Ends With

```R
> grep("e$", c("Apple", "Orange", "Lemon"), ignore.case = TRUE)
[1] 1 2
```
Matches "Apple" and "Orange", but not "Lemon", because the "e" in Lemon is not at the end!

## Starts & Ends With

To combine both:

```R
> grep("^A.*e$", c("Apple", "Orange", "Lemon"))
[1] 1
```

* ```^A``` = beginning with "A"
* ```.*``` = any string
* ```e$``` = ends with "e"

To control the number of characters between start and end you can use ```*```, ```+``` and ```{ }```:

* ```.*``` = any string 
* ```.+``` = any string with minimum length of 1 character
* ```.{3}``` = exactly 3 character
* ```.{3,}``` = 3 or more character
* ```.{1,3}``` = between 1 and 3 character


```R
> str = c("Apple", "Ape", "Ae")
> grep("^A.{2,}e$", str)
[1] 1
```
Only "Apple" starts with "A", ends with "e" and has of 2+ character inbetween!

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

Charcters you need to escape:

* ```.``` =  ```\\.```
* ```+``` =  ```\\+```
* ```*``` =  ```\\*```
* ```"``` =  ```\\"```
