---
layout: post
title:  utf8ify your text!
---

Format text using {utf8ify} if there is no format option!


## ggplot

**{utf8ify}** your ggplot!

```
library(tidyverse)
library(explore)
library(utf8ify)

title <- paste(
 utf8_text_bold("Beer"),
 utf8_text_italic("Beer"),
 utf8_text_bolditalic("Beer"),
 utf8_text_gothic("Beer"),
 utf8_text_circle("Beer"),
 utf8_collection()$fav["beer"])

use_data_beer() |> 
 ggplot(aes(x = alcohol_vol_pct, y = energy_kcal_100ml)) +
 geom_point() +
 ggtitle(title) +
 theme(plot.title = element_text(size=20))
```

![Ubuntu running R/RStudio](../images/utf8ify-ggplot-beer.png)
