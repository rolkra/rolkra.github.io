---
layout: post
title: Regex for beginners - detect!
---

Introduction to Regular Expressions (regex) in R: how to detect patterns

## Intro

As a Data Scientist you should know how to use regular expressions (regex). 

There are several ways how to use regex in R to search for patterns in a text-vector:

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

To return the value instead of the index use parameter ```value = TRUE```:

```R
> grep("a", c("Apple", "Orange", "Lemon"), value = TRUE)
[1] Orange
```

If you want to use {tidyverse} you can use ```str_detect()```from {stringr}. Here the pattern is the 2nd argument (not the first)!

```R
> library(stringr)
> str_detect(c("Apple", "Orange", "Lemon"), "Orange")
[1] FALSE  TRUE FALSE
```

## Case Sensitive

```grep``` is case sensitive by default:

```R
> grep("a", c("Apple", "Orange", "Lemon"))
[1] 2
```

Only "Orange" matches (but not "Apple"), because searching is case sensitive by default.

To switch off case sensitivity you can use the parameter ```ignore.case = TRUE```

```R
> grep("a", c("Apple", "Orange", "Lemon"), ignore.case = TRUE)
[1] 1 2
```
Now "Apple" and "Orange" matches as both contain "a" (ignoring upper/lower-case).

The same using {tidyverse} and {stringr}:

```R
> library(stringr)
> str <- c("Apple", "Orange", "Lemon")
> str_detect(str, regex("a", ignore_case = TRUE))
[1]  TRUE  TRUE FALSE
```

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
"Apple" and "Orange" matches, but not "Lemon", because the "e" in Lemon is not at the end!

## Starts & Ends With

To combine both:

```R
> grep("^A.*e$", c("Apple", "Orange", "Lemon"))
[1] 1
```

* ```^A``` = beginning with "A"
* ```.*``` = any string
* ```e$``` = ends with "e"

To control the number of characters between start and end you can use ```*```, ```+```, ```?``` and ```{ }```:

* ```.*``` = any string 
* ```.+``` = any string with minimum length of 1 character
* ```.?``` = string with length 0 or 1
* ```.{3}``` = exactly 3 characters
* ```.{3,}``` = 3 or more characters
* ```.{,3}``` = maximum 3 characters
* ```.{1,3}``` = between 1 and 3 characters

```R
> str = c("Apple", "Ape", "Ae")
> grep("^A.{2,}e$", str)
[1] 1
```
Only "Apple" starts with "A", ends with "e" and has of 2+ character inbetween!

## Which character?

To search for ANY character you can use ```.```

If you want to be more specific:

* ```[a-z]``` = letter a to z (lower case) 
* ```[A-Z]``` = letter A to Z (upper case)
* ```[ACES]``` = letter A or C or E or S
* ```[0-9]``` = digit (0 to 9)
* ```[1234]``` = digit 1 or 2 or 3 or 4
* ```[A-z0-9]``` = letter (A to Z, a to z) or digit (0 to 9)
* ```[ ]``` = blank (" ")

You can exclude characters too (using ```^```):

* ```[^0-9]``` = non digit (all characters, but no 0 to 9)
* ```[^A-Z]``` = all characters, but no upper case letter (A to Z)

## Character Classes, Groups & Quantifiers

We are looking for words that contain a repetitive letter.

```R
> grep("[a-z]{2}", c("apple", "apple+apple", "appleapple"))
[1] 1 2 3
```
We define the character class ```[a-z]``` (letter a to z) with the quantifier ```{2}``` (two times)
All words contain "pp"! How about detecting a repetitive word?

```R
>grep("apple{2}", c("apple", "apple+apple", "appleapple"))
[1] integer(0)
```

This regex is NOT detecting the repetitive word "apple"! It searches for a repetitive "e".

Detecting the repetitive word "apple" can be done by using brackets.

```R
>grep("(apple){2}", c("apple", "apple+apple", "appleapple"))
[1] 3
```
We define the word as a grouping (using brackets) and the quantifier ```{2}``` (two times).
Here only "appleapple" matches. "aplle+apple" does not match, as there is an other character between the words.

## Escaping

```R
> grep("*.txt", c("f1.txt", "f2.txt", "f3-txt"))
[1] 1 2 3
```

This result may surprise you if you are not used to regex. Here "." is not the character ".", but means "any character". To search for the character ".", we need to "escape" it:

```R
> grep("*\\.txt", c("f1.txt", "f2.txt", "f3-txt"))
[1] 1 2
```

Charcters you need to escape (using ```\\```):

* ```.``` =  ```\\.```
* ```+``` =  ```\\+```
* ```*``` =  ```\\*```
* ```"``` =  ```\\"```
* ```\``` =  ```\\\```
* ```$``` =  ```\\$```
* ```^``` =  ```\\^```

And more: ```?``` ```|``` ```(``` ```)``` ```[``` ```]``` ```{``` ```}```  

## Fixed (Literal)

If you just want to search for a string as it is (literal), you can use ```fixed = TRUE```

```R
> grep(".", c("a.b.c", "a-b-c", "a^b^c"), fixed = TRUE)
[1] 1
```

Here "." is just the character "." (no special meaning). So only the first item matches. Without ```fixed = TRUE``` all three elements matches, because all contain "any character" (meaning of "." as a regex)

```R
> grep(".", c("a.b.c", "a-b-c", "a^b^c"))
[1] 1 2 3
```

You can use ```fixed``` in {stringr} too:

```R
> library(stringr)
> str_detect("a[b", fixed("["))
[1] TRUE 
```

## Mix Regex + Literal

If you want to mix a regex with a literal expression, you can use ```\\Q``` and ```\\E```:

```R
grep(".\\Q[x^2]=\\E[0-9]+", c("a[x^2]=0", "b(x^2)=1")
[1] 1
```

* ```.``` = any character
* ```\\Q[x^2]=\\E``` = string "[x^2]=" (literal)
* ```[0-9]+``` = one digit or more

## Or

You can use ```( | )``` for a logical OR.
Example: detect all filenames with extension ".csv" or ".txt":

```R
> grep(".+\\.(csv|txt)", c("f1.csv", "f2.xls", "f3.txt"))
[1] 1 3 
```

* ```.+``` = any string (min lenth 1)
* ```\\.``` = the character "." (need to escape it)
* ```(csv|txt)``` = "csv" OR "txt

## Examples

### Email format

This is a very simplified email format checker

```R
> pattern <- "^[a-zA-Z0-9_\\.\\+\\-]+@[a-zA-Z0-9\\-\\.]+$"
> grep(pattern, c("bob.hope@me.com", "bob.hope"))
[1] 1
```
Only the first Email matches

* ```^[a-zA-Z0-9_\\.\\+\\-]+``` = Starts with alphanumeric or _ . + - (min 1 character)
* ```@``` = Character "@"
* ```[a-zA-Z0-9\\-\\.]+$``` = Ends with alphanumeric or - . (min 1 character)

### User name

```R
> pattern <- "^[a-z0-9_-]{3,16}$"
> grep(pattern, c("bobhope", "x"))
[1] 1
```

Only the first user name matches.

* Allowed: letter a to z, digit 0 to 9, characters ```_``` and ```-```
* Minimum length = 3
* Maximum length = 16

### Hex Color Code

```R
> pattern <- "^#[a-fA-F0-9]{6}$"
> grep(pattern, c("#00FF12", "#xxff"))
[1] 1
```

Only the first color code matches.

* ```^#``` = must start with "#"
* ```[a-fA-F0-9]{6}``` = 6 character (a to f, A to F and 0 to 9 allowed)
* ```$``` = end of string

## Continue ...

with pattern extraction & greedy matching<br>
<https://rolkra.github.io/regex-for-beginners-extract/>
