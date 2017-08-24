---
layout: post
title: "The (Unadulterated) Mathematics of Incidence: Incidence Algebra"
date: 2015-05-21
---

After my
[previous MOI post](http://bjkeller.github.io/2015/03/27/math-of-incidence-fca.html),
this one is is going to seem a little like I just decided to explore a different
subject simply because it has "incidence" in its name. This post introduces
Incidence Algebras, which are generally used in algebraic combinatorics as
defined by [Rota][Rota64]. Just to confuse matters, the "incidence" in
Incidence Algebra has little to do (at least directly) with the incidence
relation of Formal Concept Analysis. But, the point is not just to explore
another version of "incidence", the point is that the incidence algebra gives us
another way to consider lattices using mathematical machinery that is more
computationally useful, or at least familiar.

The "unadulterated" in the title represents my aspiration to an implicit tagline
*Most of the Math, with none of the motivation*,
but I am trying to remember to be a good mathematical writer and add definitions
and background for the uninitiated, but if I happen to miss anything, I would
suggest you find a resource on Abstract Algebra (such this
[first year graduate course text by Ash](http://www.math.uiuc.edu/~r-ash/Algebra.html)).
Most of what is needed on posets and Formal Concept Analysis should be in the
first post, and I give relevant definitions here.
However, this post does have some blatant omissions in the proof department.

## Rings, Fields and Algebras
I expect that most computational readers have learned linear algebra, but
not necessarily abstract algebra. So let's fill in the gaps with some definitions.

A *ring* $$(S,+,\cdot,0,1)$$ is a set $$S$$ closed on addition and multiplication,
where addition satisfies

1. $$a+(b+c)=(a+b)+c$$ (associativity)
2. $$a+b=b+a$$ (commutativity),
3. has identity $$0$$: $$a+0=0+a=a$$, and
4. inverses $$-a\in S$$ for $$a\in S$$: $$-a+a=0$$; and

multiplication

1. has identity $$1\in S$$, $$1\cdot a=a$$, and
2. distributes across addition, $$a*(b+c)=a*b+a*c$$.

A ring $$R$$ is *associative* if multiplication is associative, and *commutative*
if multiplication commutes. We will generally have associative rings, but incidence
algebras are non-commutative.

A *field* is a ring with multiplicative inverses.
The integers $$\mathbb{Z}$$ are a ring, while the real
numbers $$\mathbb{R}$$ are a field.

A *vector space* over a field $$K$$ is a set $$S$$ with sum and scalar products
$$rv\in S$$ for $$v\in S$$ and $$r\in K$$ such that

1. $$r(v+w)=rv+rw$$,
2. $$(r+s)v = rv+sv$$,
3. $$r(sv)=(rs)v$$, and
4. for the unit $$1\in K$$, $$1v=v$$

for $$r,s\in K$$ and $$v,w\in S$$.

An *algebra* $$(A,+,\ast,0,1)$$ over a field $$K$$ is a set $$A$$ with sum,
product and scalar multiplication such that

1. $$(A,+,\ast,0,1)$$ is a ring,
2. $$(A,+,\cdot)$$ is a vector space over $$K$$,
3. $$k\cdot (a\ast b)= (k\cdot a)\ast b= a\ast (k\cdot b)$$ for all $$k\in K$$,
$$a,b\in A$$.

## Incidence Algebra
We are interested mainly in lattices, but the definitions work for posets.
Remember that the interval $$[p,q]=\{ r\in P\,\vert\, p\leq r\leq q\}$$, for
elements $$p\leq q$$ of $$P$$. Let $$\mathit{Int}(P)$$ be the set of intervals in
$$P$$. A poset $$(P,\leq)$$ is *locally finite* if every interval is finite
([Rota64][Rota64]).

Now, let $$R$$ be an associative ring, and $$P$$ be locally finite.
The *incidence algebra* of $$P$$, $$\mathit{I}(P)$$, is the set of functions
mapping intervals of $$P$$ to $$R$$, which we write as
$$f:P\times P\rightarrow R$$ with the property $$f(p,q)=0$$ if
$$p\not\leq q$$, $$p,q\in P$$.
The incidence algebra is closed on sums of functions

$$
(f+g)(p,q) = f(p,q)+g(p,q),
$$

scalar products of functions

$$
(k\cdot f)(p,q) = k\cdot f(p,q),
$$

for $$k\in R$$, and products defined as the convolution

$$
(f\ast g)(p,q) = \sum_{p\leq r\leq q} f(p,r) g(r,q).
$$

Note that this sum ranges over $$[p,q]$$, which is finite by the locally finite
assumption.

This structure is an associative, since the product is associative.
But the algebra is not commutative unless any two elements of $$P$$ are incomparable,
which means that all interesting examples are non-commutative.

The identity element is

$$
\delta (p,q) = \left\{
  \begin{array}{ll}
    1 & \mbox{if}\; p=q\\
    0 & \mbox{otherwise}
  \end{array}
  \right.
$$

for $$p,q\in P$$, and the idempotent elements are

$$
e_p(q,r) =
\left\{
  \begin{array}{ll}
    1 & \mbox{if}\; p = q = r,\\
    0 & \mbox{otherwise}
  \end{array}
\right.
$$

for $$p,q,r\in P$$. An idempotent element satisfies $$e_p*e_p = e_p$$.

From the combinatorics perspective, a couple of the elements of the incidence
algebra are especially useful. The first is the function $$\zeta$$ defined by
$$\zeta(p,q) = 1$$ whenever $$p\leq q$$ and is zero, otherwise.
The second is the function $$\mu$$, which is the inverse of $$\zeta$$, and generalizes
the inclusion-exclusion principle that we see when defining the cardinality of
a set union: $$|A\cup B|=|A|+|B|-|A\cap B|$$.


##Representations
We can define a formal representation of an incidence algebra by representing
intervals symbolically: using $$[p,q]$$ as a symbol. We define the product
as

$$
[p,q][r,s] =
\left\{
  \begin{array}{ll}
    [p,s] & \mbox{if}\; q = r,\\
    0 & \mbox{otherwise}
  \end{array}
\right.
$$

and, then the incidence algebra is $$R$$-linear combinations of intervals

$$
\sum_{[p,q]\in \mathit{Int}(P)} f(p,q)[p,q]
$$

It is an easy switch to thinking of the symbolic $$[p,q]$$ as matrices. To do
this we have to enumerate the elements of $$P$$, then the interval $$[x_i,y_j]$$
corresponds to a $$|P|\times |P|$$ matrix $$e_{ij}$$ with the $$ij$$th-entry
equal to $$1$$ and all other entries zero. Then elements of the algebra can be
defined as linear combinations like before, and with product being the matrix
product.

OK, time for an example. Let's go simple and use the powerset lattice of
the three element set $$\{ a_1, a_2, a_3\}$$ which can be drawn as here.

![Powerset lattice for a three element set](/figures/moipt2/b3.svg "The lattice for the powerset of a three element set has 8 elements")
{: style="text-align: center"}

To represent this lattice using matrices we have to decide how to order the elements.
Let's just use a linear extension of the inclusion order with a lexicographic order
on the elements where $$a_1 < a_2 < a_3$$.
This gives us an order
$$\emptyset < \{a_1\} < \{a_2\} < \{a_3\} < \{a_1,a_2\} < \{a_1,a_3\} < \{a_2,a_3\} < \{a_1,a_2,a_3\}$$
that we use to determine how elements correspond to rows and columns of the matrix.
Here, just using the unit for nonzero entries, we get

$$
\begin{pmatrix}
1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 \\
0 & 1 & 0 & 0 & 1 & 1 & 0 & 1 \\
0 & 0 & 1 & 0 & 1 & 0 & 1 & 1 \\
0 & 0 & 0 & 1 & 0 & 1 & 1 & 1 \\
0 & 0 & 0 & 0 & 1 & 0 & 0 & 1 \\
0 & 0 & 0 & 0 & 0 & 1 & 0 & 1 \\
0 & 0 & 0 & 0 & 0 & 0 & 1 & 1 \\
0 & 0 & 0 & 0 & 0 & 0 & 0 & 1
\end{pmatrix}
$$

In fact, the matrices for a powerset (or Boolean) lattice will always have this
structure with a linear extension of the inclusion ordering.

The fact we can switch into matrix representations is cool enough, but let's pull
in graphs too.  
This is going to seem like I just want to reference my
[dissertation][Keller97] in a post, but really its not (exactly) why.
We are going to look at a different representation of the incidence that we can
also use computationally, which *is* something that the reference to my dissertation
will hint at (but not directly address).

For this, let $$K$$ be a field, and $$\Gamma$$ be
a directed graph, then the *path algebra* $$K\Gamma$$ consists of $$K$$-linear
combinations of finite paths of the graph $$\Gamma$$. We can also define the
incidence algebra this way.

First, remember that $$p\prec q$$ ($$p$$ *covers* $$q$$) means that $$p<q$$ and
there is no $$r\in P$$ such that $$p<r<q$$.
Given a locally finite poset $$P$$, we can create a *covering* graph
$$\Gamma = (P,\succ)$$. The covering graph is a simple directed graph where we
have an arc from $$p$$ to $$q$$ whenever $$p\succ q$$. This is the graph that
we draw as the Hasse diagram of the lattice except now we draw labeled arcs, and
vertices are maybe labeled differently. For our simple lattice, we would have the graph:

![Graph of powerset lattice of three elements](/figures/moipt2/b3graph.svg "The graph for the powerset of a three element set is basically the lattice diagram")
{: style="text-align: center"}

For interval $$[p,q]$$ of $$P$$, there is a subgraph of $$\Gamma$$ consisting of
paths from $$p$$ to $$q$$. We use this set of paths to represent the interval as
a sum of paths from $$p$$ to $$q$$. (Again, it is useful to order the terms, but
we can skip that for now.) For instance, for $$[\{a_1\},\{a_1,a_2,a_3\}]$$ in the
lattice, we have

$$
e_{12}\cdot f_{1} + e_{13}\cdot g_{1}
$$

##Epilogue

My goal is to eventually explain how we can compute over the Galois connection(s)
derived from an incidence relation to discover dependencies within a data set
viewed this way. We could stay in the lattice theoretic framework, but stepping
sideways into an incidence algebra can help us by switching into settings where
definitions/computations are already established – we just have to squint the
right way. Things that could be more natural from this perspective include
defining (information) measures over a concept lattice, studying the Galois connection
as an algebraic object, and using constructions within the incidence algebra to
suggest different algorithmic strategies. I'm not sure I will go to either of the
latter two in these notes, but will at least hint.

Before proceeding with incidence algebras, I will switch back to the concept analysis perspective to look at attribute
logic, and relate it back to intervals and dependencies in the lattice.


[Rota64][Rota64] Rota, G-C.
On the foundations of combinatorial theory.
*Z. Wahrscheinlichkeitstheorie*,
**2** (1964) 340--368.

[Keller97][Keller97] Keller, B.J.
*Algorithms and Orders for Finding non-commutative Gröbner Bases*,
Ph.D. thesis,
Virginia Tech,
1997.

[Keller97]:http://scholar.lib.vt.edu/theses/public/etd-405814212975790/etd-title.html
[Rota64]:http://link.springer.com/article/10.1007%2FBF00531932
