---
layout: post
title: Let's {explore} count-data!
---

{explore} offers a simple interface for Exploratory Data Analysis (EDA) of count-data!

## What are count-data?

Data are stored in tables most of the times. Tables have rows, columns and cells:

|           | column 1  | column 2  | column 3  | ... |
| --------- | --------- | --------- | --------- | --- |
| row 1     | value     | value     | value     | ... |
| --------- | --------- | --------- | --------- | --- |
| row 2     | value     | value     | value     | ... |
| --------- | --------- | --------- | --------- | --- |
| row 3     | value     | value     | value     | ... |
| --------- | --------- | --------- | --------- | --- |
| ...       | ...       | ...       | ...       | ... |
| --------- | --------- | --------- | --------- | --- |

This data is called **tidy** if:

* each row is an observation
* each column is a variable
* each cell is a value

So for the Titanic-dataset each row is representing a person on the ship. 
Each column is representing a variable (like age or gender). And each cell is representing a value (like gender of a specific person is "Male")

|           | Age       | Gender    | Survived  | ... |
| --------- | --------- | --------- | --------- | --- |
| Person 1  | 20        | Female    | Yes       | ... |
| Person 2  | 44        | Male      | No        | ... |
| Person 3  | 7         | Male      | Yes       | ... |
| ...       | ...       | ...       | ...       | ... |


Now lets take a look to **count-data**

| n         | Age       | Gender    | Survived  | ... |
|-----------|-----------|-----------|-----------|-----|
| 10        | Adult     | Female    | Yes       | ... |
| 20        | Adult     | Male      | No        | ... |
| 5         | Kid       | Male      | Yes       | ... |
| ...       | ...       | ...       | ...       | ... |

Each row does not represent one person anymore:

* each row is a group of people with similar attributes (like age-category, gender and survived)
* one column is a numeric variable representign the number of observations (in this case n)
* the rest of the columns are categorical variables
* each cell is a value

# Why use count-data?

They save a lot of disk-space and memory!


