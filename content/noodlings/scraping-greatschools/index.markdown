---
title: Scraping GreatSchools
author: Enrico Manlapig
date: '2021-06-30'
slug: []
categories: 
  - modeling
tags:
  - R
  - modeling
  - web scraping
  - decision lab
  - consulting
subtitle: ''
excerpt: 'Getting better at webscraping for a new DLab project'
images: ~
series: ~
layout: single
edit: TRUE
draft: FALSE
---


![contemporary aboriginal art](featured.jpg)




*Emu Dreaming by [Raymond Walters Penangke](https://artisticsolutionsgroup.com.au/). Used with permission*

I'm always in two minds about web-scraping.  You can feel like a wizard when you you can identify parts of a webpage and make them appear somewhere, transformed, all without opening a browser.  At the same time, it feels icky.  The designer clearly intended you to experience their page in a certain way so it feels wrong to pick it apart to consume the bits you like.  You wouldn't do this to a beautiful and lovingly crafted piece of nigiri sushi.

This dilemma is for chewing over another day.

Today, I'm planting a new seed and this post will outline some of the things I've learned.  I'm preparing for [Decision Lab](../../dlab/) project that will be exploring the local market for faith-based schools. As part of this exercise, I'm writing some R scripts to help them scrape local school information from [GreatSchools.org](https://www.greatschools.org/).

At this point, I have scripts to scrape a listing page and review pages.

At first, it was hard to get started because the data was being dynamically generated by some JavaScript.  I didn't want to go down the `RSelenium` path because that seemed overwhelming. I learned, though, that you can point [`rvest`](https://rvest.tidyverse.org/) at the script's xpath and then use `V8` to execute the script.  Very clever!

The review pages were trickier.  I could still use the `rvest` + `V8` move to grab the data but there were two little wrinkles.  First, the page would expand when you scrolled down.  If I blindly scraped the page with `rvest`, I'd only get the first few reviews.  The second issue was that each review was initially presented collapsed.  You would need to press a "more" button to expand the review.  Since this required some actual window work, I concluded there was no way to do this with `rvest` alone so I jumped into the `RSelenium` pool.  Thankfully, it was surprisingly straightforward to scroll and click in the client browser.

At the moment, I have everything driven by RMarkdown document for no particular reason.  I would like to try rolling this material into a package, which I think will be a [kinder tool](https://alison.netlify.app/ares-kind-tools/) for the students.

One last thing before I leave the garden for the day, I was practicing bowing and nodding to the website because I wanted to be (and use) [`polite`](https://dmi3kno.github.io/polite/).  As I said earlier, I am a little bit bothered by this practice. But that's for another day. 

Hmm... Now I want some sushi ????
