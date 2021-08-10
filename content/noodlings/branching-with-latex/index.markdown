---
title: Branching with LaTeX
author: Enrico Manalpig
excerpt: "My slow transition away from LyX"
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

![contemporary aboriginal art](featured.jpg)
*Healing our land by [Sarrita King](https://artisticsolutionsgroup.com.au/). Used with permission.*



I've been a fan of LaTeX for a long time.  It's so flexible and beautiful and light. And, when I discovered LyX in graduate school, I had found my happy place. When I started teaching, LyX was my go-to typesetting tool.

With the rise of Markdown and RMarkdown over the last few years, I've grown typeset-curious.  RMarkdown great for taking notes and writing things that were R-centric.  And it's the only way to teach R-centric classes. But for classes that don't require R, I would always go back to LyX.

Why? What's so great about LyX? Lots!  For all the good stuff (the math!), writing in LyX is the same as writing LaTeX. But the focus on "What You See Is What you Mean" makes your text much more readable.  For all the annoying stuff, LyX just gets it done.  Tables are more convenient to work with than in LaTeX. Footnotes, images, lists, and referencing - LyX just deals with it.  No more annoying syntax errors!

My all time favorite feature of LyX, though, is *branches*. You can create one branch for student space and another branch for yourself. I can share prompts with students and keep answers and talking points for myself. These branches are precision instruments, too.  You can branch a single entry in a table.

But the incredible people at RStudio have created an keep adding features to their own IDE. RMarkdown continues to develop and, *gulp*, it can do almost everything that LyX and LaTeX can do.  Readability? Check! Table support? Check! Lists, images, referencing? Check! Check! Check!

And so, like a fanatic, I'm holding out because of LyX's branches. I had dabbled in it before.  I knew you could parameterise code chunks so some chunks would evaluate and others would not.  With the ability to call images from a chunk, it's almost there.  Some plain text would, theoretically be possible.  But how would you pass an equation or a table?

As part of my peek into social media, I decided to ask Twitter.  I wasn't sure I'd get a reply, in truth: A few of my past questions fell on deaf ears but when [@Kierisi](https://twitter.com/kierisi) retweeted my question, the internet started talking to me! 😮

Now I know.  It's possible.

First, you will need to include your branching switch in your YAML. I've called mine `is_handout`.
![image of code with parameter highlighted](./images/yaml.png)
Then, tell the code chunk you want to toggle to use LaTeX rather than pandoc with an `include=` option.

![Image of code chunk with option highlighted](./images/blank_space.png)

The code ``\\vspace{5cm}`` inserts a vertical space where students can write.  *This* is LaTeX! Well, sort of.  It has an extra backslash so R knows I really mean to insert a backslash.

For my notes, we can pass `!is_notes`.  Again, we're writing plain LaTeX but inserting an additional backslash every time.

![Image of code chunk with option highlighted](./images/eqnarray.png)


We can do tables, too! Here you can see the first table with a blank space an the second with a `\\mathbf{d}` in the bottom right corner.

![Image of code chunk with option highlighted](./images/table.png)

I don't want to say, yet, that RMarkdown can do *everything* that I did in LyX.  Clearly, there are a lot of backspaces.  This code is not as readable or as elegant LyX's method.  And it's not exactly the high precision tool that LyX is: I needed to copy the whole table to insert one letter.

But it's pretty close!  Thank you internet!

For all of these little code snippets together, head over to [my GitHub](https://github.com/enricomanlapig/useful_snippets/tree/master/branching_with_latex).

I'm going to start moving some things over...
