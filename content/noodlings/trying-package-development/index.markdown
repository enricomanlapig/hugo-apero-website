---
title: Trying package development
author: Enrico Manlapig
exerpt: "I made a package! Introducing my `floweR`"
date: '2021-07-16'
slug: []
categories:
  - modeling
tags:
  - R
  - package development
  - art
subtitle: ''
excerpt: ''
images: ~
series: ~
layout: single
---

I have always wanted to try building a package.  Serious people seem to build packages.  At least, serious people seem to know *how* to build packages. 

But what to make? I was thinking of packaging the [GreatSchools scraper](../scraping-greatschools/) but I'm a bit nervous that it might be too difficult or annoying to maintain.  This may still happen, but not today.  I need something simpler.

Independently, I've been inspired to try making art with R. I'll write more about this later, but I went to an interview with artist [Shirley Wu](https://shirleywu.studio/) about how she got started in data visualization.  She said she wanted to draw realistic flowers.  This seemed like a good place to start. I have much more to say about making art with R but that, too, is for another day.

So I had a go at both!  I made a little script that uses `dplyr::geom_curve` to draw little flowers.  They're not particularly realistic (yet!) -- they're a bit hacky, too symmetric, they need to be filled -- but it's a start.

One of my favorite people on Twitter, [Jesse Mostipak](https://twitter.com/kierisi), did a  [Twitch stream](https://www.twitch.tv/kierisi) on package development.  What perfect timing! I followed along (badly!) but I did it!  

So, a new seed for the garden! A digital [floweR](https://github.com/enricomanlapig/floweR)



```r
#devtools::install_github("enricomanlapig/floweR")

library(floweR)
library(dplyr)
library(ggplot2)


num_petals <- 7

df <- data.frame(
  group = c(rep("A", num_petals),
            rep("B", num_petals),
            rep("C", num_petals)),
  metric = c(runif(num_petals, min = 1, max = 2)*0.5,
             runif(num_petals, min = 1, max = 2),
             runif(num_petals, min = 1, max = 2)*1.2)
)

df %>%
  draw_flowers(group, metric, metric, 
               my_hole_size = 0.5, 
               my_curvature = 0.5, 
               my_angle = 100, 
               my_lwd = 7) +
  
  scale_colour_gradient(low = "purple", high = "pink") + 
  
  scale_fill_manual(values = c("violet", "orange", "yellow")) + 
  
  theme(legend.position = "none")
```

<img src="{{< blogdown/postref >}}index_files/figure-html/draw_flower-1.png" width="672" />

```r
#ggsave("featured.png")
```

![flower graphic](featured.png)
