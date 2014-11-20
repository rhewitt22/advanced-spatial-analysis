---
title: "Elementary Customization of ArcMap"
layout: default

course: "GIS 520: Advanced Geospatial Analytics"
topic: "Customization"
excerpt: "The City of Oleander's GIS department recently had lots of employee turnover with several retiree positions being filled by recent college graduates.  The GIS manager for the department sees this as an opportunity to standardize how business is done, and would like to create some common training tools and manuals for the new employees.  I, the remaining GIS Analyst, volunteered to codify my analysis steps and procedures by customizing the ArcMap interface for all computers in the GIS lab as a first step.  I began by creating two new toolbars: an Oleander toolbar containing Save Edits, Start Editing, Stop Editing, Use Snapping, and Run EasyCalculate10 commands as well as a drop down menu called Select view, which allows the user to easily switch between data and layout views.  The second toolbar is called Fast Edits, which brought together the Save Edits, Edit Tool, Rotate Tool, and Curve Calculator commands.  Finally, I added the `Open Table with Selected Features` command to the feature layer context menu in the Table of Contents."
---

{% include topic-header.html %}

## Problem

The City of Oleander's GIS department recently had lots of employee turnover with several retiree positions being filled by recent college graduates.  The GIS manager for the department sees this as an opportunity to standardize how business is done, and would like to create some common training tools and manuals for the new employees.  I, the remaining GIS Analyst, volunteered to codify my analysis steps and procedures by customizing the ArcMap interface for all computers in the GIS lab as a first step.  I began by creating two new toolbars: an Oleander toolbar containing `Save Edits`, `Start Editing`, `Stop Editing`, `Use Snapping`, and `Run EasyCalculate10` commands as well as a drop down menu called Select view, which allows the user to easily switch between data and layout views.  The second toolbar is called Fast Edits, which brought together the `Save Edits`, `Edit Tool`, `Rotate Tool`, and `Curve Calculator` commands.  Finally, I added the `Open Table with Selected Features` command to the feature layer context menu in the Table of Contents. 

## Analysis Procedures

### Strategies

Customizing the ArcMap interface is relatively easy as they make a customization window available from which you can select any of the built-in ArcMap commands to any menu of your choosing.  Additionally, with some basic knowledge of the Python scripting language, you can write your own GIS tools and append them to the graphical user interface (GUI) to make them easy to find and use.  Beyond adding commands to existing toolbars, the customization window allows you to add commands to new, user generated, toolbars as well as the context menus that show specific commands based on the context in which they were opened.  Finally, ArcMap allows us to save our interface customizations either in a specific Map Document (MXD), or to the user's default map template, which applies to all maps moving forward.  In the event that the interface was edited in a way that reduces a user's efficiency they can always revert back to the defaults settings by deleting their default mxt.  ArcMap, after searching for the user's mxt, will automatically create a new default mxt if it was unable to find the user's version.

### Methods

Customizing the interface entails launching the customize mode window under ArcMaps `Customize` file menu.  Once opened the user can toggle built-in toolbars on or off, create new toolbars, add commands to existing or user-generated toolbars and context menus, as well as save those customizations for future use.

![Customizing the ArcMap UI]({{ site.baseurl }}/img/diagrams/customize-arcmap.png "Customizing the ArcMap UI")

The above image shows the processes necessary to modify the ArcMap User Interface.  The last stage connecting the modified toolbars/menus to the “save” disk is used to illustrate the two different places changes can be saved.
## Discussion

### Difficulties Encountered

For some reason, despite saving my ArcMap customizations to the MXD I noticed that the `Open Table with Selected Features` command that I added to the feature class context menu continued to disappear each time I closed ArcMap.  I included the context menu in my screen shot to show that I was able to add the command.  I'm still not entirely sure why it wasn't present after closing the document and re-opening it.

### Evaluation

Since this assignment didn't require any actual analysis there is not result to consider for accuracy.  I was able to add commands to existing toolbars, and context menus.  I was also able to create my own custom toolbars to which I added several commands.

## Application & Reflection

Customizing the interface of ArcMap allows more advanced GIS users to increase their efficiency by having all the tools they need at their fingertips.  I have begun to write my own GIS script tools in Python that our Fisheries department uses to analyze data they collect throughout the Southeast using a standardized sampling methodology.  Their methodology takes into account effort, standard survey units, and seasonal variability, salinity, and riparian buffers around the stream/river being surveyed.  My scripts take in the standard datasets and run analyses to find species richness, biomass, and proportion of aquatic invasive species both annually and seasonally.  Since I will now be able to customize the ArcMap interface I can create a map document specifically for this project that allows field biologists without extensive GIS knowledge to find only the necessary tools. I can hide much of the other functionality that ArcMap provides as to reduce the amount of complexity the biologists need to navigate in order to analyze their data.

## Study Questions

### List four tools to place on a customized toolbar that would help you become more efficient using ArcMap. What is the objective of this new tool bar?

I have my ArcMap interface customized with tools related to the MXD.  I find that I often need to change the orientation of my maps based on the shape of my input datasets to create a good composition.  To accomplish this I've added the `Page and Print Setup` command from the File category to my standard toolbar.  On a related note, when I change between map orientations rather than manually re-sizing the data frame boundaries I use the `Fit to Margins` command from the Page Layout Category.  I also added `Map Document Properties` command from the File category, which allows me to quickly edit the map's metadata.  I can add many of the options available in the map document properties to my map layout through the Insert -> Dynamic Text option.  Finally, I added the `Start Editing`, `Save Edits`, and `Stop Editing` commands to my Editor toolbar.  This allows me to by-pass the drop-down menu and save a click each time I need to turn on/off editing mode.

### If you had a chance to redesign the ArcMap interface to include different tools available on the standard toolbars. how would you do it? Would you choose to display fewer tools or more of them?

I would absolutely display fewer tools on the default ArcMap interface.  To this day I remember my first GIS course that explored the ArcMap software.  I was so overwhelmed with all of the options available that I was paralyzed. Trying to keep all of the different options that I actually used separate from the hundreds of commands that are present can be very difficult for beginners.  This is, of course, a balancing act as the continuum of expertise between beginner and seasoned pro is wide.  I fear that intermediate users are unaware of the options to customize the interface so leaving a limited number of options by default may prevent some users from taking full advantage of the software.  I think this middle ground leans more heavily on the search feature than customizing individual commands on the GUI.

### Do you think you could streamline the interface for non-GIS professionals and make their job easier? Or would you simply teach others where to find the tools they need? Explain your answer.

Streamlining the interface for non-GIS professionals is a must.  Biologists and the like cannot be expected to have several years of GIS training just to explore data that they collect in the field.  In the same vein they should not have to rely solely on a GIS Analyst to create extraordinarily simple maps for them on a regular basis.  With a solid grasp of the user's needs and how to customize the interface a GIS analyst can set-up a map document to show only the tools necessary to get the job done.  By saving the customizations to the interface we can customize the UI for a number of different use-cases, which can follow the project through to the finish rather than creating new maps each time the user goes into the field.  When ArcGIS introduced the Search function in version 10.0 it became dramatically easier to find tools as needed.  This allows for a sort of middle-ground where the user isn't presented with an overwhelming number of options, but knows exactly where to go if the exact command he/she needs is not immediately available.