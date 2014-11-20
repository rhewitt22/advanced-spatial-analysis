---
title: "AutoCAD Integration"
layout: default

topic: "Geospatial Data Issues"
thumbnail: autocad

excerpt: "The NC State administration has asked that the GIS Department take over the management of the facilities inventory supporting campus planning. To this point the Campus Masterplan has been managed through Computer Aided Design (CAD) software.  I have been tasked with transitioning the data from AutoCAD to an ESRI Geodatabase."
---

{% include topic-header.html %}

## Problem:

The NC State administration has asked that the GIS Department take over the management of the facilities inventory supporting campus planning. To this point the Campus Masterplan has been managed through Computer Aided Design (CAD) software.  I have been tasked with transitioning the data from AutoCAD to an ESRI Geodatabase.

## Analysis Procedures:

### Strategies:

In order to complete this assignment I'll need to georeference the files from the CAD department to the North Carolina State Plane projection. I will then convert the files into their GIS equivalent features.  ArcGIS provides a series of tools for both georeferencing and file conversion that support input CAD datasets.

### Methods:

I will be using ArcGIS to convert the Campus Masterplan datasets from CAD files into a spatial database.  Since the initial CAD files do not contain any spatial reference my first task is to georeference the files using an orthophotograph. ArcGIS's georeferencing toolbar allows the user to create control points that are used to create a [World file](http://en.wikipedia.org/wiki/World_file). The World file is used to transform vector or raster data between two coordinate systems.

![Georeferencing Diagram]({{ site.baseurl }}/img/diagrams/georeferencing-diagram.png "Georeferencing Diagram")

Once the CAD files are georeferenced I can begin to convert them to an ESRI geodatabase.  As with most GIS problems there is more than one way to accomplish this task.  ESRI actually provides a CAD to geodatabase geoprocessing tool.  This converts each of the parts of a CAD `.dwg` file into a corresponding feature class in the output geodatabase.  One of the nicest parts of this geoprocessing tool is that it does not convert any pieces of the CAD file that are empty.  For example, there is an annotation file in the `.dwg` that is completely empty.  After running the CAD to Geodatabase tool this particular piece was excluded.

AutoCAD files are notorious for having open polygons.  When these files are converted to an ESRI format since they do not fully close they are represented as line features.  In order to create a complete inventory of campus facilities we need to combine the line and polygons representing similar physical features.  Typically features in a GIS are represented as points, lines, or polygons based on how they will be used.  Lines are used for features that will be used only to measure distance.  Polygons are used when you may need to measure area or perimeter.  As such, buildings, athletic fields, and water features will be represented as polygons.  Roads and sidewalks will be represented as lines.

![Conversion Diagram]({{ site.baseurl }}/img/diagrams/conversion-diagram.png "Conversion Diagram")

## Discussion:

### Difficulties Encountered:

The latest enterprise software update that was installed for all of my agencies users corrupted ArcMap's ability to write data to geodatabases.  It took me quite a while to understand the cryptic errors, which only mentioned a location on disk rather than what the actual problem was.  I downloaded a [patch](http://support.microsoft.com/kb/2732673) to Microsoft Windows 7, which fixed the problem.

I'm not entirely sure why georeferencing CAD files only allows two control points.  In the past when I've used the georeferencing tool I was able to select a number of different control points which contribute to the overall accuracy of the output by allowing me to spread control points throughout the full extent of the project.

Finally, features are represented differently in CAD and GIS applications.  With CAD files the features are designed to look as close to exact to the features they represent as possible.  In GIS we often use more simple representations in order to make analysis more straight forward.  One such example is how roads are drawn in both of these software packages.  In GIS roads are generally represented as a single line corresponding to the center of the road.  This allows us to easily measure distance along any segment of that line.  In the AutoCAD files we were given roads are represented as polylines corresponding to the outer edge of each side of the road.  In a GIS analysis this added complexity makes simple analysis more difficult because they are approximately two times the total length.

### Evaluation:

![Georeferenced Map]({{ site.baseurl }}/img/full-size/georeference.png "Georeferenced Map")

I'm very confident in the results of my data conversion.  I compared the final datasets against both the orthophotograph provided by NC State, and an imagery layer provided by ESRI.  In both cases the margin of error was very small and could be contributed to the low number of control points used to georeference the initial dataset.  Because I used the `Select by Attributes` tool on each of the pertinent layers I am confident that my final output for each feature class contains all features -- even those that were represented as polylines in the initial dataset due to digitization errors. 

## Application & Reflection:

Georeferencing is a very common and useful application of GIS.  In the past I have georeferenced Engineering drawings (rasters) when the CAD files themselves are not available.  In this case we have the features in a GIS already, but we use the official engineering drawings to ensure their accuracy.  Another case where I applied my georeferencing skills to a raster dataset was on an aquatic invasive species removal effort.  Field staff were on the water almost every day in search of nutria, a semi-aquatic rodent that has ravaged marsh throughout the Chesapeake Bay.  There were high resolution navigation charts available on the web as simple `.png` images.  The files themselves were not associated with a coordinate system, but they contained very valuable information such as submerged hazards, and shallow areas.  I georeferenced these images and trained the staff on how to make simple field maps that could help them navigate for their surveys.