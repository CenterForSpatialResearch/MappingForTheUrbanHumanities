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

**Save** your QGIS project by selecting `Project` > `Save`. Name your project MappingData_Population.qgs. QGIS projects are saved as .qgs files. It is important to note that the data layers are not saved with it the map project but are rather linked to the project.

###Mapping Data 01: Mapping World Population(s) to understand the difference between multiple methods of measuring world population 

####Premise

We will work with the basemap we made in Mapping Data 00 and add new data to it in order to examine multiple measures of world population. We will examine population aggregated to cities and countries and a raster dataset that depicts the distribution of world population at a resolution of approximately 1km. 

We have already mapped the locations of populated places (which contains population estimates collected using [LandScan](http://web.ornl.gov/sci/landscan/)) as well as country polygons. We also have tabular data available for population at the country level from the [United Nations](http://esa.un.org/unpd/wpp/Download/Standard/Population/) which we will join to the country polygons, as well as a raster layer that describes world population in 1km grid created by CEISIN. We will answer questions about the differences between the depictions of population at the city, country, and 1km scale. 

####Notes on the data: 

The Gridded Population of the World describes the distribution of population across the planet and is not explicitly linked to geopolitical boundaries. It is created by Columbia’s Center for International Earth Science Information Network (CIESIN) through compiling census surveys from all over the world. We have included a version of it in the Mollweide projection (more on projection systems later...)with the files for this course however, it is also downloadable [here](http://beta.sedac.ciesin.columbia.edu/data/set/gpw-v4-population-count/data-download). The data is free to download however you will need to create an account to access it. 

The data we are using about populated places is aggregated by [Natural Earth v. 2.0](http://www.naturalearthdata.com/downloads/10m-cultural-vectors/10m-populated-places/), the population estimates included in the point file are gathered using [LandScan](http://web.ornl.gov/sci/landscan/) which uses satellite imagery and sophisticated (but some say flawed) algorithms in order to model world population. 

Country-level population data was published by the [United Nations Population Division](http://esa.un.org/unpd/wpp/Download/Standard/Population/) in 2010. All figures are reported in thousands, i.e., if the population field says 7,000 in the dataset this equals 7,000,000 inhabitants. We have provided a cleaned version of this dataset but the original can be downloaded [here](http://esa.un.org/unpd/wpp/Download/Standard/Population/). 

####Setting up QGIS
Open your MappingData_Population.qgs file. 
It should still contain the countries polygons and populated places points we added previously. (*Note* if these layers are not immediately visible then **right click** on the name of either layer in the `Layer` menu and click `Zoom To Layer`). We will first add CEISIN’s Gridded Population of the World to our map project. Then we will add a tabular data file containing population by country for 2010. This is the information we will join to the countries polygons. 

**Select** the `Add raster layer` button in order to add the CEISIN’s Gridded Population of the World raster layer. 

![add](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/09_Adding_Layers_Raster.png)

Then in the dialog box which opens browse to the MappingData\Raster folder and select gpw-v4-population-count_2010.tif. We will speak about the qualities of raster datasets a bit more later but for now let’s just add it to the map. After you’ve added this layer you can **un-click** the box next to the layer name in int Layers menu in order to toggle the visibility of the layer off. 

**Select** the `Add delimited data` button in order to add the table containing population by country. 

![CSV](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/09_Adding_Layers_Delimited.png)

Then in the dialog box which opens browse to the MappingData\Tabular folder and **select** TotalPopulation_Countries.csv. Select `CSV (comma separated values)` as the file format, this describes the way that the tabular dataset is structured. Notice that there is also a file named TotalPopulation_Countries.csvt in the MappingData\Tabular folder, this file tells QGIS the data type for each field in the TotalPopulation_Countries.csv -- we will cover this in greater depth later on.

**Select** `First record has field names,` because we have formatted the table so that the names of the variables are in the first row. Select `No geometry (attribute only table)` for the Geometry definition. Then use the preview window to make sure the dataset is displaying correctly. You should see three columns with the headers, Country_Code, Name, Pop_2010. 

![CSV](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/08_AddCSV.png)

####Performing a Table Join
In order to answer questions about world population by country we will join tabular data published by the United Nations to the country polygons we have already mapped. A table join allows GIS users to combine tabular data with vector data based on an identical field in their attribute tables.  

We have already cleaned the TotalPopulation_Countries.csv file and removed additional rows included in the original dataset that we will not need for our purposes here. In addition, we have abbreviated the column names and reformatted them so that they can be read by QGIS. In future exercises we will cover in depth how to clean, format, and save data so that it can be read by QGIS.  

**Right-click** admin_0_countries in the layer menu and select `Open Attribute Table`. The layer’s attribute table will appear. This describes the data associated with each feature in the feature class.

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/10_AttributeTable.png)

In order to join attributes from a table to a shapefile the two data sets must share a common attribute field. 
Let's review the fields in the attribute table for the admin_0_countries layer:

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/11_Admin0FieldNames.png)

They are: 
* NAME, NAME_LONG: a text name for the admin 0 area or country
* ISO_N3: the unique three digit code assigned to each country by the International Organization for * Standardization (ISO). 
* REGION_UN: a text name for the UN designated region the country lies within. 
* SUBREGION: a text name for the UN designated subregion the country lies within. 
* Cnt_Code: a unique code assigned to each country, that matches the ISO code but without preceding zeros.

Let’s review the column names in the TotalPopulation_Countries.csv file. **Open** the attribute table in the same way we just opened the attribute table for the admin_0_countries layer.
* Country_Code: a unique numeric code corresponding to each country
* Name: text name for the country
* Pop_2010: estimated population of country in 2010

Note that the Country_Code is identical to the Cnt_Code for each country, and each is unique -- no two countries have the same ISO_N3 number. This unique field common to both datasets is what allows us to join the tabular population data to the vector file describing the geometry of those countries. 

We always start the join on the file that we are joining to. Here, we are joining the population estimates table to the country boundary shapefile. Thus, Open the Properties for admin_0_countries, and navigate to “Joins” in the left hand menu. Click the “+” icon. Make the following selections in the dialogue box which appears.

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/12_JoinDialogue.png)

**Select** TotalPopulation_Countries as the “join layer”, Country_Code is the “join field”, and Cnt_Code is the “target field” which matches the join field in the admin_0_countries layer. Select the box next to “Custom field name prefix” and delete the contents of that field (note this is a helpful field if we are joining data from many different tables to one shapefile as it allows you to distinguish the source table). **Click** `OK` to close the join dialogue. Then **Click** `OK` to close the layer properties menu. 

Open the attribute table for the countries shapefile. You’ll notice two new fields have been joined to the right hand side of the table: `Name` and `Pop_2010.`

Note: the population estimates data that is joined to the country boundaries is not permanently associated with its attribute table. Instead the relationship only exists within this QGIS project. If we added the admin_0_countries layer to another QGIS project the fields we have joined from the population estimates would not be there. 

In order to permanently incorporate the population estimates into a shapefile of world countries we must save a new version of the shapefile. **Right-click** on admin_0_countries in the layers menu and select `Save.` Select `ESRI Shapefile` as the format, and save your file in the MappingData\Shape folder as admin_0_countries_UNPop.shp. 

This new layer will then be added to the map and will contain the population estimates that we joined from the UN tabular data. 

####Attribute Tables and Data Querying

Now that we have assembled these data layers we can begin to ask a few simple questions about the different measures of world population that each depicts. We will accomplish this by querying the attribute fields of our two vector layers, the populated places and the countries. To do this we will select features using an expression which is sometimes referred to as Select by Attributes. In addition we will use 

We will answer a few questions: 
* How many cities have populations of greater than two million people? 
* How many countries have populations of less than seven million people? 
* How many cities with more than two million residents are within countries where the total population is less than seven million?

In order to answer these questions we’ll first select just those cities which have populations of more than two million. Then we will export that as a separate layer. Then we will do the same for countries which have populations of greater than seven million people, and also less than seven million. 

There are multiple routes to select features within a dataset, either we can open its attribute table and select `select features using an expression` or we can highlight the layer in the layers menu and select the `select features using an expression` button in the main toolbar. 

Option 1: 

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/13_SelectByExpres.png)

Option 2:

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/13_SelectByExpression.png)

Either route will open the `Select by Expression` tool. We can be sure we are selecting features from the correct layer from the header of this dialogue box. Here we see that the header reads “Select by expression - populated_places” and because we will select the cities first we know we are selecting features from the correct layer. 

If we click on any of the terms in the central box (highlighted in magenta) a description of it will appear on the right side (highlighted in blue). We will combine the field name with other operators which we will find in the magenta box in order to build an expression in the green box on the left side. 

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/15_SelectExpressionMenu_opt.png)

We want to select just those cities with a maximum estimated population of greater than two million. To do this we will expand 'Fields and Values` and select `max_pop`. **Double-click**  on `max_pop` and it will appear in the expression box on the right. Next we will open `Operators` and double-click on the greater than symbol (>). We will then type in 2,000,000. Your expression should now look like the following. 

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/16_SelectionExpression_Final.png)

**Click** `Select`. You should notice that some of the populated_places points will turn yellow. In addition at the bottom left corner of your QGIS project the footer will tell you how many features were selected: we see that 215 cities were selected. 

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/17_SelectOutcome.png)

We will now save those 215 cities as a separate shapefile, just like we did for the admin_0_countries layer after we joined the UN population estimates to it. **Right-Click** populated_places in the Layers menu, **select** `Save As`. Then in the dialogue box which opens select `Save only selected features`, and save the shapefile in MappingData\Shape as populated_places_2mil.shp. This will then be added to our map as a new layer. In order to see the new layer clear your selection by clicking the `Deselect features from all layers button.`

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/18_Deselect.png)

####Select by location

As we outlined above  we are interested in finding out how many countries have fewer than seven million inhabitants, and then how many cities with over two million inhabitants fall within those boundaries.  In order to answer these two questions we will need to perform a spatial query by layering these two datasets rather than merely querying within the attribute table of one dataset. 

**Open** the attribute table for admin_0_countriesUNPop and select the `select features using an expression` tool. We will again select by expression in order to select the countries with fewer than seven million inhabitants. Use the expression builder as we did above with the populated places in order to select the countries with fewer than seven million inhabitants. Remember the dataset is expressed in thousands thus 7,000,000 will appear in the data as 7000. Your expression should read:  `"Pop_2010"  < 7000`

The header bar of the attribute table will indicate that 124 of 238 features were selected. 

Now, we will use this selection to identify which cities of greater than two million people are within countries with fewer than seven million people. To do this we will use the select by location tool. On the menu bar navigate to `Vector`>`Research Tools`>`Select By Location`. In the dialogue box that opens make the following selections: 

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/19_SelectLocation.png)

In the bottom left hand corner of your QGIS window you will see that five populated places were selected. Open the populated places attribute table and identify which cities these are by choosing `Show Selected Features` from the dropdown menu at the bottom left of the window. 

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/20_SelectedFeatures.png)

####Symbolizing World Populations

Now that we have these three different layers we can begin to create maps that highlight the differences between these different ways to measure population. We will compose a map that symbolizes each of our three data layers differently. We will use graduated symbols to express city population, a choropleth map for population by country and a classified color ramp for the gridded population. We will then go over cartographic conventions adding a legend and scale bar to the map and exporting as a PDF. 

*Proportional  symbols*
We will symbolize the cities layer with symbols that are sized proportionally to their population -- a city with a larger population will have a larger circle and visa versa. 
To do this open the layer properties menu for the populated_places layer and navigate to the Style tab. 

Choose Graduated Symbols. Select pop_max as the column, and Natural Breaks (Jenks) as the mode. Click Classify and then click Apply. The populated places will now be colored according to their population. Now we’ll adjust them by size. 




