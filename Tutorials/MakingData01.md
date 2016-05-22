##Making Data

###Georeferencing Exercise

In this exercise, you will explore some of the georeferencing tools available in QGIS and use then to georeference a 1902 map of the Bronx.   

Open QGIS:

![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef1.png)

You are going to use OpenStreetMap (OSM) as reference data for the georeferencing process.  OSM provides a free, open-source map of the world from public domain and volunteered data.   You can view the OSM basemap service is QGIS through the OpenLayers plugin.  This plugin does not come pre-installed with QGIS, so you will probably need to add it.  Under the plugins menu, select “Manage and Install Plugins…” 
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef2.png)

The plugins dialog will open.  Search for “Openlayers Plugin.”  Highlight it, and click “Install plugin”:

![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef3.png)

It may take a few seconds to install.  Close the plugins menu when finished.  The OpenLayers tools should now appear under the Web menu: 

![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef4.png)

This plugin will allow you to view a number of basemap services and steam them directly into your QGIS workspace.  Choose the OpenStreetMap>OpenStreetMap option.
Since you are working in a new QGIS project, the map should show the entire earth as the default: 
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef5.png)
Use the zoom in tool ![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef6.png) and zoom into the Central Bronx in the area around The Botanical Garden:
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef7.png)
Now you will access the georeferencing tools and match the scanned map to the OSM map.  

Under the Raster menu, select Georeferencer>Georeferencer:
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef8.png)

The Georeferencer screen will open:
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef9.png)

Click on the Add Raster button ![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef10a.png) and navigate to the image file in the working directory and open it.  It will appear in the georeferencer window:
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef10b.png)

This map is one sheet of six of a map of the East Bronx in 1902.  If you would like to see the entire map, there is another copy (in a lower resolution) in the New York Public Libraries digital collections here: http://digitalcollections.nypl.org/items/dc910ee0-4682-0131-4759-58d385a7bbd0
This section represents the area around the New York Botanical Garden and the (just opened) Bronx Zoo. Fordham University can be seen just to the southwest of the garden and the Norwood neighborhood is in the northeast corner.  The area to the east of the Bronx Park area is still largely undeveloped at this point.  
Historical maps can be difficult to georeference, and this sheet poses a number of complications.  The map projection is unclear and there are no ground control points or coordinates specified.  Because of this, you will georeference by matching physical features represented on the map with their current counterparts (and their known coordinates).  However, most of the features in this map have changed or no longer exist (or were never actually built in the first place).  Thus, you will need to be very careful to choose locations that you are confident match up well with their contemporary counterparts.   Fortunately, there are a number of good candidates, particularly on the western half of the map where many streets and buildings still exist in the same location.  You will use those to georeferenced the map.
The QGIS georeferencer does not allow you to view both the scanned map and the workspace at the same time, so you will have to inspect both maps in turn and choose carefully to select locations to add georeferencing control points. 
One candidate is the Haupt Conservatory in the Botanical Garden which continues to exist largely its original configuration.  Using the georeferencer zoom tools ![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef11.png) to zoom to the conservatory structure in the southwest corner of the park: ![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef12.png)


![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef13.png)
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef14.png)
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef15.png)
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef16.png)
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef17.png)
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef18.png)
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef19.png)
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef20.png)
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef21.png)
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef22.png)
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef23.png)
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef24.png)
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef25.png)
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef26.png)
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef27.png)
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef28.png)
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef29.png)
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef30.png)
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef31.png)
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef32.png)
![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData01/GeoRef33.png)
