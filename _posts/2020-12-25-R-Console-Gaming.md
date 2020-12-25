---
layout: post
title: R Console Gaming
---

Writing Games that run in the R console

## Is it even possible?

R is a great language for doing statistics and data science, but it is not designed to run games. So obviously writing games in R is more a fun project. 
But during the corona-lockdown I started getting interested into this topic. I found out, that there are some games written in R that are running in the R console:

* [The Secret of Landusia] (https://lucidmanager.org/data-science/text-adventure/) - A Text Adventure in the R Language
* [Tenliner Cave Adventure] (https://lucidmanager.org/data-science/tenliner-cave-adventure/) - Miniature Text Adventure Ported From the ZX81
* [Hangman] (https://sites.google.com/site/marekhlavac/computer-games-written-in-r) - Classic Hangman Game

[Here](https://lucidmanager.org/tags/r-games/) I found a nice collection of Games writen in R

So, yes it is possible!

## Text Input / Output

Base R has the functionality to input text and write text to the console.

```R
name <- readline("your name = ")
cat("Hello ", name)
```

So, thats probably all you need to write an text adventure. But I wanted to add at least some color and some sounnd.

## Color

To get some color output in the console, I used the package {cli}, that provides functions to control the output in the R console. You can select 
the foreground using col_*() and the background-color using bg_*().

```R
library(cli)
cat("text")
cat(col_blue("text"))
cat(bg_blue("text"))
```
So I was able to create some very basic "sprites" by using a space (" ") and setting a background color.

```R
library(cli);

sprite_show <- function(txt)  {
  for (i in 1:nchar(txt)) {
    char <- substr(txt, i, i)
    if(char == "R") {cat(bg_red(" "))}
    if(char == "B") {cat(bg_blue(" "))}
    if(char == "C") {cat(bg_cyan(" "))}
    if(char == "G") {cat(bg_green(" "))}
    if(char == "M") {cat(bg_magenta(" "))}
    if(char == "Y") {cat(bg_yellow(" "))}
    if(char == "W") {cat(bg_white(" "))}
    if(char == "X") {cat(bg_black(" "))}
    if(char == ".") {cat(" ")}
    if(!char %in% c("R","B","C","G","M","Y","W","Y","W","X",".")) {cat(char)}
  }   
} # sprite_show() 
```

Now I can "draw" a golden key in the R console!

```R
txt <- paste0(
    "..............YYYY.", "\n",
    ".............YY..YY", "\n",
    "...YYYYYYYYYYYY..YY", "\n",
    "...Y.Y.......YY..YY", "\n",
    "...Y.Y........YYYY.", "\n")
  
sprite_show(txt)
```






