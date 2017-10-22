---
title: Overview of GW4
tags: [overview]
keywords: overview, model based testing, graphwalker, gw4e, Eclipse plugin, GraphWalker Eclipse Plugin
summary: "Overview of GW4E"
sidebar: mydoc_sidebar
permalink: mydoc_nutshell.html
folder: mydoc
---

## Model Based Testing Overview

The Model Based Testing (MBT) is a test practice in the software industry to increase the effectiveness of the tests, both in
their coverage of the requirements and in the productivity for creating and maintaining test repositories.
Model Based Testing improves the test process by piloting the creation and maintenance of tests from modeling for the test.

![MBT](https://github.com/gw4e/gw4e.samples/blob/master/images/mbt.png "MBT")

The model describes all or part of the system. From the model are derived the abstract tests that are the basis of 
the executable tests that will test the black box, called system. Abstract tests are like the model, independent of the 
platform used. They are a common interface to the executable tests that will be generated; they represent a path in the use
of the system.

## GraphWalker & GW4E Overview

The purpose of the test design in MBT is to describe the expected behavior of the system under test. The result of design looks
like a graph model with a number of edges (aka arrow, arc or transition) and vertices (aka node or state) and how do they interact 
with each other. A model would remind you a popular in testing state transition diagram or a finite state diagram. 
An edge express an action with the SUT and a vertex express a state of the SUT which should be tested. 
When a test is generated from the model, a model derives to a java interface and a class implementation, and each graph element 
(Vertex or Edge) is converted to a java method.

![MBT](https://github.com/gw4e/gw4e.samples/blob/master/images/modeltojava.png "MBT")

When a test has been generated, it needs to be completed because generation ends up with a test skeleton. Once you've completed the test,
you will want to run it. At execution time GraphWalker walks thru the graph model, when it encounters a graph element (node, or vertex), it calls
the test java method having the name of the element. The way GrahpWalker walks thru the graph is determined by a PATHGENERATOR. The way it stops walking is 
handled by a STOPCONDITION. Path generators together with stop conditions will decide what strategy to use when generating a path through a model, and when
to stop generating that path. Different generators will generate different test sequences, and they will navigate in different ways.

#### Generators
There are many path generators offered by GraphWalker. The following are two examples :
##### random( some stop condition(s) )
Navigate through the model in a completely random manor. Also called “Drunkard’s walk”, or “Random walk”. This algorithm selects
an out-edge from a vertex by random, and repeats the process in the next vertex.
##### weighted_random( some stop condition(s) )
Same as the random path generator (see above), but, will use the weight property when generating a path. The weight 
is an edge property, and it represents the probability of an edge getting chosen.

#### Stop conditions
There are many stop conditions offered by GraphWalker. The following are two examples :
##### edge_coverage( an integer representing percentage of desired edge coverage )
The stop criteria is a percentage number. When, during execution, the percentage of traversed edges is reached, the test
 is stopped. If an edge is traversed more than one time, it still counts as 1, when calculating the percentage coverage.
##### vertex_coverage( an integer representing percentage of desired vertex coverage )
The stop criteria is a percentage number. When, during execution, the percentage of traversed states is reached, the 
test is stopped. If vertex is traversed more than one time, it still counts as 1, when calculating the percentage coverage.


#### Generator and Stop conditions usage
You have two options when using Generator and Stop Conditions.
1. You use it in the class '@GraphWalker(...)' annotation
![GraphWalker annotation](https://github.com/gw4e/gw4e.samples/blob/master/images/graphwalkerannotation.png "GraphWalker annotation")
2. You use them with api in your test
![Generator and Stop condition Apis](https://github.com/gw4e/gw4e.samples/blob/master/images/generatorstopconditionapi.png "Generator and Stop condition Apis")

 