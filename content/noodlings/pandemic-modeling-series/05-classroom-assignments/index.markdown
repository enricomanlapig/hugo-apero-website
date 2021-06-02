---
title: Classroom assignments
author: Enrico Manlapig
date: '2021-04-04'
slug: []
categories:
  - modeling
tags:
  - covid-19
  - optimization
  - AMPL
  - MathProg
subtitle: ''
excerpt: 'Using mathematical programming to optimize classroom assignments'
---






![contemporary aboriginal art](featured.jpeg)

*Language of the Earth by [Sarrita King](https://artisticsolutionsgroup.com.au/). Used with permission.*

At the beginning of the pandemic, when classes were moved online, I reached out to the college administration to see if they needed or wanted decision support.  I didn't really expect anyone to take me up on the offer - people have their own way of doing things and ORMS techniques can be hard to sell at the best of times.  Still, I was convinced that these tools can help, so I offered.

To my surprise, I was invited to share some of my thoughts! I shared the [dynamic network](../02-dynamic-network-visualization) animation, the [SIR models](../03-sir-simulations/) and even the [discrete event simulation of the Dining Commons](../04-simulating-the-cafeteria/).  In the next few posts, I'll you some  more prescriptive models, I thought might be most helpful.

One of those, the only one that really got some real use was a class assignment model.  The thinking was this:  Most schools had gone online but we have relatively small classes and a small student body.  We also have beautiful mild weather all year around.  Would it be possible to teach in person while maintaining social distancing?  

Some colleagues physically visited every classroom, and every potential classroom, to estimate its capacity to maintain social distancing.  They imagined where the instructor would stand and even considered obstructions like poles in their estimates. To pull it off, we would need to serve the same number of students using half the number of chairs.

Okay, I have to tell you: I love this kind of challenge.  I love OR.  So fun.

I built a simple integer program that shuffled classes into new spaces at their assigned time.  We committed to maintaining the same schedule. This reduced the number of variables but also ensured that students and faculty wouldn't have scheduling conflicts.  One less drama.



At first, I allowed classes to use spaces with insufficient capacity and sought to minimize the total excess demand. I got a little worried that the model might try to accommodate the largest classes while disrupting many small classes so I redefined the objective function to minimize the number of classes disrupted. I won't bore you with the details, but the general idea was:

* Minimize classes disrupted with a small penalty for unmet registrations and a tiny, tiny reward for keeping the class in its currently assigned room)
* Subject to
    - A usage constraint on classes: Each class may have only one room per schedule pattern
    - A usage constraint on rooms and days/times: A room may have only one class in it at each time of each day
    - A usage constraint on rooms and schedule patterns: A room may have only one class in it in each schedule pattern
    - A disruption permission constraint: Declaring a class disrupted allows a class to go over capacity
    - A constraint that computes registrations constraint for each class
    - Some constraints to allow/block certain class/room/time assignments.
    
The penalty/reward system was just to prioritize the various objectives in the case of ties (or near ties).

In terms of data, the model took as inputs:

* All existing classrooms with reduced capacities, rooms that could be converted into classrooms, and tents that could be erected.
* Class schedules and typical Fall enrollments for these classes

This amounted to 30 to 40 spaces (depending on what was allowed to be a classroom), around 5000 enrollments across 300 classes scheduled throughout the week.  

I built the model in [*GLPK*](https://www.gnu.org/software/glpk/) because I love [*AMPL*](https://ampl.com/) and *MathProg*. 

The results were very encouraging: by shuffling the class assignments, it's possible to maintain the same class schedule while disrupting 50 classes with around 200 enrollments without a socially distanced seat.  Not half bad!  I was expecting much worse. And, adding a few tents would help tremendously.

The college then surveyed faculty to see who wanted would remain online.  It offered students an option to remain online.  And, after a bit of to-and-fro with the county, it erected a whole bunch of tents.

It's April 2021 now.  Almost a year after I built and used this model.  By all accounts, the college successfully hosted the vast majority of its students on campus.  Many classes elected to remain online and many tents went underutilized.

It was so satisfying to have a model actually used.  Can't say this was the case for the other models, but hey, I'll take it!
