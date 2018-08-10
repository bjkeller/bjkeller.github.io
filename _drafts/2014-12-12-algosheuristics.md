---
layout: post
title: "Job require algorithms like decision trees, and other stuff I don't understand"
date: 2014-12-12
---

Flipping through the LinkedIn job recommendations, I landed on one for a
Machine Learning (ML) scientist. Somewhere buried in the text was a statement
that the person hired should know ML algorithms. I should have
stopped reading there.

Machine Learning (ML) was born as a subfield of Artificial Intelligence where we
want to build an agent that can both learn from and reason about its environment.
The key to ML is learning a representation of that knowledge that can be used for
reasoning. The tradition of AI is that computational problems that humans can solve
start as AI, and as understanding of the problems grows they move out on their own.
ML still has at least one foot firmly in the AI world, but some hefty chunks of
ML are now under-the-hood of much of what we encounter on the web.

And *everybody wants it*.

If you think about it ML is a relatively complicated idea. We have computational
strategies that learn knowledge representations, many of which capture knowledge
that has a procedural bent to it. As an example, a decision tree encodes a
computation in which we decide how to classify entities based on attributes or
features. But, there are computational strategies to construct decision trees
from a data set, which means we have a computation that learns how to do a
computation. Just *that* is complicated enough, but you have to figure out what
representation you want to learn, and then how to go about learning it.

People, including me, are sloppy about language. So, the job description saying
"ML algorithms" is OK, just the slight hint of a red flag. The reason?
An *algorithm* is a computational strategy that makes guarantees like actually
solving the problem. This requires that the problem be well enough defined that
we can make such a guarantee. A *heuristic* is a strategy that may solve the
problem in general, but may fail to solve the problem in very specific situations.
If we are learning decisions trees, there may be a large number of correct
answers, and we'd have to refine the problem to specify the properties met by
the trees found by a particular heuristic before we could make any guarantees.
Of course, only a vocabulary wonk is going to care, so maybe let's peek ahead.

So, the person hired should know *ML algorithms such as decisions trees,
neural networks,...*. Sounds OK, but, wait, what? No, a decision tree is a
knowledge representation in the ML context. Technically, it is an algorithm
solving some problem, but so trivial we wouldn't even bother. Instead we have
algorithms (or heuristics) that 


I don't view myself as an Machine Learning expert. Instead, I solve problems
that involve discovering dependencies hidden within a data set. Because
dependencies are relationships, it just happens that they have representations,
say, partial functions. So, discovering relationships as partial functions is
basically *learning* partial functions from the data.

, because the examples of ML algorithms they listed were a hodge-podge
of ML-related concepts, none of which are algorithms or even heuristics.

Machine learning is just the latest branch of Artificial Intelligence to find
utility outside of building an intelligent machine, and because it is being used
effectively in a number of settings, everyone wants it. What exactly they want,
they probably could not say, but it is not someone who knows a loose
confederation of concepts.

AI is one of the oldest subfields of computer science, and has pretty much been
the home of any problem that could be done by a human, but we didn't really know
how to do it well on a computer. For many of these problems, eventually, as
theories developed and understanding improved, it would become obvious that less
intelligence was required and they would move off into another subfield. And, we
are seeing something similar with ML.

##ML algorithms

I came out of a theory background, where algorithms are the bread and butter.
For the most part, Machine Learning
