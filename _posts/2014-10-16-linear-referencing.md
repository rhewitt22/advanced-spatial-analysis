---
title: "Linear Referencing"
layout: default

topic: "Geospatial Analytics with Vector Data"
thumbnail: linear-referencing

excerpt: "This assignment covers the use of GIS to apply attributes to specific segments of a line with a technique called Linear Referencing.  More specifically I analyzed the occurrence of accidents along segments of a road network and compared those accidents against both the type of material of the road, and the road's condition."
---

{% include topic-header.html %}

## Problem

This assignment covers the use of GIS to apply attributes to specific segments of a line with a technique called Linear Referencing.  More specifically I analyzed the occurrence of accidents along segments of a road network and compared those accidents against both the type of material of the road, and the road's condition.

## Analysis Procedures

### Strategies

To solve the problem I used the Linear Referencing tools available in ArcGIS to assign the attributes listed below to specific locations along the road network.  The input datasets required were (1) a road network (line features), (2) a table of attributes representing specific location of traffic accidents along the road network, (3) a table of attributes representing specific segments of the road network representing the type of material that makes up the road.

### Methods

Connecting attribute data to segments of the road network was easy as most of the leg-work was already done for us.  The attribute data already contained the necessary location along the network information required to connect the two datasets.  As a result I was able to take the plain `accidents` table and create an event layer (a temporary in-memory feature class) from it which linearly referenced accidents to the road network.  I could then use built-in tools to query all accidents along a particular route of the network.  I repeated the same method using the `pavement` to create a line event layer representing the different materials used to pave road segments.  This new layer contained a score representing the condition of the road between 0 and 100.  Part of the exercise was to analyze whether a poor road condition led to an increased rate of accidents.  I found that there was an insignificant difference (0.1) in the number of accidents per mile for roads with a score less than or equal to 75 as opposed to better maintained roads with a score greater than 75.

![Linear Referencing Datasets]({{ site.baseurl }}/img/diagrams/linear-referencing-diagram.png "Linear Referencing Datasets")

The diagram above shows the steps used to complete this exercise.  Input datasets are in blue, processing steps are in light red, intermediate datasets are in green, and exercise outputs are in dark red.

## Discussion

### Difficulties

Describe any difficulties encountered and briefly explain how the difficulties were resolved.  For example, you may indicate where you had a roadblock in the exercise, i.e., downloading data, finding data, getting model builder past a particular point, editing a field in the attribute table, etc.  Even if you did not have any major problems you should report the difficulties encountered.

### Evaluation

My results showed that poorly maintained roads (score less than or equal to 75/100) had only 0.1 more accidents per mile than those with a score of 76/100 or greater.  I'm not particularly surprised by these results as there are many factors that contribute to traffic accidents.  I would guess that road maintenance has a higher impact on the number of accidents per mile as the score drops more dramatically towards the 50/100 range.

Evidence suggests that distracted and intoxicated driving are some of the most dangerous variables contributing to accidents on the road.  Both of these variables are unrelated to road condition.  I would also assume that roads with high speed limits and a large density of on-ramps and off-ramps would also account for more accidents per mile.

## Application & Reflection

Linear referencing is a powerful tool anytime you are dealing with attributes along a line feature.  In the Fish &amp; Wildlife Service we often look at river and tributary segments that block migration of diadromous fish.  While some dams offer a means for fish to migrate upstream to their typical spawning grounds many do not.  Not only do some dams contribute directly to fish mortality as they try to swim through energy producing turbines, but they also contribute indirectly as adults of reproductive age are unable to find suitable spawning grounds.

With linear referencing in GIS we can assign attributes such as fish species presence/absence to particular reaches of rivers and streams.  The nodes separating these dynamic segments are typically some sort of stream/river blockage that can be addressed through restoration work.  This could include dam removals or fish passage projects.  With linear referencing and dynamic segmentation we can model the blockages that would offer the greatest return on investment by opening up the greatest area for diadromous fishes.