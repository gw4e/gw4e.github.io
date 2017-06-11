---
title: How to contribute to GW4E
tags: [build,installation]
keywords: how to, build, graphwalker, Eclipse plugin, GraphWalker Eclipse Plugin
summary: "How to build GW4E"
sidebar: mydoc_sidebar
permalink: mydoc_contributing.html
folder: mydoc
---

## Introduction
You will contribute with Git tooling.

## Pre-install requirements
 * Install Java JDK 8
 * Install [Maven](http://maven.apache.org/download.cgi)
 * Git
 * Eclipse Neon IDE for Java EE Developers
 
## Get the source code

Get the latest source code from GitHub:

```sh
git clone https://github.com/gw4e/gw4e.project.git gw4e-project
```

## Build the GW4E Update site
```sh
cd gw4e-project
mvn clean install 
```
The location of the update site file is:<br/>
YOUR_M2_REPO_LOCATION/repository/org/gw4e/tycho/org.gw4e.tycho.update/4.0.0-SNAPSHOT/org.gw4e.tycho.update-4.0.0-SNAPSHOT.zip


## Loading the GW4E Eclipse projects in Eclipse IDE 
In order to have all libraries in your environment, execute first the above step **Build the GW4E Update site**

1. Launch Eclipse Neon
2. File -> Import
3. General -> Existing Project into Workspace
4. Click Next button
5. Click Browse... button
6. Select the folder **gw4e-project** (created when you cloned the git repository)
7. Click Finish
