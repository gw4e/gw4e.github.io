---
title: Installing GW4E on top of Eclipse
tags: [getting_started,installation]
keywords: getting_started,installation,model based testing, graphwalker, Eclipse plugin, GraphWalker Eclipse Plugin
summary: "Installing GW4E on top of Eclipse"
sidebar: mydoc_sidebar
permalink: mydoc_install_gw4e_on_top_of_eclipse.html
folder: mydoc
---

## Prerequisites

 * [Install Maven](https://maven.apache.org/install.html), if not already installed 
 * Install GraphWalker in your local maven repository, if not already installed 
   * Download the [GraphWalker client library](http://graphwalker.github.io/content/archive/graphwalker-cli-4.0.0-SNAPSHOT.jar) in a directory
   * Run in a shell, the following command :
     * <b>mvn install:install-file -Dfile=YOUR_DOWNLOAD_LOCATION/graphwalker-cli-4.0.0-SNAPSHOT.jar -DgroupId=org.graphwalker -DartifactId=graphwalker-cli -Dversion=4.0.0-SNAPSHOT</b> 


## Installation
 * Make sure you've followed the prerequisites
 * Use one of the 2 following options to install GW4E
   * [Option 1](#option1) - Installing GW4E with the Eclipse MarketPlace Option (IN PROGRESS)
   * [Option 2](#option2) - Installing GW4E with the Standard Option 




### <a name="option1">Option 1</a> - Installing GW4E with the Eclipse MarketPlace Option (IN PROGRESS)

Drag the **Install** button to your running **Eclipse workspace** and follow the wizard.

[![Drag to your running Eclipse workspace.](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=3480626 "Drag to your running Eclipse* workspace.")

### <a name="option2">Option 2</a>  - Installing GW4E with the Standard Option 

 1. Launch **Eclipse IDE for Java EE Developers** , if not already running
 2. In the main menu, click on the **Help -> "Install New Software..."**,
 3. Click the **Add** button
 4. Enter **GW4E** in the **Name** field
 5. Enter **https://github.com/gw4e/gw4e.project/raw/p2repo-4.0.0/repository** in the **Location** field
 6. Check the **GraphWalker Integration for Eclipse** check box
 7. Click **Next**  (processing might take a while)
 8. Click **Next** , select **GraphWalker Integration for Eclipse** and read the details
 9. Follow the wizard until you get GW4E installed.
 
 
 
 
 
 

 