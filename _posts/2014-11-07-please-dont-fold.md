---
layout: post
title: "Incidence Data: Please don't fold..."
date: 2014-11-07 09:03:59
---

##Jumping connections

The closest I was to data before Naren Ramakrishnan and I started talking research
was the experimental results in my dissertation.
But, incidence data has dominated nearly everything I've done for the 15 years since.

Naren was interested in recommender systems --- and when we first sat down
together, he sketched out how some different algorithms worked, and we started
exploring how they are all kind of the same.

Now, the ratings in collaborative filtering can be viewed as a weighted
bipartite graph.
But, when getting started, it is always easier to go with the simplest
possible examples, so, the first thing we did is drop the weights, which gives us something like this silly little graph.

![Bipartite graph of user ratings of food items](/figures/foldnot/abby-bipartite.svg "A rating graph of users and foods")

In the graph, there are users, Abby and three others, and five items, which are
the apples, bananas, etc.
A CF algorithm would use these ratings (originally weighted ones, but, increasingly, unweighted) to give Abby some recommendations by operating over
the graph.
Redrawing the graph allows us to see how this might work a little better.

![Graph redrawn to show how Abby connects to other users through common likes](/figures/foldnot/abby-hammock.svg "Abby connects to other users thorugh apples and bananas")

One form of algorithm uses Abby's ratings to find a neighborhood
of similar users for Abby whose ratings could be used to generate
recommendations for her.
Because Abby has rated both apples and bananas, she has common ratings with the
other three users, and recommendations can be viewed as being made over this graph:

![Abby connects to users through shared likes, and can be recommended items that they like](/figures/foldnot/abby-user-hammock.svg "Abby connects to users with similar likes")

But, other algorithms instead find neighborhoods of similar items and recommend
items that are similar to ones that Abby likes:

![Foods Abby likes connected to other foods by likes of other users, and Abby can be recommended items similar to those she likes](/figures/foldnot/abby-item-hammock.svg "Abby likes foods that are similar to others")

To get to these graphs, an algorithm might say that a user had to have
a certain number of ratings; and define a neighborhood based on a
certain number of neighbors and a certain level of similarity.
But, in both cases, we end up collapsing diamond shaped subgraphs (or _hammocks_)
that either link users to users or items to items to edges in a new graph.

![Relating users or items by similarity collapses common ratings into a single edge of a new graph](/figures/foldnot/hammocks.svg "Hammock subgraphs become edges in user or item graphs")

Seeing that most algorithms operated by measuring similarity over these hammocks,
we focusing on the induced graphs and studying their properties ---
we called it ["jumping connections"][mirza].

## Concept graphs and Conjunctions

After moving on from VT, I ended up involved in Bioinformatics projects, and,
in particular, a project with Rich McEachin at U.Michigan where I mined terms
from descriptions of genes and we used them to look at the "jumps"
between blocks of genes for genetically implicated regions of the genome.
Rich dubbed this approach [PDG-ACE][keller].
Because of this project, I found myself working on projects with other researchers and developers at the [NCIBI](http://ncibi.org), a nationally funded center with
the goal of building tools that biomedical scientists could use to understand
disease at a molecular level.

Rich and I really hadn't been looking at the induced graph, but others were.
In particular, before the center started, Dan Rhodes had been using concept
graphs to explore relationships among cancer genes, and his graduate work
eventually led to [Oncomine](http://www.oncomine.org). If we start with a bipartite graph with genes and concept attributes, the concept graph is the graph induced between attributes just like we had done for recommender data. This graph-based approach
became one of the tools in the arsenal of the center.

My role in the center shifted to working with biomedical
scientists to apply center developed tools so that we could drive development.
And, so it was natural that I would end up working with Barbara Mirel,
who studies how people think about and do their work.

Barbara had done a study of users of the center tools.
One of the things she [observed][mirel] was that when making queries
users wanted to be able to use conjunctions to explore the data. For instance, they might want to see genes known to be involved in kidney disease, known to be active in the epithelium, and involved in ion transport.
Nearly every tool that had been built at the center allowed the user
to explore single annotations of genes --- the concept graph allows us
to see when they intersect --- in other words, a conjunction of two "concepts".
I was curious how to use the concept graph for this incremental exploration
that Barbara had described.

So, for my exploration, I took some gene annotation data I had sitting around
and constructed this concept graph. The annotations are from the
[Gene Ontology](http://geneontology.org) (GO), commonly used to annotate genes with
terms from three sub-ontologies: one for the functional role a gene plays,
another for where a gene occurs in a cell, and a third for the processes to
which a gene contributes.

![Concept network for a set of genes based on GO annotations.](/figures/foldnot/conceptnet1.svg)

The colors indicate the kind of annotation: blue is location, green is function,
and purple is process. The vertices in the graph correspond to each annotation,
and the edges indicate the intersection of the sets of genes for the annotations
defining the vertices. For instance, the edge between the vertices for cytoplasm
and signal transduction indicates the genes that have both of those annotations.

What Barbara had said was that users wanted to be able to fold in different
annotations successively, and explore which genes belong together. The concept
graph is clearly emphasizing the wrong thing: the size of a vertex is proportional
to the number of genes with that annotation, but we are really interested in the
edges. So, I tried successively building the graph by combining different types
of annotations --- first as conjunctions of location and functional role:

![Concept graph for conjunction of location and function with process](/figures/foldnot/conceptnet2.svg)

Notice that certain edges become vertices, while the new edges represent common
genes between those new vertices. Now, pulling in the biological process, I got
this graph:

![Concept graph for conjunction of location and function and process](/figures/foldnot/conceptnet3.svg)

Now --- _I_ built this graph, and I have a hard time understanding what it means.
The annotated sets are clear enough, but the edges are really hard to interpret.
If we look hard enough, we can see that there are common annotations in the
pairwise connected conjunctions, but to we have to do some Boolean algebra to figure out what we are looking at. This graph really didn't help me understand the
information any better, and I decided I needed another way.

This is how I got to Formal Concept Analysis.

## Formal Concepts

What Naren and I had created for Jumping Connections was very reasonable in the
context of what we were trying to do, but, even there, we had missed something.
The hammock subgraphs capture the user-user or item-item commonality in terms
ratings: Abby likes foods that Brian likes, or apples are liked by people who
like bananas.
The hammocks virtually _fold_ the graph --- projecting to a graph of only users
or items, and losing the information carried by the other vertices of the
bipartite rating graph.

If we look at the bicliques of the rating graph we get a better
picture of the data --- we consider the closure of the relationship between
users and items.
For instance, the relationship between Abby and Brian:
they both like apples and bananas, but these are also liked by Charles.

![Biclique involving users Abby, Brian and Charles based on shared likes of apples and bananas](/figures/foldnot/abby-brian-charles.svg)

This particular biclique shows us not only that Charles is related to the others
in the same way, but it also explains how apples and bananas are related.

Conjunctions are natural in this setting, because the bicliques represent a set
of users who like all of a set of items.
Or, in the gene annotation situation, a biclique represents genes that all have
(at least) a particular set of annotations.
It might be that other items are also liked by those users, or the genes have
common annotations, but those "extras" may tell us something else useful we
wouldn't have seen otherwise.

In formal concept analysis, these bicliques are called _formal concepts_, and
ordering the concepts by inclusion on user sets --- our biclique with Abby,
Brian and Charles comes before the biclique of Abby, Brian, Charles and David
who all like bananas --- we get what is called the Formal Concept Lattice.
The structure of the lattice captures the subtleties of relationships between
the concepts that can be exploited in different ways.
For collaborative filtering, the lattice allows us to define the space of possible
recommendations for a user based on the inclusion relation, and there is a small
set of lattice structures that are useful in different data mining problems.
(To learn more, see my slides on [Mathematics of Incidence](http://www.slideshare.net/BenjaminKeller/incidencemath-basics0914).)

When we draw the concept lattice for the gene annotation example, we get the following picture.
It looks like a graph, but now each node is a formal concept, and the downward arcs indicate the ordering on concepts.
The concepts at the second level from the top correspond to the individual annotations we saw in the concept graph, and the ones at the second level correspond to the edges of that graph.
As we move down the lattice the concepts have more annotations (longer conjuctions) and fewer genes.
To make things a little clearer, the concepts are labeled at the highest position that an annotation occurs in the lattice --- usually we'd do this for the genes too (labeling the lowest position where they first occur), but there are thousands of genes (and while they form big groups, I'm being lazy). We can figure out which conjunctions the unlabeled elements represent by tracing back to the labeled ones. The bottom concept corresponds to the individual gene (ANK3) that this story centers around.

![The concept lattice for the gene-annotation example shows all conjunctions of annotations](/figures/foldnot/conceptnet-lattice.svg "Concept lattice for gene-annotations")

The concept lattice formalism has no notion of frequency, so as is done for the
concept graph we can draw the size of the nodes for an concept relative to the
number of genes in the concept (gene counts are shown in each node). The colors
correspond to those of the concept graph, with other colors meant to evoke the
combination of different types of annotations by conjunction.

It is a little harder to read the diagram of a concept lattice, but everything in
the concept graph is there, and more.
For instance, the edge of the concept graph that connects cytoskeleton and
cytoplasm is represented by a concept at the next level down, connected to them
by the two subconcept (inclusion) arcs.
Each successive graph that I created includes the concepts at the next level down.
But, while the concept graph for the conjunctions only shows the relationships
among the sets of genes defined by those particular conjunctions, the concept
lattice allows us to explore how different conjunctions relate to one another.

This happens to be a nice compact concept lattice. But, they can be very large.
So, it would be wrong to conclude that these diagrams should be the _de facto_
standard for visualizing incidence data. However, the lattice _does_ make explicit
all of the relationships based on commonality that are in the data, and this is
a problem that occurs over and over again when we deal with data like this.
This means that data explorations can operate over the lattice, allowing us to build
more intuitive visualizations for particular problems
(see, for example, my [Graph Annotation](http://www.slideshare.net/BenjaminKeller/graphannotation0714) slides).

## Please, don't fold your incidence

I come out of the algorithmic tradition of Computer Science where graphs are a
standard model for many problems, so it is natural that I would turn to them as
a representation for a problem that looks like a graph problem. But, the result
is that I've spent a lot of time looking at incidence data in the wrong way.

A concept lattice captures relationships of commonality within a data set in a
way that a concept graph cannot. When we build a jumping connections/concept
graph from incidence data we get hints of higher order relationships --- the
concepts show up as cliques in the graph, but we'd have to work really hard to
go beyond conjunctions of two annotations. And, we have to work even harder get
any hint of different ways that the annotations are related as shown by the
lattice structure.

I can remember bioinformatics projects where we generated a concept graph, and
then used graph analysis tools to find the cliques, and then, for each, had to
back up and figure out what they meant. _Ouch_. But, no more.

So, seriously, don't fold your incidence data. Or, if you must, take a look at
the concept lattice first...

[keller]: http://www.ncbi.nlm.nih.gov/pmc/articles/PMC2646236/ "Keller and McEachin. Identifying hypothetical genetic influences on complex disease phenotypes, BMC Bioinformatics 10(Suppl 2), (2009), S13."
[mirel]: http://www.j-biomed-discovery.com/content/4/1/2 "Mirel. Supporting cognition in systems biology analysis: findings on users' processes and design implications, J. Biomedical Discovery and Collaboration 4, 2 (2009)."
[mirza]: http://link.springer.com/article/10.1023%2FA%3A1021819901281 "Mirza et al., Studying Recommendation Algorithms by Graph Analysis, JIIS 20, 2 (2003) 131-160."
