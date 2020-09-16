---
layout: post
title: Let's {explore} count-data!
---

{explore} offers a simple interface for Exploratory Data Analysis (EDA) of count-data!

## What are count-data?

Data are stored in tables most of the times. This data is called **tidy** if:

* Each row is an observation
* Each column is a variable
* Each cell is a value

So for the Titanic-dataset each row is representing a person on the ship. 
Each column is representing a variable (like age or gender). And each cell is representing a value (like gender of a specific person is "Male")

```R
titanic_tidy
```
```
# A tibble: 2,201 x 5
      id Class Sex   Age   Survived
   <int> <fct> <fct> <fct> <fct>   
 1     1 3rd   Male  Child No      
 2     2 3rd   Male  Child No      
 3     3 3rd   Male  Child No      
 4     4 3rd   Male  Child No      
 5     5 3rd   Male  Child No      
 6     6 3rd   Male  Child No      
 7     7 3rd   Male  Child No      
 8     8 3rd   Male  Child No      
 9     9 3rd   Male  Child No      
10    10 3rd   Male  Child No      
# ... with 2,191 more rows
```

We see that the first 10 observations are similar except the id. So the basic idea of having count-data is, to group all similar observations and add a count variable.

```R
library(tidyverse)
titanic <- as_tibble(Titanic)
```
```
# A tibble: 32 x 5
   Class Sex    Age   Survived     n
   <chr> <chr>  <chr> <chr>    <dbl>
 1 1st   Male   Child No           0
 2 2nd   Male   Child No           0
 3 3rd   Male   Child No          35
 4 Crew  Male   Child No           0
 5 1st   Female Child No           0
 6 2nd   Female Child No           0
 7 3rd   Female Child No          17
 8 Crew  Female Child No           0
 9 1st   Male   Adult No         118
10 2nd   Male   Adult No         154
# ... with 22 more rows
```

Now we have a table with just 32 rows instead of 2201 rows without any lost of information!

**Count-data**:

* Each row is a group of observations with similar attributes 
* One column is a numeric variable representign the number of observations 
* The rest of the columns are categorical variables
* Each cell is a value

# Why use count-data?

They save a lot of disk-space and memory!
There where x people on the Titanic. In tidy data, you have x rows.

# Table Test


|           | Age       | Gender    | Survived  | ... |
| --------- | --------- | --------- | --------- | --- |
| Person 1  | 20        | Female    | Yes       | ... |
| Person 2  | 44        | Male      | No        | ... |
| Person 3  | 7         | Male      | Yes       | ... |
| ...       | ...       | ...       | ...       | ... |


