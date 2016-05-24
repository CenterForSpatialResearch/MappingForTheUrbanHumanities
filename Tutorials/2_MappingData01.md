##Mapping Data 

###Mapping Data 01: Mapping World Population(s) to understand the difference between multiple methods of measuring world population 

####Premise

We will work with the basemap we made in Mapping Data 00 and add new data to it in order to examine multiple measures of world population. We will examine population aggregated to cities and countries and a raster dataset that depicts the distribution of world population at a resolution of approximately 1km. 

Open your MappingData_Population.qgs map project.

We have already mapped the locations of populated places (which contains population estimates collected using [LandScan](http://web.ornl.gov/sci/landscan/)) as well as country polygons. We also have tabular data available for population at the country level from the [United Nations](http://esa.un.org/unpd/wpp/Download/Standard/Population/) which we will join to the country polygons, as well as a raster layer that describes world population in 1km grid created by CEISIN. We will answer questions about the differences between the depictions of population at the city, country, and 1km scale. 

####Notes on the data: 

The Gridded Population of the World describes the distribution of population across the planet and is not explicitly linked to geopolitical boundaries. It is created by Columbia’s Center for International Earth Science Information Network (CIESIN) through compiling census surveys from all over the world. You will be prompted to download a version of it in the Mollweide projection (more on projection systems later...) in the next section. The original data is downloadable [here](http://beta.sedac.ciesin.columbia.edu/data/set/gpw-v4-population-count/data-download), the data is free to download however you will need to create an account to access it. 

The data we are using about populated places is aggregated by [Natural Earth v. 2.0](http://www.naturalearthdata.com/downloads/10m-cultural-vectors/10m-populated-places/), the population estimates included in the point file are gathered using [LandScan](http://web.ornl.gov/sci/landscan/) which uses satellite imagery and sophisticated (but some say flawed) algorithms in order to model world population. 

Country-level population data was published by the [United Nations Population Division](http://esa.un.org/unpd/wpp/Download/Standard/Population/) in 2010. All figures are reported in thousands, i.e., if the population field says 7,000 in the dataset this equals 7,000,000 inhabitants. We have provided a cleaned version of this dataset but the original can be downloaded [here](http://esa.un.org/unpd/wpp/Download/Standard/Population/). 

####Downloads
In addition to the data files you have downloaded already you will need to download the Gridded Population of the World raster dataset here. Please create a new folder in your Class_Data\MappingData directory called Raster and save this file there. Once it has downloaded unzip the file so that we can use its contents. 

####Setting up QGIS
Open your MappingData_Population.qgs file. 
It should still contain the countries polygons and populated places points we added previously. (*Note* if these layers are not immediately visible then **right click** on the name of either layer in the `Layer` menu and click `Zoom To Layer`). We will first add CEISIN’s Gridded Population of the World to our map project. Then we will add a tabular data file containing population by country for 2010. This is the information we will join to the countries polygons. 

**Select** the `Add raster layer` button in order to add the CEISIN’s Gridded Population of the World raster layer. 

![add](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/09_Adding_Layers_Raster.png)

Then in the dialog box which opens browse to the MappingData\Raster folder and select gpw-v4-population-count_2010.tif. We will speak about the qualities of raster datasets a bit more later but for now let’s just add it to the map. After you’ve added this layer you can **un-click** the box next to the layer name in int Layers menu in order to toggle the visibility of the layer off. 

Now we will add the table that describes population by country which we will join to the country polygons in order to be able to examine country level population values spatially. QGIS can read several types of tabular data formats, including .csv and .xls files. Our total population file is saved an .xls file (note QGIS cannot generally read .xlsx files saved in the newest version of microsoft excel). We will again use the `Add vector layer` button to add our TotalPopulation_Countries.xls file. (Note: we realize it is a little bit confusing that we use the `Add vector layer` button in order to add tabular data to our map project however this is somewhat a product of the fact that QGIS is open source -- later we will go over how to .csv files which will, more intuitively, be added using the `Add delimited data` button).

![CSV](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/02_Adding_Layers_Vector.png)

Then in the dialog box which opens browse to the MappingData\Tabular folder and **select** TotalPopulation_Countries.xls. You'll notice TotalPopulation_Countries has been added to the Layers menu. Because it is just a table and does not have any geometry it does not show up in our map view. Lets open up its attribute table to see the fields that it contains before we embark on joining it to our country polygons. It contains three columns (or fields): `Country_Code`, `Name`, and `Pop_2010`. 

![CSV](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/09_Attributexls.png)

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

**Proportional  symbols**

We will symbolize the cities layer with symbols that are sized proportionally to their population -- a city with a larger population will have a larger circle and visa versa. 
To do this open the layer properties menu for the populated_places layer and navigate to the Style tab. 

Choose Graduated Symbols. Select pop_max as the column, and Natural Breaks (Jenks) as the mode. Click Classify and then click Apply. The populated places will now be colored according to their population. Now we’ll adjust them by size. 

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/21_Graduate.png)

**Click** on the Advanced dropdown menu in the bottom right and navigate to the `Size scale field` option. Select `pop_max`. **Click** `Apply`. You’ll notice that the circles are huge and fill up the entire screen. Return to the `Size scale field` and now select `expression`. In the expression builder window that opens write the following `“pop_max” / 1000000`. Click `Okay` in the expression builder then click `Apply`. Click Okay to close the Properties window. 

The outcome of your selections should look something like this:

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/22_Graduated2.png)

**Choropleth**

We will create a choropleth map for population by country, where each country will be colored according to its population size. 

**Open** the properties for the admin_0_countriesUNPop layer and navigate to the Style tab. Select Graduated Symbols from the dropdown at the top left, and select Pop_2010 as the Column on which we will color the map. Then in order to change the color of the entire country polygon we will need to change the symbol from an outline to a filled polygon by clicking the Change button next to Symbol and selecting “simple fill.” Next we will break up our data into classes, or ranges of values, and classify the colors for our choropleth map according to these. 

Change the mode to Natural Breaks (jenks), and the number of classes to 8. Then **Click** `Classify`. Your properties menu will now look like the one below. Click `Apply`. The country polygons will change on the map. 

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/22_Choropleth.png)

**Raster Classified Color Ramp**

Next we will symbolize our gridded population of the world layer. This layer is different from the ones we have been primarily working with thus far because it is a raster dataset. 

As we discussed briefly in the lecture a raster is a data layer that is composed of a grid of cells, or pixels, of a specific size where each cell has a value that represents information. In our case each cell has a value for population. Unlike a vector data layer which has an attribute table and each point, line or polygon can have multiple values associated with it, a raster grid cell can only have one value. Examples of other types of raster datasets include, temperature gradients, satellite images, and scanned historical maps. 

If it isn’t already check the box next to the gridded population layer, gpw-v4-population-count-2010, to make it visible if it is not the top layer drag it in the Layers menu so that it is the top visible layer. It will largely be black. Now open the properties menu for the gridded population layer. Navigate to the style tab. You’ll notice that this looks different than the style menu we have been working with for our vector layers. Instead of a symbol type we have an option for ‘Render type’ and many options for how to color the bands in our dataset. 

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/23_RasterSymbol.png)

Here you will see that the default style is `Singleband gray`, which means that it's only symbolizing in grayscale based on one band (other raster datasets can be made up of multiple bands, some examples of these include satellite images and color historical maps). The color gradient is currently set as `Black to white` but that can be switched to `White to black`. 

And it is symbolizing based on the minimum value, in this case '0' and on the maximum value, '422.56'. Now, that's not actually the maximum value of the raster dataset. If you look at the right-hand panel (`Load min/maxvalues` highlighted in blue), which is where the min and max values come from, you will notice that the min/max values are being calculated based on a `Cumulative count cut`, which is used to get rid of the outliers. The Cumulative count cut means that QGIS is only taking into account the values between 2% and 98%, in the default cases. You could change that and use the option Min / max to use the actual minimum and maximum values. If you choose this one, you have to click on the Load button to load the new values. Do this and click on `Apply` to see how the image changes. Now the minimum is still '0' but the maximum is '140853'. Because of this new maximum value, most of the image appears black.

Now change the `Render type` to `Singleband pseudocolor` to get something similar to a symbology we would do for a vector file. On the right-hand panel you will see the `Mode of classification` (`Continuous` or `Equal Interval`) and below, again, the Load min/max values panel. Click on the `Classify` button to load the values and then hit `Apply` to see it on the map. Now you can see clearly the regions of the world with the highest population density. You can experiment with the style of your map by changing the colors used with the pulldown menu highlighted in blue.

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/24_Pseudo.png)

####Designing a map
In order to present these three types of population measures we will now compose a map layout and become familiar with the QGIS map composer. The map composer allows you to add a legend, north arrow and scale bar to the map as well as to export our work as a PDF. 

Create a map composition where all three depictions of world populations are values. You can adjust the transparency of your data layers using the style menu. Experiment with changing the colors of the different layers to become more familiar with the style menus for raster and vector layers. 

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/26_LayerTransparency.png)

Once you are pleased with your map composition we will create a new print composer. When prompted you can either name the print composer or not. 

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/25_PrintComposer.png)

To add a new map to the composer select the add new map button. Then click once to begin to drag a rectangle over the area on the page that you would like the map to occupy and click again to stop. Whatever is showing in your QGIS map project window as you create this new map in the print composer is what will appear in the new map. 

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/27_PrintComp.png)

Next we will add a legend. Select Add new legend, and again click to draw a rectangle where you would like to place the legend. An unformatted legend that matches the information from the Layers panel will appear. You can use the options in the Item Properties tab (circled in blue) to change which layers are represented in the legend and to change the labeling of the layers in the legend. Scroll within this tab to familiarize yourself with which properties about the legend you can change. 

We will format the legend and change the titles of each dataset so they are more descriptive. To do this un-click “Auto update” to make changes, then change the layer names by clicking the “legend item properties” button circled in magenta. 

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/27_PrintComp1.png)

Next we will add a scale bar. Click the add new scale bar button. Again you will be able to change the properties of the scale bar, including the style, number of segments and size. 

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/27_PrintComp2.png)

Last we will add two text boxes, one with a title for the map and another with abbreviated citations for our data sources. Click the add new label button then use the Main properties field to add the text you want, and use the Font button to change the text size and font. 

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/27_PrintComp3.png)

Finally use one of the export options circled in blue above to save the map composition as an image file, PDF, or SVG. 

![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/Mapping_WorldPopulation.png)
