---
layout: post
title: "The complexity of boring data"
date: 2015-06-12
---

Gurjeet Singh (CEO Ayasdi) gave [a great talk at Exponential Finance 2014](https://youtu.be/5lrcb8F6j8s) on data
science in which he walks us through the argument that with increasing data
we should do more to automate the analysis, because for data sets that grow with
time the hypothesis space is growing at a doubly exponential rate.

The argument goes like this, say we have a table of $$n$$ customers with $$m$$
products, then

1. we have $$N = nm$$ cells in the table;
2. each hypothesis over this data is a selection of entries in the table, so the
number of hypotheses is $$2^N$$; and
3. the size of the data set is growing exponentially with time $$t$$ as $$\beta^t$$, and
so the number of hypotheses is growing proportionally to $$2^{\beta^t}$$.

This big number allows Singh to make a quick point in a context where exponentials
are the story, and I'm with him that we do need to exploit the mathematics of data to find the interesting
structures in the data. But, based on my perspective, it got me thinking about how much of this data is boring.

## First, the hypothesis space

That second step was a quick and dirty trick that makes it easy to exploit the
power-law of data sets in the third step.
But, the size of the hypothesis space is not $$2^{nm}$$.

Why? As Singh describes them, each hypothesis is a selection of a set of customers and products.
So, the hypothesis space is all pairs of subsets of customers with subsets of products.
Formally, this is the cross product $$2^n\times 2^m$$ where $$2^n$$ is the powerset of a
set of $$n$$ elements.
This cross product has $$2^n\cdot 2^m$$ pairs. So, the maximum number of hypotheses
is $$2^{n+m}$$. Definitely a smaller, yet still big, number.

## Different "old math used in new ways" (and an even smaller big number)

In [this interview](https://youtu.be/5QZ8BkCi420), Singh talks about how Topological
Data Analysis (TDA) can be traced back to "old mathematics". My perspective on data
comes from a different version of *old math used in new ways*, which in this case
traces back to Galois indirectly through Birkhoff in the 1940s, and resurrected
by Wille in the 1970s. The approach is called Formal Concept Analysis (FCA), but
it is based on a pair of maps between, in our example, sets of customers and sets
of products that is called a *Galois connection*, that are induced by the data set.

What the Galois connection looks like is simplest when the data just reflects a
simple relationship like "Ben bought green curry paste".
Things gets a little slippery when we add values, but let's ignore that at the moment.

If you look at my
[introduction](http://bjkeller.github.io/2015/03/27/math-of-incidence-fca.html) to the
math in the simple case (warning: *most of the math with none of the motivation*),
you'll see a Galois connection drawn for you. What this illustrates is that the data
induces maps that, in our customer-product scenario, relate families of sets of customers
to the representative of a family of sets of products, and families of sets of
products to the representative of the corresponding set of customers.
The key point is that the maps can be used to build a closure based on the data
so that we know, for instance, that "products bought by Ben and Ed"
are also products bought by Gunnar and Gurjeet.
The pairs of representative sets are the *formal concepts* of FCA,
and represent classes of the pairs of sets I have been referring to as hypotheses.

The implication of all this is that there are many hypotheses that can be
collapsed by a closure induced from the data set to the same formal concept.
(We only have a unique closure in the unweighted case.) So, the concept lattice
(the set of formal concepts), represents the effective hypothesis space for the
data set.

The maximum number of formal concepts is determined by the smaller of
the number of customers $$n$$ and the number of products $$m$$. It likely that
$$n < m$$, in which case the upper bound on the number of formal concepts (as
hypothesis representatives) is $$2^n$$, determined only by the number of customers.

## Complexity of boring data

So, I've whittled the number of hypotheses down from Singh's $$2^{nm}$$
down to $$2^n$$ by playing the trick of switching to formal concepts. I've got a
slight problem, in that our growth model is that $$nm\propto \beta^t$$, but sparsity
of data sets tells me that most of the growth is in customers and products. So,
we might as well forget I said that, and say $$n\propto\beta^t$$ instead, meaning
that we get a similar double exponential to before (with appropriate hand waiving about $$\beta$$).

But, there are a lot of hypotheses that we don't even need to consider.
How many? Well, I generally work on the "product"-side of the Galois connection, and
am always a little leery of calculations I haven't done before. Especially those
based on duality, so let's flip perspectives. From the product perspective,
for each individual interesting hypothesis involving $$p$$ products,
there can be up to $$2^{m-p}$$ that we don't even have to look at because they
are implied by the first. This suggests that as long as $$p$$ is small for each
interesting hypothesis of the data set, the irrelevant hypothesis space is
actually what is growing by the double exponential.

So, how much of the data is boring?  My guess is most of it. But, perhaps this
supports Gurjeet Singh's point – let's let the mathematics of the data
guide us in finding the interesting parts – simply because there is a lot of boring to
sort through.
