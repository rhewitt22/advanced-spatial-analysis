---
title: "Suitability Analysis and Weighted Overlay"
layout: default

topic: "Geospatial Analytics with Raster Data"
thumbnail: black-bear

excerpt: "A recent trend in park visitors across the U.S. attempting to take Bear Selfies has led to increased interaction between bears and humans.  Despite warnings park visitors continue to try to approach bears to post photos to instagram and other photo sharing services.  Capturing and re-locating bears has proven to be unsuccessful as the bears continue to return.  Based on several factors we will need to identify the safest areas for bears to reduce the amount of bear-human interaction."
---

{% include topic-header.html %}

## Problem

A recent trend in park visitors across the U.S. attempting to take [Bear Selfies](http://www.npr.org/2014/10/31/360300892/selfies-with-bears-prompt-warning-from-park-rangers) has led to increased interaction between bears and humans.  Despite warnings park visitors continue to try to approach bears to post photos to instagram and other photo sharing services.  Capturing and re-locating bears has proven to be unsuccessful as the bears continue to return.  Based on several factors we will need to identify the safest areas for bears to reduce the amount of bear-human interaction.

For more, listen to the NPR story here:  

<audio controls>
  <source src="{{ '/assets/bear-selfies.mp3' | prepend: site.baseurl }}" type="audio/mpeg"> post.url 
  Your browser does not support html5 audio.
</audio>
<br>

## Analysis Procedures

### Strategies

We will be using the ArcGIS Spatial Analyst extension to model the best available bear habitat in the park to minimize human-bear interaction.  We will use both raster and vector data inputs to create a bear suitability surface with a weighted overlay analysis.  Our vector data inputs include line features representing streams, roads, and trails.  Our raster input datasets include an elevation surface and a vegetation raster that describes the vegetation type of a given cell.  The vegetation raster best represents habitat conditions for black bear.

### Methods

To conduct this analysis I need to convert all datasets to raster.  I used the feature to raster geoprocessing tool to accomplish this.  The next step was to convert the elevation surface to a slope surface using the slop geoprocessing tool.  I then had to use the euclidean distance tool to derive a distance measure (raster) from the input vector datasets. Once I had all of my datasets in the correct form (raster), representing the correct features I could reassign their values to a consistent scale.  Our model uses a scale of one to three with one being the least optimal and three being the most optimal.  I used the reclassify tool paired with the research I was given on black bear suitability to convert all rasters to a common scale.  I then fed the reclassified rasters into the weighted overlay tool where I gave each input the same (20%) weight to produce my final result.

![Bear Model]({{ site.baseurl }}/img/diagrams/bear-model.png "Bear Model")
  
## Discussion

### Difficulties Encountered

During the reclassification step I encountered a problem where a number fell outside the range that I dictated for my new one to three scale.  In the tool I included the large number in my range, but the output didn't take it into account.  I went back into the tool using the results window, which auto-populates the tool as it was run previously.  I then changed the value to the highest value +1 re-ran the tool and everything came together nicely.

### Evaluation

I checked the output of each step of my analysis to ensure the results I got were what I expected.  Anything that was incorrect at an early stage would follow through to the end of the analysis and it would be difficult to know exactly where the error occurred.  Based on checking each individual step along the way and the final output, I am confident in my results that show a majority of pixel values with a score of two or three.

## Application & Reflection

This project focused no strictly on species habitat needs, but also took into account the need to keep bears and humans separate as much as possible.  In my own work we generally work in areas that are less frequently used by humans which is the case of State and National parks.  As such our analysis generally focuses on habitat specific factors.  I could use a similar weighted overlay approach to model the habitat of a rare species using more detailed habitat descriptors like soil type, and canopy cover in addition to the features used in the black bear analysis.  This type of model would be helpful in two scenarios: (1) we have dollars that we can use to directly improve habitat to move it from one favorability class to a higher class, (2) target surveys in areas of high favorability that have no reports of the species.  If we can show that a species is more widespread than previously thought it would prevent the risk of extinction if a meta population were lost in a stochastic event.

## Model Parameters and Results

### Road Reclassification

![Road Reclassification]({{ site.baseurl }}/img/full-size/road-reclass.png "Road Reclassification")<br>
This reclassify tool shows that an increasing distance from roads represents a more favorable habitat for black bear.

### Stream Reclassification

![Stream Reclassification]({{ site.baseurl }}/img/full-size/stream-reclass.png "Stream Reclassification")<br>
This tool shows necessity for water.  As a raster cell gets closer to a stream, the favoraiblity score goes up.

### Trail Reclassification

![Trail Reclassification]({{ site.baseurl }}/img/full-size/trail-reclass.png "Trail Reclassification")<br>
This tool shows one way we try to minimize human-bear encounters.  Optimal habitat is located further away from trails in the park.

### Vegetation Reclassification

![Vegetation Reclassification]({{ site.baseurl }}/img/full-size/veg-reclass.png "Vegetation Reclassification")<br>
This tool categorizes different vegetation types into categories based on black bear's habitat preferences.  Habitat preferences are generally based on food availability and the ability to find trees and dens for escaping predators and raising young.

### Slope Reclassification

![Slope Reclassification]({{ site.baseurl }}/img/full-size/slope-reclass.png "Slope Reclassification")<br>
Bears do well in areas with lower slope.  As slope increases it takes more energy to survive; therefore the favorability score decreases with increasing slope.

A screen capture of the Weighted Overlay dialog box's table clearly showing all parameters. The image needs to show all fields for all input data (if needed screen capture the dialog box/table in two sections);

### Weighted Overlay (2 photos)
![Weighted Overlay]({{ site.baseurl }}/img/full-size/weighted-overlay-1.png "Weighted Overlay")<br>

![Weighted Overlay]({{ site.baseurl }}/img/full-size/weighted-overlay-2.png "Weighted Overlay")<br>

### Final Black Bear Habitat Suitability Model Output
![Model Output]({{ site.baseurl }}/img/full-size/black-bear-map.png "Model Output")<br>