---
title: GW4E in a nutshell
tags: [overview]
keywords: overview, model based testing, graphwalker, gw4e, Eclipse plugin, GraphWalker Eclipse Plugin
summary: "GW4E in a nutshell"
sidebar: mydoc_sidebar
permalink: mydoc_nutshell.html
folder: mydoc
---

## Model Based Testing Overview

The Model Based Testing (MBT) is a test practice in the software industry to increase the effectiveness of the tests, both in
their coverage of the requirements and in the productivity for creating and maintaining test repositories.
Model Based Testing improves the test process by piloting the creation and maintenance of tests from modeling for the test.

![MBT](https://raw.githubusercontent.com/gw4e/gw4e.github.io/master/images/mbt.png "MBT")


## Model and tests 

The model describes all or part of the system. From the model are derived the abstract tests that are the basis of 
the executable tests that will test the black box, called system. Abstract tests are like the model, independent of the 
platform used. They are a common interface to the executable tests that will be generated; they represent paths in the use
of the system.

The purpose of the test design in MBT is to describe the expected behavior of the system under test. The result of design looks
like a graph model with a number of edges (aka arrow, arc or transition) and vertices (aka node or state) and how do they interact 
with each other. A model would remind you a popular in testing state transition diagram or a finite state diagram. 
An edge express an action with the SUT and a vertex express a state of the SUT which should be tested. 
When a test is generated from the model, a model derives to a java interface and a class implementation, and each graph element 
(Vertex or Edge) is converted to a java method.
![MBT](https://raw.githubusercontent.com/gw4e/gw4e.github.io/master/images/modeltojava.png "MBT")
 
## Tests Generation Mode

There are two kinds of generation 

__Online__

Online testing means that a model-based testing tool connects directly to an SUT and tests it dynamically.
![MBT](https://raw.githubusercontent.com/gw4e/gw4e.github.io/master/images/mbtonline.png "MBT")

__Offline__

Offline means generating a test sequence once, that can be later run automatically. Or, just generating a sequence to prove that the model
with the path generator(s) together with the stop condition(s) works.
![MBT](https://raw.githubusercontent.com/gw4e/gw4e.github.io/master/images/mbtoffline.png "MBT")
 
## Online Model Navigation

When a test has been generated, it needs to be completed because tests generation ends up with a test skeleton. Once you've completed the test,
you will want to run it. At execution time GraphWalker walks thru the graph model, when it encounters a graph element (node, or vertex), it calls
the test java method having the name of the element. The way GrahpWalker walks thru the graph is determined by a __Generator__. The way it stops walking is 
handled by a __Stop Condition__. Path generators together with stop conditions will decide what strategy to use when generating a path through a model, and when
to stop generating that path. Different generators will generate different test sequences, and they will navigate in different ways.



## Generators

There are many path generators offered by GraphWalker. The following are two examples :

### random(some stop condition(s))
Navigate through the model in a completely random manor. Also called “Drunkard’s walk”, or “Random walk”. This algorithm selects
an out-edge from a vertex by random, and repeats the process in the next vertex.

### weighted_random(some stop condition(s))
Same as the random path generator (see above), but, will use the weight property when generating a path. The weight 
is an edge property, and it represents the probability of an edge getting chosen.

You can find more details [here](http://graphwalker.github.io/generators_and_stop_conditions).

## Stop conditions

There are many stop conditions offered by GraphWalker. The following are two examples :

### edge_coverage( an integer representing percentage of desired edge coverage )
The stop criteria is a percentage number. When, during execution, the percentage of traversed edges is reached, the test
 is stopped. If an edge is traversed more than one time, it still counts as 1, when calculating the percentage coverage.

### vertex_coverage( an integer representing percentage of desired vertex coverage )
The stop criteria is a percentage number. When, during execution, the percentage of traversed states is reached, the 
test is stopped. If vertex is traversed more than one time, it still counts as 1, when calculating the percentage coverage.

You can find more details [here](http://graphwalker.github.io/generators_and_stop_conditions).

## Generator and Stop conditions usage
You have two options when using Generator and Stop Conditions:  

1. You use it in the class '@GraphWalker(...)' annotation
![GraphWalker annotation](https://raw.githubusercontent.com/gw4e/gw4e.github.io/master/images/graphwalkerannotation.png "GraphWalker annotation")  
2. You use them with api in your test
![Generator and Stop condition Apis](https://raw.githubusercontent.com/gw4e/gw4e.github.io/master/images/generatorstopconditionapi.png "Generator and Stop condition Apis")

## Tests Generation 

There is currently 2 kinds of graph model format : __.graphml__ and __.json__, and there are many ways to generate artifacts from a Graph Model.
Here the options :  

| Model Type         | Artifact Generated       | Goal                             |
| ------------------ | :----------------------- | :------------------------------- |
| json/graphml model | "Java Model" Based code. | To learn GraphWalker apis usage. |
| json/graphml model | "Java Test" Based code.  | To generate Test Interface and a default java implementation from the graph. |
| json/graphml model | Dot graph model          | To convert a json file to a .dot file. |
| json/graphml model | "Java Interface Test"    | To generate Test Interface from the graph. You use this option when you already have a test implementation and you have updated your graph model. In that case you would regenerate the interface and make your test implements the newly generated interface so that the test is in sync with the model. |

The graphml options usage are possible ones but are not recommended. If you have 'graphml' formatted files, you would first convert them to 'json' format and then you would work from the 'json' formattted files.
 
Here the different scenarios :  

1. Right click the json graph model file and you choose __GW4E -&gt; Convert to..."__. If you do so, you will have an opportunity to fine tune the generated code with the opened wizard.  
   *  __GraphWalker Class Based Test__ : the generated java class file contains a GraphWalker Annotation  
   *  __GraphWalker Model Based Test__ : the generated java class file contains a method that shows GraphWalker Model Apis usage  
   *  __JUnit Smoke Test__ : the generated java class file contains a test to verify the basic flow of the model  
   *  __JUnit Functional Test__ : the generated java class file contains a test covering the complete graph  
   *  __JUnit Stability Test__ : the generated java class file contains a test that randomly walk the model, until the stop condition is fulfilled  
2. Right click the json graph model file and you choose __GW4E -&gt; Generate Test Interface"__. If you do so, you will regenerate the interface from the latest saved state of the graph model. It is up to you to update the test implementation to implement the newly generated interface.  
3. Right click the __src/main/resources__ folder or __src/test/resources__ folder and you choose __GW4E -&gt; Generate Test and Interface"__. If you do so, you will generate a default test implementation and an interface from the latest saved state of the graph model. If there is an existing test implementation, it will be renamed. You could use the __Eclipse diff/merge__ tools to update the newly generated test. Notice that in that case you don't have the opportunity to fine tune the generated code.

Model files in __src/test/resources__ generate java class in __src/test/java__ while those in __src/main/resources__ generate in __src/main/java__. The same way, a java interface
is generated in the __target/generated-sources__ directory or __generated-test-sources__. This structure complies with the GraphWalker command line tools expectation. This means that you can work without any changes in the two environments (GW4E Eclipse Plugin vs  GraphWalker Command line tools).<br/>

The test interface name derives directly from the graph name. In fact only the extension is changed from ".json" to ".java".
The test implementation name follows the same rule except that a suffix is added to the name. The default suffix is __Impl__ (Can be customized on the project reference).  
  		
## Requirement Coverage
It is essential that the tests you run meet your original requirements. To track of the relationship between your requirements and tests, 
you link them by setting a comma separated list of requirements in a dedicated vertex property of the model. These informations, can be used to create 
traceability with external requirements and the models. The information associated to the requirements are available at the end of the test execution in a JSON format.

![Requirement Coverage](https://raw.githubusercontent.com/gw4e/gw4e.github.io/master/images/requirement.png "Requirement Coverage")

>Notice that the requirement_coverage can be used as a Stop Condition:<br/>
>__requirement_coverage( an integer representing percentage of desired requirement coverage )__  
>The stop criteria is a percentage number. When, during execution, the percentage of traversed requirements is reached, the test is stopped. If requirement is traversed more than one time, it still counts as 1, when calculating the percentage coverage.

 		
## Launching Tests within Eclipse
You have two options when it comes to run you tests:  

1. You want to use the class '@GraphWalker(...)' annotation, in that case you use the Graphwalker Maven plugin. Use one of the following shell commands  
  *  __Right-click__ the java test source file in the __Package Explorer__ and select __"Run As -> GW4E Test"__ menu item
2. You use GraphWalker api to set the PATHGENERATOR/STOPCONDITION in your test, in that case you use the Surefire Maven plugin. Use one of the following shell commands  
  *  __Right-click__ the java test source file in the __Package Explorer__ and select __"Run As -> JUnit Test"__ menu item

## Launching Tests in your CI or at Shell Command  
You have two options when it comes to run you tests:  

1. You want to use the class '@GraphWalker(...)' annotation, in that case you use the Graphwalker Maven plugin. Use one of the following shell commands  
  *  define the plugin in your pom.xml file and bind the graphwalker test goal to the test phase  
  *  use a fully qualified name like 'mvn org.graphwalker:graphwalker-maven-plugin:test'  
  *  add org.graphwalker as a pluginGroup in your settings.xml file (See maven documentation)  
2. You use GraphWalker api to set the PATHGENERATOR/STOPCONDITION in your test, in that case you use the Surefire Maven plugin.   
  *  define the Surefire plugin in your pom.xml file and bind the graphwalker test goal to the test phase

