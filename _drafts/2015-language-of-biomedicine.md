---
layout: post
title: "Defining the map of medicine"
date: 2017-08-25
---

In the last few months, I've taken my kids into the doctor for their annual physicals, and I've been watching what goes on – what the nurse does, what the doctor does, and the conversations that occur. I see really obvious things: the nurse manually typing in the results from my daughter's hearing test, and a UI that was new when my hair was blonde. But, the subtle thing is that when the doctor walks in, they have no context – they say hello and sit down and read. I have friends whose doctors will never forget their histories, but who can forget a story about hacking up blood. So, it is probably a good sign when we aren't terribly memorable, but these visits have started me thinking about how we get better at watching our own health.

To get started, please indulge me in a bit of morbidity: *life is a trip toward death*. Our goal should be to not get there too soon, and to not suffer through ill health on our way there.

In late spring, I took my teenage son to the doctor for his annual physical.
Watching the doctor do his thing, I started to think about similar my son's visits are to mine, even though we are decades apart in age. Sure there are some differences – the doctor checks him for conditions that arise in those who are still growing – but the choreography of the visit is very similar.

What our doctor is doing when we visit him is try to figure out what is going on with us, spot possible concerns, nudge us in the direction of healthy behaviors.
But the fact is that a visit is choreographed by a list of standard gender/age/risk-specific examinations and questions, and very little that happens is specific to me or my son. In my visits, palpating my abdomen and listening to my heart are about as concrete as we get. The rest is generality based on the broad population, only some of whom have a comparable genetic makeup, but even fewer that have had the same environmental exposures. Even the answers I get when I have specific concerns are very general – often boiling down to being a *man-of-a-certain-age*.

With all the noise around precision medicine, the question is how we get these interactions to be more precise – so that I walk out of a visit thinking the doctor was talking about me and not some generic version of a middle-aged male who, it seems to me, parties a lot harder than I do.

## Of maps and our health

In some sense, we can think of health and wellness in the same way we think of a geographic map. We can use a map to figure out where we are, and, once we know our location, to plan how we can get to somewhere else. When we visit the doctor, the goal is basically that: the doctor determines our location on the map, and point us in the direction we need to go.

In reality, it is a bit like this. Say, I want to walk to New York City, so I visit the geographer – the Map Reader. The Map Reader has this map:

![Cartoon map of the United States](/figures/medmp/cartoon-us.svg)
{: style="text-align: center"}

The map is divided into six regions, each with a location that represents our most likely position if we were in the region.  Using the map, it is possible to tell roughly where I am, where I want to go, and a direction to get here. In my case, the Map Reader determines I'm in the western region, and knows that New York City is in the northeastern region. So, to get to New York City, the Map Reader says I need to head northeast.

This is not a whole lot different than my visit to the doctor with all the generality. I know I'm near Seattle, not really close to that dot on the map. Since I'm actually **north** of NYC, the trajectory that the cartoon map takes me would end somewhere in Canada. Probably, I would end up in northern Ontario staring out at the Hudson Bay wondering why I couldn't see the Statue of Liberty.

Fortunately, in medicine, the equivalent of ending up in northern Ontario is often close enough. If my doctor finds prostate cancer, I will pay attention, and will probably be happy if the oncology team gets me to a state where the cancer is simply not progressing, and I may not worry about being cured.
But, in general, if I walk out of the doctor's office feeling the same way I would walk away from the Map Reader – either knowing or having a feeling that I'm nowhere near that dot on the map, that the directions don't make sense – what happens?  

Of course, my story with the cartoon map is kind of ridiculous, because my phone has a GPS and *two* mapping apps. While the GPS can be a little flakey – right now, it says I'm in my neighbor's house – it is really close. So, I know where I am within a reasonable tolerance, and I can get very detailed walking directions from Google Maps that include a ferry across Lake Michigan and a transit across southern Ontario all in a mere 37 days and 9 hours non-stop. That is still ridiculous, but the point is that I have a map that *I* can read, and I have tools that allow me to figure out where I am and where I'm going. We shouldn't expect health care to be the same as navigating the world, but we should aim for something analogous.

## Scientific wellness as a start

A hint of where we might want to go can be seen in the idea of scientific wellness that has come
out of the [Institute for Systems Biology](http://www.systemsbiology.org).
The
[Wellness Project](http://research.systemsbiology.net/100k/)
led by Nathan Price and Lee Hood is focused on understanding what it means to be
and stay well, and has been spun out into the company [Arivale](https://www.arivale.com).
Participants in the project have data collected at regular intervals so that their
condition can be monitored. When the data shows they are skewing "unhealthy",
personalized interventions can be applied to move them back toward their normal.

The goal is that instead of walking into the doctor when something feels wrong, or
waiting until our next regular "well visit" to mention that something feels wrong,
our care would involve active monitoring of our "wellness" and interventions would
be triggered, hopefully, before complications have the chance to arise.
Success would be a change from medicine centered on treating illness to medicine
instead centered on maintaining wellness through things like changes in diet and
more aggressive interventions when needed. This opportunity comes from the ability
to collect data, and learn what it means to be well – to define the language of wellness.

## Getting to a wellness map

The key to our geographical maps is the math that allows surveys to be translated into projections onto the page.

Getting to this refined map is going to mean

Central to our ability to analyze and understand complex data is powerful
mathematics. Usually, this means the math that underlies statistics and/or Machine
Learning, but I'm thinking of other mathematics –
other *old math used in new ways*.

In particular, the math behind Ayasdi's technology, Topological Data Analysis
(TDA), is quintessential *old math used in new ways*.
TDA takes data and looks it in just the right way so that techniques from
topological homology can be applied to recognize relationships within the data
that define its *shape*.

The shapes include linear structures (lines/planes/hyperplanes), clusters,
circles, and flares.
As [Allison Gilmore](http://www.ayasdi.com/blog/bigdata/the-shape-of-the-future-building-predictive-models-using-machine-intelligence/)
of Ayasdi describes, the shapes of data are used as assumptions in standard analysis where
we try to build linear models, clusters and maybe even flares (in the form of
decision trees). But, TDA, instead of assuming a shape, finds all shapes as they
occur in subsets of the data.

The idea that our data can be described as combinations of these shapes gives us
a different way to think about that data and what it represents.


As a new language for data, the shapes of TDA can give us a different way to think
about wellness. Imagine a map of the population


And, rather than math being a
["new science of medicine"](http://www.kevinmd.com/blog/2015/05/mathematics-is-the-new-science-of-medicine.html),
I'm talking about *old math used in new ways* to change how we talk about data.



I recently had one of those *aha* moments that usually makes people scratch their
heads and give me funny looks. It came through the convergence of a Lee Hood talk
on wellness, a
[presentation](http://www.ayasdi.com/blog/bigdata/the-shape-of-the-future-building-predictive-models-using-machine-intelligence/)
by [Ayasdi](http://ayasdi.com) data scientist Allison Gilmore, and a
[blog post](http://www.kevinmd.com/blog/2015/05/mathematics-is-the-new-science-of-medicine.html)
on the increasing role of mathematics in medicine.
