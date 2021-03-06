---
title: "Geocoding Tabular Data"
layout: default

topic: "Geospatial Data Issues"
thumbnail: geocoding-results-final

excerpt: "A local business has chosen me to conduct a geographic analysis of their customer base near Raleigh, North Carolina.  The goal of the analysis is to assist the business in targeting an advertising campaign to expand their customer base in Wake County, North Carolina.  The business collects customer address information, but is unsure how to visualize their customer base on a map.  My job is to convert their database of customers into a geographic dataset that can be used to conduct further spatial analysis."
---

{% include topic-header.html %}

## Problem:

A local business has chosen me to conduct a geographic analysis of their customer base near Raleigh, North Carolina.  The goal of the analysis is to assist the business in targeting an advertising campaign to expand their customer base in Wake County, North Carolina.  The business collects customer address information, but is unsure how to visualize their customer base on a map.  My job is to convert their database of customers into a geographic dataset that can be used to conduct further spatial analysis.

## Analysis Procedures:

### Strategies:

The solution to this problem is not new, and is one of the main business applications of Geographic Information Systems.  The process of Geocoding and Reverse Geocoding involve the conversion of natural language representations of a location (or table of locations) into a geographic dataset, and visa-versa.  ArcGIS has geocoding tools and services built-in that allow us to batch convert addresses to a point shapefile or feature class.  The process requires an input dataset of addresses as well as a reference layer (generally a road network) that are passed through an address locator.  The output is a shapefile or feature class of geographic points.  Geocoding is rarely a perfect process; as a result GIS users generally need to look at unmatched records to correct errors manually.

### Methods:

There are three main components to any geocoding workflow.  First we need reference data that describes our area of interest.  Reference data can come in many forms – points, lines, polygons representing buildings, streets, and other natural features – but in the end reference data always describes the geographic makeup of our area of interest.  Second we need a table of features that we would like to geocode. This table is usually a list of natural language locations (addresses), but can also include fields that contain geographic coordinates stored as text (as opposed to geometry).  Finally we need an address locator.  An address locator takes as inputs both our reference data and the data that we’re geocoding, which is generally a table of addresses.  The result of the entire geocoding process is a set of geographic features that can be visualized/analyzed in a GIS.  Fixing errors in the geocoding process generally requires a manual approach.  The interactive matching tool allows users to fix typos in the input dataset.  After fixing errors you can re-run the geocoding process in order to get an updated output.  The geocoding process is also capable of creating points at specific address locations and adding labels to the map as graphics.

![Geocoding Diagram]({{ site.baseurl }}/img/diagrams/geocoding-diagram.png "Geocoding Diagram")

The above diagram shows the basic process of geocoding tabular data.  Tabular address data and reference data (such as a road network) are fed into the address locator, which produces a feature class of points representing each row in the address input table.

![ArcMap Interactive Rematch Window]({{ site.baseurl }}/img/full-size/interactive-rematch.png "Image showing ArcMap Interactive Rematch Window")

This image shows the ArcMap interface for interactively rematching geocoding results.  This is an important tool for fixing errors made by the address locator, or typos in the input dataset.

## Discussion:

### Difficulties Encountered:

First and foremost, the software produced unexpected results on several occasions.  The find tool that uses the Address Locator continually returned no results for one of the addresses we were instructed to search for.  This is not a new phenomenon with a software package of this size, and simply restarting the program seemed to fix the issues.
The main difficulty I encountered had to do with the data from Wake County, NC.  For several addresses the Address Locator indicated that the geographic location for a given point fell within two zip codes.  I am under the impression that zip codes have a strict topological relationship where the boundary between two zip codes must coincide.  This would suggest that it is impossible for a point to occupy multiple zip codes, however, upon further inspection several of the zip code polygons did in fact overlap.

Beyond the scope of this simple example I can imagine that maintaining a reference layer of either street or building addresses could become very difficult.  In such cases we can rely on third-party address locators/reference data so we can focus on solving the problems at hand rather than constantly updating an address layer as a city grows. 

### Evaluation:

The accuracy of our results is limited to the quality of the data inputs.  In our case the zip codes layer had topological errors that were perpetuated through the analysis leading to many “tied” results.  This is a problem that can easily be solved by enforcing topological rules on our dataset.

In the case of an address table provided by a client we are at the mercy of the client and their customers.  Tabular data in general can often suffer from typos, which result in unmatched or mis-matched geocoding results.  Additionally, some customers may intentionally obfuscate their location as a means to maintain privacy.  For example, a customer buying something simple like a candy bar could be turned off by the fact the business wants to know their personal information.  In such cases it is not uncommon for the customer to provide incorrect information as a means of maintaining their privacy.

## Application & Reflection:

Geocoding is an immensely powerful tool for converting natural language locations into geographic data.  While people generally understand coordinates refer to a specific location they are much more difficult to understand without the help of GIS software.  Addresses on the other hand can be understood by just about anyone; in many cases we geocode these locations manually with a map without realizing it.

An example of how geocoding can be applied to real-world problems is through a web mapping application.  Rarely do we know the exact coordinates of a given location.  To find a place on a map without continually panning and zooming we can enter the name of a place, or even an exact address.  In both cases the web map can geocode real-world places, convert them to geographic coordinates, and zoom to that location so the user can quickly carry on to find their required information.

### Problem description

A local government seeking to improve transparency wants to release crime data from the local police force.  They want to make data available to the public so they can explore and analyze it.

### Data needed

The city would need to release a point feature class of crimes that included attributes including the date/time the crime was committed, the type of crime, and information related to the police force investigation.

### Analysis procedures

If I were to want to make data available to the public in addition to releasing a complete dataset in an open format like a comma separated value I would create a "clip-and-ship" web application.  The application would include two input fields for the user: (1) an address text-box, which I would geocode to create a central point to select crime points, (2) a buffer distance (number) indicating the number of miles the address location should be buffered to clip crime location points.  This application would take the onus off of the police department to provide custom crime reports to citizens who would now be able to find crimes around their homes, or some other area of interest quickly and easily.

![ArcMap Interactive Rematch Window]({{ site.baseurl }}/img/full-size/geocoding-part-one.png "Image showing ArcMap Interactive Rematch Window")

This map shows the initial feature class of points created by geocoding the input address table.  The first attempt at geocoding this dataset resulted in only 53% of addresses being `Matched` by the address locator.

![ArcMap Interactive Rematch Window]({{ site.baseurl }}/img/full-size/geocoding-part-two.png "Image showing ArcMap Interactive Rematch Window")

This map shows the second attempt at geocoding our input dataset.  This time we interactively corrected many of the errors present in the dataset so they could be properly matched by the locator.  In this case the number of `Tied` matches dropped drastically from 32% to 4% which increased our `Matched` results from 53% to 78%.