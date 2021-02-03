---
layout: post
title: Let's grow trees - the easy way!
---

The fast way to create and visualise Decision Trees using {explore}  

![Who is in the bus?](../images/trees-thehardway.jpg)

## Decision Trees

Decision Trees are an "old" machine learning method to create a model that predicts the value of a target variable based on several input variables. The big advantage of Decision Trees is, that the result is easy to understand for humans!

The most popular package to create Decision Trees in R is {rpart}. For visualisation of trees {rpart.plot} is frequently used.


## Growing Trees
### The hard way

Using {rpart} and {rpart.plot} can be timeconsuming, as there are a lot of different parameters to set and the code for using a categorical target differs from using a numeric target. So instead of growing a tree fast, you end up in searching for code syntax in the help-files or searching the web.

### The easy way

{explore} offers a simple function to grow and visualise a Decision Tree. 

In this example we will use the following packages
```R
library(dplyr)
library(explore)
library(palmerpenguins)
```

Creating a Decision Tree explaining the sex-variable is just this line of code:

```R
penguins %>% explain_tree(target = sex)
```

![Who is in the bus?](../images/trees-pinguins-sex.png)

