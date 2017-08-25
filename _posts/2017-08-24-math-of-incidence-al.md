---
layout: post
title: "The (Unadulterated) Mathematics of Incidence: Attribute Logic"
date: 2017-08-24
---

As promised in the [previous MOI post](http://bjkeller.github.io/2015/05/21/math-of-incidence-ia.html) on Incidence Algebra, I'm going to switch back to the concept analysis view of things before continuing with other perspectives.
This post deals with attribute logics, which will look familiar for those who know about association rules in data mining.

If you read [Ganter and Wille][GanterWille], the motivation for attribute logics is to provide a way to build a concept lattice when we don't know the formal context: first forming the implications of the logic, and then using those to construct the concept lattice.
However, even if we start from a formal context, an attribute logic is interesting because it describes relationships among attributes in a different way than the corresponding concept lattice: as implications between sets of attributes.
The subject also naturally motivates the idea of a basis --- in this case, a subset of the attribute logic sufficient to construct the whole logic --- because, as we'll see, we will want to be lazy.

Once again, I'm adhering to the informal tag-line of *Most of the Math, with none of the motivation*.
Unfortunately, this topic has no general resources other than [Ganter and Wille][GanterWille], but it does overlap heavily with the topic of association rules in data mining, for which you should be able to find plenty of resources.
If you haven't already gone through the [first post](http://bjkeller.github.io/2015/03/27/math-of-incidence-fca.html) on Formal Concept Analysis, start there.
And, in case you haven't gotten the idea yet, don't expect any proofs.

##Implications of attribute logic

Assume a formal context $$\mathbb{K}=(G,M,I)$$ that consists of a set $$G$$ of objects, a set $$M$$ of attributes, and the incidence relation $$I\subseteq G\times M$$.
As we have seen before, the relation $$I$$ gives us the functions $$\phi(A)=\{b\in M\,\vert\, (a,b)\in I, a\in A\}$$ for $$A\subseteq G$$, and $$\psi(B)=\{a\in G\,\vert\,(a,b)\in I, b\in B\}$$ for $$B\subseteq M$$.

An *implication* in the context $$\mathbb{K}$$ is $$A\rightarrow B$$ for $$A,B\subseteq M$$.

Of course, not all of these possible implications represent relationships among attributes in the context.
If we think of the sets $$A$$ and $$B$$ as conjunctions of propositions, then we want the implication $$A\rightarrow B$$ to represent a statement of the form
"if A is true for an object $$g$$, then B is true for the object $$g$$", which
would hold in context $$\mathbb{K}$$ if $$\psi(B)\supseteq \psi(A)$$.

With some hand-waving, we can see that we can guarantee this conceptual relationship when $$B\subseteq\phi(\psi(A))$$.
So, we say that $$A\rightarrow B$$ *holds* whenever $$B\subseteq\phi(\psi(A))$$.
When the context needs to be clear, I'll write this using the notation $$\mathbb{K}\models A\rightarrow B$$.

To understand this definition, remember that
$$
\phi(\psi(A))=\{ m^\prime\in M\,\vert\, \exists m\in A, (g,m)\in I, (g,m^\prime)\in I\}
$$
is the closure of $$A\subseteq M$$ relative to the incidence relation $$I$$.
It is also the extent of the concept $$\mu A$$.

The collection
$$\mathfrak{A}(\mathbb{K}) = \left\{ \mathbb{K}\models A\rightarrow B\right\}$$ of implications that hold in $$\mathbb{K}$$ is the *attribute logic* of $$\mathbb{K}$$.
Since we are just interested in the implications in this logic, I'll just drop the $$\mathbb{K}\models$$ qualifier on implications for the rest of this post.

Let's look at the implications that hold for the context with the incidence relation

| | $$a$$ | $$b$$ | $$c$$ | $$d$$ | $$e$$ |
$$w$$ | x | x | | | |
$$x$$ | x | x | x | x | |
$$y$$ | x | x | x | x | x |
$$z$$ |   | x |   | x | x |

This is the context from the
[first post](http://bjkeller.github.io/2015/03/27/math-of-incidence-fca.html)
except with object names changed to protect the innocent from notational conflict.

We can construct the implications of the attribute logic by selecting a set $$A\subseteq M$$, and then writing down the implications for subsets of $$\phi(\psi(A))$$.
For instance, let $$A$$ be $$\{a\}$$ for which $$\phi(\psi(A)) = \{ a,b\}$$.
Writing a set $$\{ x,y\}$$ as $$xy$$, this pair of sets gives us the implications

$$
\begin{align*}
a &\rightarrow ab\\
a &\rightarrow a\\
a &\rightarrow b\\
a &\rightarrow \emptyset
\end{align*}
$$

Next, consider the set $$\{b\}$$ as $$A$$.
Here $$\phi(\psi(\{b\}))= \{b\}$$, and so the implications are

$$
\begin{align*}
b &\rightarrow b\\
b &\rightarrow \emptyset
\end{align*}
$$

We could keep going this way: selecting a set of attributes, then constructing the implications for that set.
But enumerating all the implications that hold for the context is going to take a while.

The reason?
There are many sets $$A\subseteq M$$, and $$2^{\left|\phi(\psi(A))\right|}$$ implications for each set $$A$$, giving a total count of

$$
\sum_{A\subseteq M} 2^{\left|\phi(\psi(A))\right|}.
$$

The attribute logic of the example context has 596 implications, which is enough that I don't want to enumerate them.
(Be sure to check my math.)

However, it turns out that many of these implications are uninteresting; including some that we have already seen such as $$a\rightarrow a$$, $$ab\rightarrow a$$, and $$a\rightarrow\emptyset$$.
These are implications that hold regardless of the context, and that we don't need to construct.

One way we could avoid having to build these implications is to identify rules that tell us when an implication holds.
For instance, here is a rule that we can derive from the definition of an implication of the logic:

  If $$A\rightarrow B$$ and $$A\rightarrow C$$ both hold, then $$A\rightarrow B\cup C$$ holds.

This rule allows us to only consider implications where the consequence (the right hand side) is a singleton that is not part of the premise.
Clearly this allows us to build fewer implications, the count being

 $$
 \sum_{A\subseteq M} \left|\phi(\psi(A))\right| - \left|A\right|.
 $$

For our example, this is 42 implications, which is still more than I want to write down, so we either need more rules or a different approach.

##Implications and the lattice

Before we get further into reducing our set of implications, let's pause and look at how the
implications relate to the attribute powerset.
The lattice diagram of the powerset lattice of the attribute set is shown below.
(The lattice is drawn as the dual -- meaning it is drawn upside down -- because of the Galois connection derived from the context.)

![The five element powerset lattice for our example.](/figures/moipt3/lattice.svg)
{: style="text-align: center"}

Remember that the Galois connection with the object sets partitions this lattice into the intents of the formal concepts of $$\mathbb{K}$$.
Each blue blob in the diagram corresponds to one of these partitions.
Each partition is an equivalence class of sets
$$[A]=\left\{ B\subseteq M\,:\,\phi(\psi(B))=\phi(\psi(A))\right\}$$.
And, for each class $$[A]$$, $$\phi(\psi(A))$$ is the largest element, shown
as the bottom element of each blob in the diagram.

The definition of $$\mathbb{K}\models A\rightarrow B$$ tells us that the implications for
$$A\subseteq M$$ are determined by the subsets of $$\phi(\psi(A))$$, which is just the powerset $$\mathcal{P}(\phi(\psi(A)))$$.
For our example, when $$A=\{a\}$$, $$\phi(\psi(A)) = \{a,b\}$$, the powerset $$\mathcal{P}(\{a,b\})$$ corresponds to the larger (yellow) blob of the following sub-diagram of the full lattice.

![The sublattice for ab implications](/figures/moipt3/ab-lattice.svg)
{: style="text-align: center"}

The implications listed above for $$\{a\}$$ correspond to the arrows shown here

![The implications](/figures/moipt3/ab-rules.svg)
{: style="text-align: center"}

As our first computation above suggests, the fact that the implications involve all elements of the powerset is why there are so many of them.
Restricting the implications to those with singleton consequences halves the number of implications for this particular set, but obviously reduces the number even further for each $$A$$ with larger $$\phi(\psi(A))$$.
But even this set of 42 implications makes for a messy diagram as shown here.

![The implications with singleton consequence](/figures/moipt3/singleton-rules.svg)
{: style="text-align: center"}

##Closed sets and bases

What we had done to get to this smaller set is to find a rule that allowed us to construct implications from a smaller set, and then decide what the elements of that smaller set were.
We want to do this again, but in a way that gives us even fewer implications.

I really want is to find a small subset of implications that tell me the remaining implications of $$\mathfrak{A}(\mathbb{K})$$ through some simple constructions.

A set of implications is *closed* whenever

1. $$A\rightarrow A$$ is an element
2. if $$A\rightarrow B$$ is an element, then $$A\cup C\rightarrow B$$ is an element
3. if $$A\rightarrow B$$ is an element, and $$B\cup C\rightarrow D$$ is an element,
  then $$A\cup C\rightarrow D$$

The *closure* of an arbitrary set of implications $$\mathcal{G}$$ is the minimal closed set $$\left\langle\mathcal{G}\right\rangle$$ containing $$\mathcal{G}$$.
The set $$\mathcal{G}$$ is a *basis* for $$\left\langle\mathcal{G}\right\rangle$$ if there is no $$\mathcal{F}\subset\mathcal{G}$$ such that $$\left\langle\mathcal{F}\right\rangle = \left\langle\mathcal{G}\right\rangle$$.
There are several ways to define a basis for $$\mathfrak{A}(\mathbb{K})$$, so let's consider a basis called the *stem-basis*.

Let $$P\subseteq M$$, then $$P$$ is an *pseudo-intent* if and only if
$$P\neq \phi(\psi(P))$$ and $$\phi(\psi(Q))\subseteq P$$ for all pseudo-intents
$$Q\subset P$$.
(Depending on the context, the empty set is a pseudo-intent if $$\emptyset\neq \phi(\psi(\emptyset))$$.)
The stem-basis is the set of implications $$P\rightarrow \left(\phi(\psi(P))\setminus P\right)$$ for pseudo-intent $$P$$.
For our example, this set is

$$
\begin{align*}
\emptyset & \rightarrow b\\
bc & \rightarrow ad \\
abd & \rightarrow c \\
be & \rightarrow d
\end{align*}
$$

as shown here

![The stem basis](/figures/moipt3/stem-basis.svg)
{: style="text-align: center"}

When you check my answer for this example, be sure to include the empty set as a pseudo-intent since $$\phi(\psi(\emptyset)) = \left\{b\right\}$$.

## Implications and lattice intervals

Remember that $$\mu A$$ is the concept whose extent is $$\phi(\psi(A))$$, the closure of $$A$$ under $$I$$.
Also, $$\mu A\preceq\mu B$$ means that $$\phi(\psi(B))\subseteq \phi(\psi(A))$$, which, since $$B\subseteq\phi(\psi(B))$$, translates directly to $$A\rightarrow B$$.

On the other hand, say that $$A\rightarrow B$$ holds.
Then $$B\subseteq\phi(\psi(A))$$ and so $$\phi(\psi(B))\subseteq\phi(\psi(A))$$, yielding the interval $$\mu A\preceq\mu B$$.

So, if I have the lattice $$\mathfrak{L}(\mathbb{K})$$, then I can build the attribute logic $$\mathfrak{A}(\mathbb{K})$$, and vice versa.
This means that we can switch between these representations as needed without losing any information.
(You will need to peek at section 2.3 of [Ganter and Wille][GanterWille] if you are looking for more details.)


## Epilogue

The equivalence of the attribute logic and the concept lattice is a critical point in this post.
However, from an algebraic perspective, the important concept here is a basis, and, going further than the discussion here, the closed set generated by a set of implications.
These concepts are completely under developed here, and so, as long as I don't take another two years between posts, perhaps we'll get there.

[GanterWille]: http://www.springer.com/us/book/9783540627715 "Ganter and Wille. Formal Concept Analysis: Mathematical Foundations, Springer,1999."
