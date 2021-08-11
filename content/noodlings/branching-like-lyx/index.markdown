---
title: Transitioning from Lyx to RMarkdown
subtitle: Branching like LyX
author: Enrico Manalpig
excerpt: "I've been on a years-long transition from LaTeX/LyX to RMarkdown. Over the last few days, with help from some kind folks on Twitter, I know how to branch like LyX: the asis engine"
date: '2021-08-09'
slug: []
categories:
  - TIL
tags:
  - LaTeX
  - RStudio
  - LyX
  - Twitter
---

![contemporary aboriginal art](featured.jpg) *Healing our land by [Sarrita King](https://artisticsolutionsgroup.com.au/). Used with permission.*

### Background

I've been a fan of LaTeX for a long, long time. It's flexible, light, and it produces beautiful text. When I discovered [LyX](https://lyx.org) in graduate school, I thought had found my happy place. In industry, nothing was better for documenting the behavior of financial assets. And, when I started teaching, LyX was my go-to typesetting tool for pretty much everything.

With the rise of Markdown and [RMarkdown](https://rmarkdown.rstudio.com/), though, I've grown typeset-curious. RMarkdown is great for adding commentary to my R analyses and, in my opinion, it's the only way to teach R-centric classes. For classes that don't require R, I would always go back to LyX.

Why? What's so great about LyX? Lots! For all the good stuff (read: the math!), writing in LyX is the same as writing in LaTeX. LyX's "What You See Is What you Mean" philosophy, though, makes your text more readable. You don't have to interpret the code, you just read it. For all the annoying stuff, LyX just gets it done. Tables are more convenient to work with than in LaTeX, too. You want to merge cells or add a couple of borders? Easy. Footnotes, images, definitions, formatting, lists, and referencing - LyX just deals with it. No more annoying syntax errors!

My all time favorite feature of LyX, especially as an instructor, is *branches*. You can create one branch for student space and another branch for yourself. I can share prompts with students and keep answers and talking points for myself. There's no repeating yourself - you just put your comments in another branch and you're good to go. Branches are precision instruments, too. You can just as easily branch a paragraph, a single character, or even single entry in a table if you want to.

At the same time, the incredible people at [RStudio](https://www.rstudio.com/) keep adding features to their own IDE: RStudio Desktop. It's arguably the industry standard IDE for anyone working in R. Its community is engaged and enthusiastic so RStudio and RMarkdown is constantly developing and improving and, *gulp*, it can do almost everything that LyX+LaTeX can do. Readability? Check! Table support? Check! Lists, images, referencing? Check! Check! Check![^1]

[^1]: In many ways it can many things LyX and LaTeX don't do very well. I've never had much success with [Sweave](https://wiki.lyx.org/Glossary/Sweave) or doing algebra with [Maxima](https://maxima.sourceforge.io/), for example.

So, like a fanatic, I'm holding out because of LyX's branches. I had briefly looked into parameterising code chunks in R. I know you can some evaluate some chunk and not others With the ability to call images from a chunk, RMarkdown is almost almost there. I could `kable` a table, but I'd have to construct an object first. Meh. And text would be annoying. Plain text through `paste` is fine but But how would you pass an equation, a proof, or a table?

As part of my peek into social media, I decided to ask Twitter. I wasn't sure I'd get a reply, in truth: A few of my past questions fell on deaf ears but when [\@Kierisi](https://twitter.com/kierisi) retweeted my question, the internet started talking to me! 😮

Now I know. It's possible.

### First thought

A couple of folks suggested incorporating LaTeX by including a `include=knitr::is_latex_output()` as a chunk option.  This works.  It's a bit clunky and ugly, but it works.

First, you will need to include your branching switch in your YAML. I've called mine `is_handout`.

![code chunk with yaml](./images/YAML.png)

Then, tell the code chunk you want to toggle to use LaTeX rather than pandoc with an `include=` option.

![code chunk for vertical space](./images/vspace_chunk.png)


The code `\\vspace{5cm}` inserts a vertical space where students can write. *This* is LaTeX! Well, sort of. It has an extra backslash so R knows I really mean to insert a backslash.

For my notes, we can pass `!is_notes`. Again, we're writing plain LaTeX but inserting an additional backslash every time.

![code chunk with equation array](./images/eqnarray_chunk.png)

We can do tables, too! Here's a LaTeX table with a blank in the bottom right cell.

![two code chunks with blank and filled tables](./images/tbl_chunk.png)

Notice again that, I've asked for `!params$is_handout`, since answer should only be available to me.

So it's possible!

I don't want to say, yet, that RMarkdown can do *everything* that I did in LyX. Clearly, there are a lot of backspaces. This code is not as readable or as elegant LyX's method. And it's not exactly the high precision tool that LyX is: I needed to copy the whole table to insert one letter. 

All in all, it's pretty close! Thank you internet!

For all of these little code snippets together, head over to [my GitHub](https://github.com/enricomanlapig/useful_snippets/tree/master/branching_with_latex).

Even though it's possible, there's enough friction that I'm not a 100% sure it's worth moving over yet. 

### Second thought

I discovered now that there are [other engines](https://bookdown.org/yihui/rmarkdown/language-engines.html) that might do what I want. For example, there are `exercise` and `solution` engines in `bookdown`. This might be the way to go but I don't know `bookdown` (yet). It's not clear whether tables and images will be easy to work with, either.

The more I think about it, I wonder how hard it would be to create an RMarkdown engine. A code chunk like this would be ideal.

![dream code chunk](./images/dream_chunk.png)
    
### Third thought

I went back to the thread and asked if my this engine was possible.  I was really worried about this because I was certain the internet wasn't going to be interested in talking to me anymore.  But this morning I got another reply from [yoni sidi (\@yoniceedee)](https://twitter.com/yoniceedee).

How about a chunk option `results = "asis"`?

This had me very excited.  In principle, `asis` will render the output of the chunk verbatim.  So, all we need to do is get the output of the chunk to be markdown.  Output... what gives me control over output? Well, `cat` and `paste` are obvious choices, since they can write anything, but this leaves me in a similar position to the LaTeX approach where we have to remind R not to escape when it encounters a special characters.  



### Fourth thought

The `asis` idea was tantalizingly close! And I remembered that RStudio ships with an `asis` engine.  Holy moly! That's it!

![screenshot of code with asis engine](./images/asis_code_chunk.png)

This is how you do it, people.  Just create a parameter to toggle in your YAML and `asis` will handle the rest. You can create parameters and chunks to customize the output for the instructor, handouts, teaching assistants, and more. And it's so easy.

The only little wrinkle, if you could call it that, is that I don't think you can embed new R chunks in the `asis` chunk. So no emoji fonts or calculations.  That might be a little too Inception-y anyway.  

Now -- finally, after how many years -- I feel confident I can, finally transition from LyX to RMarkdown. What a relif.

Thank you Twitter! 😙 Now, time to start moving things over!
