---
layout: post
title: {explore} making of
---

# {explore} 1.0.0

I am excited to announce the release of {explore} 1.0.0!

{explore} simplifies exploratory data analysis!

```R
library(explore)
create_data_app() |> explore()
```

![explore](../images/explore-app.png)

![explore](../images/explore-app-tree.png)

Time to look back:

## The beginning

In 2018 I was working as a Data Scientist for a big telecommunication company. I was writing a lot of R code for exploratory data analysis (EDA). I really loved R as a programming language, but it felt somehow wrong. I was spending so much time writing code, searching for the correct syntax in help files and on the web. My brain was blocked by these things. It was like trying to write a poem, but thinking way too much about grammar.  

There must be a better way.

I started inspecting the code I wrote for EDA. And there was so much repetition. It's time to pack some of this code into function! After a while I collected quite a number of useful functions and found out that putting these functions into an R package isn't as complicated as I thought.

## Start sharing

So I created my first R package with myself as the only user.

After a while some of my colleagues were getting interested in the package (it was not called {explore} at this time), so I decided to share the package within the company. Now I started to understand the benefit of writing R packages. My code helped others to do EDA much faster, and I got a lot of useful feedback.

## Go CRAN

After a while I realized that this package could help people outside of my company too. I started to inform myself if I as an employee was allowed to share R code as open source. It was difficult to get an answer, because I was the first in this company who asked to publish an R package as open source.

Luckily I got a “go” after a while and I started working on a CRAN package.

### Choosing a name

And I needed a package-name. I did a brainstorming and came up with:
* deexr (de)scribe - (ex)plore (r)eport
* eda
* edaR
* exploreR (which was already the name of an existing packages)
* explore

I was surprised that “explore” was still available. After a few days I was unsure if I am even allowed to pick such a general name for my first package. But then I decided to be brave and picked {explore}!
 
### Following the rules 

My first submission to CRAN was a disaster. I was overwhelmed by warnings, errors and complaints not following CRAN rules.

```
…does not pass the incoming checks automatically
```

I was really surprised how strict these rules are. Even a simple misspelling of a word in the DESCRIPTION file was not acceptable.

After my package was rejected (again) with the following message:

```
Thanks, we see:

         Possibly mis-spelled words in DESCRIPTION:
         grafically
```

 I was really thinking of giving up.

Luckily I was finally able to fix all the problems and {explore} hit CRAN on May 2019!

### Hexsticker

Finally the packaged needed a hex sticker. Luckily {hexSticker} helped a lot:

![hexsticker](../images/hexsticker-all.jpg)

## Improving

I started getting more used to CRAN and its rules and was able to slowly improve {explore}

What I loved most was to get feedback from other users. The most surprising one was a user that asked to support Japanese Fonts in Data-Column names:

```
explore(PatientStress,ID,ストレッサー得点) 
```

I was impressed that {explore} is used in Japan for medical analysis and so I decided to fulfill this wish.

![Japanese](../images/explore-japan.png)

## Version 1.0.0

2 ½ years after putting the first version on CRAN, I now finalized version 1.0.0.

Enjoy!
