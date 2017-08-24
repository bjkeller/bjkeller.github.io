---
layout: post
title: "The (Unadulterated) Mathematics of Incidence: Concept Lattice"
date: 2015-03-27
---

This post is intended to be a quick and dirty introduction to Formal Concept Analysis – unadulterated by all the things that would make it easier to understand.

I have a series of presentations on SlideShare that introduces Formal Concept Analysis through a recommender systems example. I did rip off the basic example to use here, but I actually stripped it down to its bare essence.
Look [there](http://www.SlideShare.com/BenjaminKeller) if you are looking for a motivated, and slightly slower, introduction.
I'm also not going to be terribly pedantic – e.g., no theorems, proofs or exercises. So, if you are looking for the real math of Formal Concept Analysis, you want to start with the book by [Ganter and Wille][GanterWille].

Here, I'm just going to jump right in.

## Incidence relations
A number of problems involve some form of incidence relation – the recommender example I use in the presentations has Users and Items, but they show up in a number of places.  For FCA, an incidence relation is a binary relation between *objects* and *attributes*.
For this post, we work with a *formal context* $$\mathbb{K}=(G,M,I)$$ that consists of a set $$G$$ of objects, a set $$M$$ of attributes, and the incidence relation $$I\subseteq G\times M$$.

We can also encounter an incidence relation that is weighted, where $$I\subseteq G\times M\times W$$ for some domain $$W$$ of weights. In this case, it is possible to scale the weights so that we could created an unweighted context with attributes that represent the original attributes with the scaled weight. You can think of the scaling as mapping $$(g,m,w)$$ into $$(g,m_{s(w)})$$ in the context where the attributes $$m_{s(w)}$$ are elements of $$M\times s(W)$$.

Different scalings will give us different unweighted incidence relations, and the "right" choice depends on the data and how we should interpret it. So, while, technically, it is sufficient to look at the unweighted cases, eventually we will want to consider alternatives.

## Partially ordered sets and lattices

Let $$P$$ be a set, then $$(P,\leq)$$ is a *partially ordered set* (*poset*) when the order is a relation on $$P$$ that is

1. *reflexive*: $$p\leq p$$, $$\forall p\in P$$,
2. *anti-symmetric*: if $$p\leq q$$ and $$q\leq p$$ then $$p=q$$, $$\forall p,q\in P$$, and
3. *transitive*: if $$p\leq q$$ and $$q\leq r$$ then $$p\leq r$$, $$\forall  p,q,r\in P$$.

For $$p,q\in P$$, we say that $$p$$ *covers* $$q$$, written $$p\succ q$$, if $$p\geq q$$ and there is no $$r\in P$$ such that $$p\geq r\geq q$$.
If the poset $$P$$ has an element $$p\in P$$ so that $$p\leq q$$ for all $$q\in P$$, then $$p$$ is called the *bottom* of the poset and written as $$\bot$$.
Similarly, the *top* of a poset, written $$\top$$, is an element $$r\in P$$ such that $$q\leq r$$ for all $$q\in P$$.

For a poset $$(\mathcal{L},\leq)$$ and $$S\subseteq \mathcal{L}$$, the *least upper bound* of $$S$$ is $$\bigvee S=p$$ where $$p\in\mathcal{L}$$ and $$s\leq p$$, $$\forall s\in S$$; and the *greatest lower bound* of $$S$$ is $$\bigwedge S= q$$ where $$p\in\mathcal{L}$$ and $$q\leq s$$, $$\forall s\in S$$. If $$\bigvee S$$ and $$\bigwedge S$$ exist for any set $$S\subseteq\mathcal{L}$$ then $$\mathcal{L}$$ is a (*complete*) *lattice*.
A *complete* lattice has both a top and bottom.

A standard example of a lattice is the powerset of a set.
For $$G$$, the set of objects of a formal context $$\mathbb{K}$$, the *powerset* of $$G$$ is $$\mathcal{P}(G)$$, the set of subsets of $$G$$.
$$(\mathcal{P}(G),\subseteq)$$ is a poset ordered by set inclusion, and is a lattice with set union as least upper bound, and set intersection as greatest lower bound. The top of $$\mathcal{P}(G)$$ is $$G$$ and the bottom $$\emptyset$$ (the empty set). The powerset is an important example, because it is the canonical Boolean algebra, and is also a major part of the construction we consider in the next section.

The *dual* of a poset $$(P,\leq)$$ is $$(P,\geq)$$ where the order is flipped. So, $$(\mathcal{P}(G),\supseteq)$$ is the dual lattice of $$\mathcal{P}(G),\subseteq)$$. In this lattice, the top is $$\emptyset$$ and the bottom is $$G$$.

We draw lattices using the covering relation (a Hasse diagram). The top of lattice $$\mathcal{L}$$ is drawn at the top. Then for any element $$q$$ in the diagram, add any elements $$p\prec q$$ and draw with a line from $$q$$ to $$p$$. The drawing will stop at $$\bot$$.

Abstracting the example from the slides, let $$G=\{A,B,C,D\}$$. Then the powerset lattice $$(\mathcal{P}(G),\subseteq)$$ can be drawn as

![diagram of powerset lattice: empty set at bottom with singleton sets above, sets of pairs above that – adding one element at each level with sets connected to indicate subsets](/figures/moipt1/powerset1.svg "Powerset lattice for for objects of formal context")
{: style="text-align: center"}

where I've left off the set notation.

##Extending the incidence to powersets
Let's get concrete with a formal context. I'm using uppercase letters to represent objects, so $$G=\{A,B,C,D\}$$; and lowercase letters to represent attributes, so $$M=\{a,b,c,d,e\}$$. The incidence relation (as a cross table) is

| | $$a$$ | $$b$$ | $$c$$ | $$d$$ | $$e$$ |
$$A$$ | x | x | | | |
$$B$$ | x | x | x | x | |
$$C$$ | x | x | x | x | x |
$$D$$ |   | x |   | x | x |

The entries in this table show us which pairs belong to the relation: the 'x' the table entry for row $$A$$ and column $$b$$ means that $$(A,b)\in I$$.

The incidence relates the lattices $$(\mathcal{P}(G),\subseteq)$$ and $$(\mathcal{P}(M),\supseteq)$$ through two functions:

1. $$\phi:\mathcal{P}(G)\rightarrow\mathcal{P}(M)$$, defined as $$\phi(A)=\{b\in M\,\vert\, (a,b)\in I, a\in A\}$$ for $$A\subseteq G$$, and
2. $$\psi:\mathcal{P}(M)\rightarrow\mathcal{P}(G)$$, defined as
$$\psi(B)=\{a\in G\,\vert\,(a,b)\in I, b\in B\}$$ for $$B\subseteq M$$.

These functions form a special relationship between the powersets of objects and attributes that is called a Galois connection.

In general, a pair of functions $$\phi: P\rightarrow Q$$ and $$\psi: Q\rightarrow P$$ between posets $$(P,\leq)$$ and $$(Q,\leq)$$ is a *Galois connection* between $$P$$ and $$Q$$ when

1. if $$p_1\leq p_2$$ then $$\phi p_1\geq\phi p_2$$,
2. if $$q_1\leq q_2$$ then $$\psi q_1\geq\psi q_2$$, and
3. if $$p\leq \psi\phi p$$ and $$q\leq\phi\psi q$$.

It turns out that the functions defined from the incidence relation partition the powerset lattices in a special way so that the relationship between sets of objects and attributes that is hidden in the incidence relation is captured.
To see this, let's start with the set of objects $$\{ A\}$$ and consider what happens when we add other objects:

$$
\begin{align*}
\phi(\{A\}) & = \{ a, b\}\\
\phi(\{A,B\}) &= \{a,b\}\\
\phi(\{A,C\}) &= \{a,b\}\\
\phi(\{A,D\})&= \{ b\}\\
\phi(\{A,B,C\}) &= \{ a, b\}\\
\phi(\{A,B,D\}) &= \{ b\} \\
\phi(\{A,C,D\}) &= \{b\}\\
\phi(\{A,B,C,D\}) &= \{b\}
\end{align*}
$$

Notice that $$\phi$$ maps the sets between $$\{A\}$$ and $$\{A,B,C\}$$ to the attribute set $$\{ a,b\}$$, and the sets between $$\{A,D\}$$ and $$\{A,B,C,D\}$$ to $$\{b\}$$. These ranges of sets are called *intervals*, and for elements $$p\leq q$$ of a poset $$P$$ the interval $$[p,q]$$ is the set $$\{ r\in P\,\vert\, p\leq r\leq q\}$$.

Going the other way, let's focus on subsets of $$\{a,b\}$$:

$$
\begin{align*}
\psi(\{a\}) &= \{A,B,C\}\\
\psi(\{b\}) &= \{A,B,C,D\}\\
\psi(\{a,b\}) &= \{A,B,C\}
\end{align*}
$$

If we look closely we can see that what is happening is that these functions directly relate intervals of each of the powerset lattice with each other. For our example, the relation identifies six intervals in each lattice that are related by the functions.

![The four element powerset lattice for objects is on the left, and the dual of the five element powerset lattice on the right, each partitioned into six intervals that are related by the functions derived from the incidence relation.](/figures/moipt1/galois-example.svg "The induced functions relate intervals of each powerset lattice that partition the subsets")
{: style="text-align: center"}

To be precise, what is happening is that $$\phi$$ maps all of the elements of each interval of $$(\mathcal{P}(G),\subseteq)$$ to the minimum element of the corresponding interval in $$(\mathcal{P}(M),\supseteq)$$ (in other words, the largest set in the interval), and vice versa. This means the composition of the two functions gives us closure operators

$$
\begin{align*}
\phi(\psi(B))&=\{ b^\prime\in M\,\vert\, (a,b^\prime)\in I, (a,b)\in I, b\in B\}\\
\psi(\phi(A))&=\{ a^\prime\in G\,\vert\, (a^\prime,b)\in I, (a,b)\in I, a\in A\}
\end{align*}
$$

This construction gives us the basic idea of formal concept analysis – that certain pairs of object sets and attribute sets represent the fundamental relationships in the incidence relation.

##Formal concepts and the concept lattice
The pairs of sets identified by the Galois connection are the *formal concepts* for the context $$\mathbb{K}(G,M,I)$$ – defined as pairs  $$(A,B)$$ of sets $$A\subseteq G$$ and $$B\subseteq M$$ satisfying $$\phi(A)=B$$ and $$\psi(B)=A$$.
The set of objects $$A$$ is called the *extent*, and the set of attributes $$B$$ is the *intent*.  In terms of notation, for formal concept $$c$$, the extent is $$\alpha(c)$$, and the intent is $$\beta(c)$$.
We can use also the closure directly to construct concepts. Given a set $$A\subseteq G$$, we define $$\gamma A=(\psi(\phi(A)),\phi(A))$$, and given a set $$B\subseteq M$$, we define $$\mu B = (\psi(B),\phi(\psi(B)))$$.

The canonical partial order on formal concepts is the *subconcept* order. Define $$(A_1,B_1)\preceq (A_2,B_2)$$ whenever $$A_1\subseteq A_2$$, or, equivalently, whenever $$B_2\subseteq B_1$$.
The set of concepts over the incidence relation (technically, the formal concept $$\mathbb{K}$$) forms a lattice $$\mathfrak{L}(\mathbb{K})$$ relative to the subconcept order.

To have a complete lattice, we have to have a least upper bound and greatest lower bound for any set of concepts.
Given a set of concepts $$C=\left\{ (A_i,B_i)\right\}_{i\in\mathcal{I}}$$, the least upper bound is defined as

$$
\bigvee C = \left( \psi\phi\left(\bigcup_{i\in\mathcal{I}} A_i\right), \bigcap_{i\in\mathcal{I}} B_i \right),
$$

and the greatest lower bound is defined as

$$
\bigwedge C = \left(\bigcap_{i\in\mathcal{I}} A_i, \phi\psi\left(\bigcup_{i\in\mathcal{I}} B_i\right)\right).
$$

Notice that the intersection is natural in the lattice, while the union requires applying the appropriate closure operator.
When we just have a pair of concepts $$(A_1,B_1)$$ and $$(A_2,B_2)$$, the least upper bound, or *join*, is written $$(A_1,B_1)\vee (A_2,B_2)$$,
and the greatest lower bound, or *meet*, is written
$$(A_1,B_1)\wedge (A_2,B_2)$$.

The concept lattice for our example looks like this

![Concept lattice has six concepts: top with all four objects, bottom with all five attributes](/figures/moipt1/fulllattice.svg "The concept lattice for the example context. Each concept is a pair of object and attribute sets, and corresponds to partition of powersets by functions induced from the incidence relation.")
{: style="text-align: center"}

It is common to simplify the labeling of a lattice diagram using the functions we defined above. If we look in the lattice above above $$\mu m$$, for attribute $$m\in M$$, every concept has $$m$$ in it. And, if we look at the lattice below $$\gamma g$$, $$g\in G$$, we see that every concept has $$g$$. So, the convention is to label $$\mu m$$ and $$\gamma g$$ for each $$m\in M$$ and $$g\in G$$ rather than to label with the full concepts.
For our example, this looks like

![](/figures/moipt1/simplifiedlattice.svg "The concept lattice simplified by labeling with first occurrences of an object or attribute. Each concept above an attribute label has that attribute, and every concept below an object label has that object.")
{: style="text-align: center"}

##Incidence and lattices
The concept lattice captures relationships among the objects and attributes that are implicit in the incidence relation. Sometimes a context will have objects or attributes that effectively don't add any new relationships – they are simply part of relationships that would be there regardless. This happens when the corresponding concepts are either join- or meet-reducible.

A concept $$c$$ is *join-reducible* whenever $$c$$ can be expressed as a join of strict subconcepts: $$\bigvee \left\{ v < c \right\} = c$$, or *meet-reducible* whenever $$c$$ can be expressed as a meet of strict superconcepts: $$\bigwedge \left\{ v > c \right\} = c$$.
The concept labeled by $$m$$ and $$g$$ in the following diagram is both join- and meet-reducible: the concept is the join of the concepts $$\gamma g_1$$, $$\gamma g_2$$, $$\gamma g_3$$; and the meet of the concepts $$a_1$$ through $$a_3$$.

![](/figures/moipt1/reducibility.svg "The object g and attribute m correspond to the same concept that can be expressed as a join or meet of other concepts.")
{: style="text-align: center"}

In general, if the concept $$\gamma g =\bigvee \left\{ v < \gamma g\right\}$$, then the object  $$g\in G$$ is called *join-reducible*; and
if the concept $$\mu m=\bigwedge\left\{ v>\mu m\right\}$$, then the attribute $$m\in M$$ is called *meet-reducible*.

The implication is that a reducible object or attribute can be removed without affecting the structure of the lattice through changes to the  concepts. So, in this example diagram, we can remove the object $$g$$ and the attribute $$m$$ without changing the structure. We can also remove the attribute $$a_1$$ in the top and  the object $$g_1$$ in the bottom since they are trivially reducible. It is also possible to remove objects or attributes that share exactly the same attributes or objects as  another. These two cases are easy to recognize in the cross table, because duplicates will have duplicate rows or columns, an object that corresponds to the bottom will have a row of x's, and an attribute that is the top will appears as a column of all x's. A context where duplicates are removed is called *clarified*, and one where both join and meet reducible elements are removed is called *reduced*.

So, for any particular formal context, there is a family of formal contexts that yield isomorphic concept lattices – identical up to labeling – where some have more labels and some have fewer.
And, when the context is finite, there is a canonical clarified and reduced context called the *standard* context that determines the structure of the lattice for all of the contexts in this family. It is possible to create the standard context from a concept lattice (for the details, see [Ganter and Wille][GanterWille]).

##Epilogue
We have explored the basic definitions and constructions used in Formal Concept Analysis to discover relationships among attributes and objects in an incidence relation.  As I discuss elsewhere, the incidence relation is a common form of data seen in applications such as biomedical research and recommender systems. The concept lattice can be used to describe common data mining constructions such as association rules and decision trees – with the lattice structure allowing the definition of heuristics for association rule and decision tree discovery. Beyond direct application, the lattice provides insight into the structure of the data, in particular the true dimensionality of a data set, since large data sets can collapse to relatively small structures because of redundancies.  For moving beyond the unweighted case, the Galois connection is an important construction to remember, but there is more to consider before we get there.

[GanterWille]: http://www.springer.com/us/book/9783540627715 "Ganter and Wille. Formal Concept Analysis: Mathematical Foundations, Springer,1999."
