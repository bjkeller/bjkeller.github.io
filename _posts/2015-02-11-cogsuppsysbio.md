---
layout: post
title: "Forget the spindling and the mutilating: it's the people"
date: 2015-02-11
---

I'm not one for hyperbole, so I had headed down a track that I wasn't prepared to follow when I started my posts by being clever with the ["please don't fold" story](http://bjkeller.github.io/2014/11/07/please-dont-fold.html) as a spin off the title of the site.

What was going to be the subject for *spindle* or *mutilate*?

What is interpreting incidence data as a matrix? Is it mutilating or spindling? Both are a little over the top. So, each time I started writing, I would decide that what I'd picked wasn't really either.

Of course, that previous post hints at the gist of what I want to get across, which is that the problem we solve should come from the people for whom we are solving it.
So, while it is easy to think of folding an incidence into a concept graph, that is just an example: we are doing analysis or solving problems for people who have their own ways of thinking about them, and we have to find ways to honor those ways of thinking or we are wasting our time.

The cognitive perspective that I learned from Barbara Mirel (U.Michigan) is basically this:
experts have particular ways that they think about and perform their tasks, and tools encode particular ways of thinking about and performing tasks.
It is the relationship between these ways of thinking that should be the focus of our concern.

For example, in a biological setting, the biological expert views their data from the perspective of their experiment, and understands the kinds of questions they want to ask of it. While the tools that they have available represent the data in a particular way, and allow manipulations based on that representation. The expert is then required to translate their questions into the manipulations allowed by their tools.

In some ways this is like needing to hammer a nail while only having a screwdriver. We can solve the problem, but maybe not as well as we would with the right tool. In the case of software tools, the bigger the cognitive mismatch between the tools and how the user views their tasks, the more they have to think about the translation, and the less they can think about their actual problem. What Barbara saw when she observed users of systems biology tools was that they were getting stuck before they could make real insights, because the tools didn't support the way they thought about their data.

I think there are a lot of factors that lead to this situation, but there are two basic ones: the inherent uncertainty in the problems means there may be many different plausible solutions, and problems are often considered out of context.
So, it is easy to look at a question that a scientist has about their data, and, because the data looks like a graph, frame it as a graph question. Since the transformation looks reasonable, the scientist will nod approval, and off we go. And, now that we have a graph, we can manipulate the data like a graph, and ask graphy questions of the graph. Perhaps we get some insights, but we've shifted to a computational representations and problem that is a proxy for the originals, the cognitive connection is lost, and it is harder to move to the next question.

In thinking about about what I learned working with Barbara, and what I've learned since, these are the quick lessons I take from this perspective:

1. *We see what we recognize.* I have learned to be skeptical about any representational proxies I choose.
2. *Don't stray too far from the biology* I try to keep original data in the same shape it came in until there is a reason to present it some other way. This is why I like FCA --- the incidence relation is still there. Basically, this means that you can solve problems in your favorite model from discrete math, but be prepare to present results in a way that makes biological sense.
3. *Any analysis is part of a larger question*. Users need to be able to take the results of one analysis and use it as input to another. Also, relevance or significance is determined by the global question, so we need to be careful in filtering.
4. *Understand how biologists think about their tasks*. I've spent a lot of time working directly with scientists formulating questions, but this is expensive. So, basically, this means we need to engage in cognitive task analysis, and should build off of cognitive models of experts' work whenever possible.
5. *Embrace the uncertainty.* In other words, be "agile". (We'll have to get back to this one.)

I expect I'll come back to some of these, but others will probably show up behind the scenes.
