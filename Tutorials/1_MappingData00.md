##Mapping Data 

With this exercise, you will learn introductory skills involved in using ArcGIS to map existing spatial datasets. After the completion of this set of exercises, you should have…

1. become familiar with the QGIS user interface 
2. learned the components of shapefiles 
3. created a clear and effective map composition 
4. critically considered symbology and classification and the differences between mapping qualitative and quantitative information 
5. created and calculated new fields in an attribute table 
6. performed a table join to combine additional data to an existing shapefile’s attribute table 
7. queried a GIS dataset, using both tabular queries and spatial queries 
8. accessed the metadata of an existing GIS dataset
9. worked with projections and examined the impacts of projection transformations on spatial analysis

####Part 00
Download the GitHub repository for this course. The Class_Data folder will then have all of the datasets needed for tutorials. 

###Mapping Data 00: Mapping World Population(s)
####Premise
We are interested in creating a map of world countries and cities (and at the same time exploring the QGIS interface). We have a point file for the locations of populated places around the world as well as a polygon file for country boundaries. This map will serve as a basemap to which we can add additional information and layers in order to examine multiple measures of population and the differences between them.
####Setting up QGIS

**Launch** QGIS. Your new blank map project will look like this:

![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/01_OpenQGIS.png)

Begin to familiarize yourself with the interface.

####Adding Layers

In order to construct our map within QGIS we will need to add our data layers to the map project. There are several ways to accomplish this however we will begin by using the `Add Vector Layer` button. 

![vector](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/02_Adding_Layers_Vector.png)

**Navigate** to the MappingData\Shape\ folder and add the populated_places.shp and admin_0_countries.shp files. Note you can select multiple shapefiles by holding down Command (on Mac) or Ctrl (on Windows) while individually clicking the file names. 
The selected layers will be added in default colors. 
![layers](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/04_LayerOrder.png)
The cities layer is represented by points and the countries layer is represented by polygons. The order of the layers can be controlled with the `Layers panel` to the left of the Data Frame. 

**Click** and drag the admin_0_countries layer on top of the populated_places layer. The cities points are no longer visible because they are behind the countries polygons (or only visible at the borders of the countries and the oceans). 

![order](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/03_Adding_Layers.png)

We can change this by removing the fill color of the country polygons, leaving only the outline of their boundaries. To do this, we must change the style of the data layer. That is, we will change the way the data is styled or symbolized on the map. The simplest style for any dataset is to apply a single symbol to every feature within the layer. 

We will display the countries as just borders. To access the `Style Menu` **double-click** on the layer name in the Layers panel, or **right-click** on the layer name and select `Properties.`  There are many different ways to symbolize data on a map through QGIS. For now, we will just use one style for all of the features in the layer. 

![properties](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/05_Properties.png)

Once inside the Layer Properties Menu **select** the `Style` tab. **Select** `Simple Fill` and then in the `Symbol layer type` menu **select** Outline: Single line. 

![style](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/05_Style.png)

When your style settings are finished, **click** `OK` to exit the properties menu. You should now be able to see each of the populated places points through the empty country polygons.

![style](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/06_PopulatedPlaces.png)

**Save** your QGIS project by selecting `Project` > `Save`. Name your project MappingData_Population.qgs and save it in the Tutorials/Exercises folder. QGIS projects are saved as .qgs files. It is important to note that the data layers are not saved with it the map project but are rather linked to the project.






