---
layout: post
title: "Whence our data"
date: 2015-04-15
---

In my [reset post](http://bjkeller.github.io/2015/02/11/cogsuppsysbio.html), I enumerated some lessons about data and the way people think about it.
The first was that _we see what we recognize_. This is a theme in my stories, because seeing our data in the wrong way can lead us in the wrong direction. When we talk about kinds of data, we might think of data as being something like tables, graphs or text; or maybe numeric or ordinal.

We see what we recognize. So, if we see data in a table, we are going to see it in the context of how we learned about tabular data.
I've already written about my story of seeing an [incidence relation as a bipartite graph](http://bjkeller.github.io/2014/11/07/please-dont-fold.html) and what happened, but we get the same effect from tabular data. A table looks like a matrix. A column or row looks like a vector.

Just like we might be inclined to do graphy things with a graph, we are even more inclined to do matrixy things to something that looks like a matrix.
Whether that is a problem or not, we'll have to explore later, but, for now, let's just consider that we need to be more careful to understand where our data comes from and what representations of data mean.

## Informational proxies and forgetfulness

Let's imagine a scientific setting as the source of the data we are to analyze.
A scientist is studying a physical system, say something like inflammatory response of epithelial cells of kidney tubules. The scientists have a number of ways to observe this response, each of which generates data.

Remember that to support the user in understanding their data we have to [keep in mind how they view their own problem](http://bjkeller.github.io/2015/02/11/cogsuppsysbio.html). There are other goals, but, in the contexts in which I've worked, the scientist's goal is generally to reason about the system based on the observations they make.

If we think in terms of the system being studied, observation is _forgetful_. We can only observe what our instruments allow, and so only see some aspects of the system – generally losing relationships that exist. It might be that a scientist will make observations in a way that the structure among observations is preserved. A simple example from soil science is measuring the depth of soil layers in cores drilled in a grid across a study area. In this case, keeping the observations in a grid allows us to infer the soil structure across the study area. But, often, observations are discrete, and while we are interested in how the observed aspects of the system relate, we do not know beforehand.

In fact, the raw data only represents the observations through the filter of the instruments used. So, not only are the observations a proxy of the real system, but the data we see is only a proxy for those observations. Data _clean-up_ is needed to get it into a form that represents what the scientist thinks of as an observation.

In particular, high throughput observation technologies commonly in molecular biology can make large numbers of discrete observations in a way that the observations can be related by temporal or spatial artifacts. These artifacts may be due to how the process starts, or physical properties of the instrument components. As a result, apparent relationships among the observations could be due to the peculiarities of a technology, or even a particular machine. So, the data clean-up has to correct for those effects.

## Understanding our data better

The implication of all this is that, to keep things straight, we need to understand that the following are different:

- what is observed and the relationships among observations,
- how data is (re)presented for human or computational consumption, and
- how data is represented mathematically in analysis.

Raw data and the features extracted from it, fall into the middle category – they are _informational proxies_ for the observations. This is where we see data in the form of table/graph/text.

This is where we can begin to do better. Just like in my ["don't fold"](http://bjkeller.github.io/2014/11/07/please-dont-fold.html) story, we need to be careful not to allow the structure of these proxies to influence our understanding of the problem we are trying to solve.
Any time we impose structure on the data that is not there originally, we muddy the waters. This is clear in the example of the structure imposed by high throughput technologies, which has the potential to create uncertainty about whether dependencies within the data are due to the structure or actual relationships.
Similarly, we need to be conscious that the choices we make in working with data might be introducing structure that is not there, or removing structure that is. There are situations where inducing or losing relationships may not matter, but it still should be a clear decision to do so.
