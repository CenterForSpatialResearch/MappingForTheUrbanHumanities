##Mapping Data 

###Mapping Data 02: Mapping Projections and Population Density

####Premise
We will now zoom in to the level of the continent and examine population along historical rail lines. We are interested in investigating population growth in counties that contain rail lines between 1850 and 1870. In addition, we will learn about projection systems and will observe the impact that changing projection systems has on spatial analysis by comparing population density calculated under different projection systems.   

####New Downloads Before We Begin
**Before we begin the tutorial download `Counties_1870_Albers_PopJoin-.zip` from [this link](https://drive.google.com/file/d/0B5KywkNXsT4JMFkzdlR1Vl9KVk0/view?usp=sharing)**. Save this in the Class_Data\1_MappingData\Shape folder. 

####The Data

We will be working with data created and published by the University of Nebraska Lincoln of historic rail networks in the U.S. We have two shapefiles, one for rail lines built as of 1850, and another for those built as of 1870. We have already included the data in the Mapping Data folder however it is available [here](http://railroads.unl.edu/resources/) for download.  

In addition, we will use historic census information for population by county which has been digitized, aggregated and published by the Minnesota Population Center at the University of Minnesota as part of their [National Historic Geographic Information System (NHGIS)](https://nhgis.org) project. This project is an amazing resource for historical research. We will be using population values for counties from the USA wide agricultural census of 1850 and of 1870 to match with the dates of our rail lines. We have already downloaded the data that we will be using however for future reference we have included brief instructions for how to download data from NHGIS at the beginning of the tutorial. 

####Downloading Data from NHGIS
This section is already completed for you and the data is downloaded in the MappingData\Tabular and MappingData\Shape folders respectively however this brief tutorial goes over the basics of downloading data from the NHGIS for future work. 

We will go through the steps for searching for and downloading historical census data and associated GIS boundary files. As an example we will download 1850 population by county along with the 1850 country boundary shapefile which we can associate the population information with through a table join.   

**Navigate** to [https://nhgis.org](https://nhgis.org) using your browser of choice. In the menu on the left choose `Select Data.`

![add](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData02/01_NHGIS.png)

Then use the filters which appear to search for the data you are interested in. First we will filter their archive by geographic level, and will select counties. 

![add](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData02/02_NHGISFilters.png)

Select `Geographic Level` from the filter options. 

A menu will open containing all of the available geographies. Click on `County (by State)`, this will open an information menu which outlines which datasets are available at this level of geography. We can scan this to confirm that the 1850 Agricultural Census is available at the county level. 

![add](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData02/03_NHGIS_Geography.png)

Once we have confirmed that the information we are interested in is available at the desired geography click the plus icon next to `County (by State)` to add it to our selected geographic level filters. Select Submit. The geographic level filters menu will close and all of the source tables available at the county level will appear. 

Next repeat this process to filter the results to display only the tables available for 1850. Then use the `Topics` filter to select `Total Population.`

Our results will now be narrowed to look like the image below. We have found the Total Population from 1850. You can select the source table name in order to view more information about it. 

![add](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData02/04_NHGIS_SourceTable.png)

**Select** the plus icon at the left of the Total Population table name to add this dataset to our selections. You’ll notice the `Data Cart` in the upper right hand of the screen reflect this.

We have selected the tabular data for population. You’ll recall that in order to work with this data spatially in GIS we will need to download GIS boundary files of the same geography for the same year. NHGIS makes this very easy. Select the GIS Boundary File tab circled in the image above. You’ll find there are two options for county boundary files for 1850. We want the file whose “Basis” is the `2000 TIGER/Line +` (NHGIS has a helpful explanation for why we are making this choice if you click on one or the other of the two boundary file names). 

Again, **select** the plus icon next to the desired boundary file to add it to the datasets we have selected to download. Select continue on the Data Cart. 

You will then be prompted to review your selections, make sure that you have selected both the source table and the GIS Boundary File, then click continue again. 

You will now be prompted to review and submit your selections and can add an additional description for future reference. Select `Comma delimited` as the table file structure, then click submit. 

On the next screen you will be prompted to create an account with NHGIS. The Minnesota Population Center provides all of its data for free however it requires users to create an account before downloading. Create a new account. Then login and you will be brought back to your data extract queue. 

This list will display all of your recent extracts and the status of each download. We see that the data we have just selected for download is currently queued. Very large files can take several minutes to be compiled and prepared for download. NHGIS will send an email to the address associated with you account when you data is ready for download, however we can also check on the status by refreshing our browser window. 

When the data is ready for download its status will be listed as complete and you can click on tables and gis in order to download the shapefile and attribute tables. 

![add](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData02/05_NHGIS_Download.png)

Your next step will be to join the table of population data to the county boundary shapefile. We will go through this together below. 

####Preparing your data
**Performing a Table Join**

The 1850 and 1870 population data that we will be working with is in tabular form and thus we will then need to join his data to county boundary polygons in order to analyze and represent it spatially. We have already performed one table join in the previous exercise, so this will be review. We will only do this for 1850, we have provided you with a shapefile of counties in 1870 with population data already joined to them. 

First, **open** Microsoft Excel and then navigate to Course_Data/MappingData/Tabular and open `nhgis_1850_Population_county.csv`. In addition open and its associated codebook `nhgis_1850_Population_county_codebook.txt` with the text editor of your choice. NHGIS uses some abbreviated naming conventions for its columns which are not entirely intuitive, however the codebook which is always automatically downloaded with their data clarifies the meanings of these column names. 

In the 1850 population CSV file you’ll see 8 columns: GISJOIN, YEAR, STATE, STATEA, COUNTY, COUNTYA, AREANAME	, ADQ001. 

If we look in the codebook we’ll notice that ADQ001 is the field that contains total population value for each county. Lets rename ADQ001 something more intuitive: POP_1850. 

Recall from the previous exercise, that in order to add a table to QGIS it must be saved as an .xls file (note for future reference there are other tabular file formats that QGIS can read however xls files are the easiest way to make sure that QGIS understands the datatype contained in each column of your data). 

**Save** the nhgis_1850_Population_county.csv file as a .xls. **Select** `File`>`Save As`. Then select `Excel 1997-2004 Workbook (xls)` as the File format and save the file as `nhgis_1850_Population_cty.xls` in the MappingData\Tabular folder. 

![add](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData02/06_xls.png)

Now we can join the 1850 population data to the county polygons for 1850 and begin to ask some questions about population along train lines in 1850 and 1870. 

**Launch** QGIS. 

First add the other vector data layers we will be working with using the `add vector layer` button and then navigating to Course_Data/MappingData/Shape and adding 

* USCounty_1870_Albers_PopJoin-1.shp 
* USCounty_1850_Albers.shp
* RR1850_Albers.shp
* RR1870_Albers.shp files

Then add the table of population values using the `add vector layer`button:
* nhgis_1850_Population_cty.xls


**Save** your QGIS project as MappingData_02_Population in the MappingForTheUrbanHumanities\Tutorials folder.

We will now repeat the steps we took in the previous exercise to join the 1850 population data to the 1850 counties shapefile. 

Open the `layer properties` for USCounty_1850_Albers. Navigate to the `Joins` tab on the left of the properties menu and select the plus icon. Then, make the following selections: 

![add](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData02/08_JoinSelections.png)

To reduce the total number of columns we are adding to the attribute table of the country boundaries we have selected to join only the area name and population fields to the shapefile. This is not a necessary step but can be helpful to keep attribute tables from getting too many columns after table joins. 

By choosing to create a custom field name prefix and deleting the contents of this box we will eliminate a prefix to the field names we are joining to the table. This can be a helpful way to distinguish between many different fields if you are joining values from many different tables to the same shapefile however it also makes the field names longer and more cumbersome.

Click OK on the Add vector join dialog box, then click `Apply` on the properties join menu.

**Open** the attribute table to verify that the `POP_1850` field was joined to the counties shapefile. Then to create a new layer with the population data permanently present in the attribute table, save as US_county_1850_Albers_PopJoin.shp. 

Do not change the selected coordinate system. We will do this next. 

**Save** your map project.

####Using the Identify Features tool
Before we experiment with applying different projection systems to our data, lets use the identify features tool in order to look at population change along rail lines between 1850 and 1870. This tool allows us to examine attribute values for a specific feature without opening the attribute table. It complements the ability to select a feature by attributes and by location which we covered in the previous exercise.
Choose a county that had a train line by 1850 (and still had one in 1870), and determine the size of its population in 1850 and then in 1870. You can do this for several counties. Select the identify features tool in the top menu.   

![add](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData02/09_Identify.png)

The layer that the identify features tool selects is determined by which layer is highlighted in the layers menu. Select US_county_1850_Albers_PopJoin so that it is highlighted in the layers menu.

You may need to zoom in closer on the map in order to select just one county. Once you have selected a feature the values from its attribute table will be shown in the Identify Results window. 

Note the 1850 population in your selected county then select US_county_1870_Albers_PopJoin so that it is highlighted in the layers menu and again use the identify features tool to note the population for that county in 1870. 

![add](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData02/10_IdentifyChicago.png)

####Working with Projections

We will now explore several projection systems and assess the impacts that re-projecting our data has on the shape of our map as well as on calculations such as area and population density. 

First we will review some terminology:

**Geographic coordinate system**
* A geographic coordinate system (or GCS) is a means for defining the locations of coordinates on the earth on a three dimensional spheroid – it is a way to model the shape of the earth in Cartesian space. Points are located using their latitude and longitude values and distances are expressed in an angular unit of measure such as decimal degrees. 

**Datum**
* A datum is a set of transformations that translates a spheroid model of the earth to the irregularities of the earth’s actual surface. Each geographic coordinate system is based off of a specific datum. The World Geodedic System (WGS) 1984 is widely used today and is the default in QGIS. 

**Projected Coordinate System**
* A projected coordinate system is a series of mathematical transformations that translate geographic coordinates (the GCS), which are the coordinates of locations on a curved surface, into locations on a flat surface. All projected coordinate systems introduce distortions to our spatial features and thus it is important to choose a coordinate system well suited to the area of interest of a map or to a specific argument. There are lots of different projection systems each with different advantages: some preserve areas, others distance, direction.

We will first check the current projection of our map layers and then re-project our data and explore the results. 

**Open** the layer properties for US_county_1870_Albers_PopJoin-1 and select the General tab. The projection or the geographic coordinate reference system for the layer is displayed in the highlighted area. 

![add](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData02/11_Projection.png)

In this case the coordinate reference system (CRS) is the USA Contiguous Albers Equal Area Conic, this is a projection system that is often used for the U.S. which, as the name suggests, preserves areas. (We have already included Albers in the name of the layer to indicate this choice of projection in an attempt to model one often helpful naming convention.) You can now close the layer properties menu.

Any spatial data format is associated with a coordinate reference system, either projected or coordinate (in a shapefile this projection information is store in the .prj file, and in a raster dataset the projection is stored in a file with the extension .tfw or .jgw). 

Similarly, each map project has a coordinate reference system on which it bases its visualizations and calculations of your spatial data. The coordinate reference system (either projected or not) of your map project is set automatically by the first layer that you add to it. If you add any subsequent data layers to the map that have different projection systems QGIS will visualize them to match the coordinate reference system of the first data layer. This is called an “on the fly” CRS transformation. We can also change the coordinate reference system (CRS) of the map project “on the fly” and thus change the appearance of the projection for all the data layers on the map. 

However, “on the fly” CRS transformations do not actually change the underlying data. Thus for any analysis or comparisons across multiple data layers it is important that we manually change the coordinate reference system so that it is the same across each of our data layers. 

Recall, our goal in this portion of the exercise is to observe the impacts of changing projections visually and quantitatively. 

First we will visually observe the transformations of our datasets under different projection systems and then we will save a layer in a new transformation and perform several calculations. 

First, open the project properties menu by navigating to project > project properties. Select the CRS tab and make sure that enable “on the fly” CRS transformations is checked. If you scroll through the available coordinate reference systems that are shown in the box highlighted in pink you can observe the many different projection systems supported by QGIS. The selected CRS will appear in the box highlighted in blue. Currently the selected CRS is USA Contiguous Albers Equal Area Conic, notice that this is the same CRS as the data layers that you added to your map project when you created it. 

![add](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData02/12_OntheFly.png)

Next we will select a few projections and observe the changes in the geometry of the map. Select a few coordinate systems of your choice from the pink box, in order to view each click Apply. Some common projection systems used for the U.S. are: North America Lambert Conformal Conic, Universal Transverse Mercator (UTM) Zones 10-19, and increasingly the Mercator projection (as a result of web mapping platforms that only support the Mercator projection). [This project](http://bl.ocks.org/syntagmatic/ba569633d51ebec6ec6e) is another great way to view the relative benefits of several different projection systems. 

**Select** the UTM 10N projection by typing it in to the filter box highlighted in yellow. Click `Apply`. This is a projection well suited for maps of the western coast of the U.S..

Now that we have explored the visual transformations produced by different projection systems we will perform several calculations to highlight the effect of projections on quantitative analysis and observations. 

Specifically, we will ask, what were the ten densest counties in 1870, and compare the results obtained under two different projection systems. 

**Right-click** US_county_1870_Albers_PopJoin-1 in the layers menu and select `save as`. Save the new layer as US_county_1870_UTM10_PopJoin. In the dialog box which opens click the globe next to the CRS bar in order to browse for UTM zone 10N using the coordinate reference system selector. Click `OK` on both windows to save the layer.  

![add](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData02/13_SaveAsUTM.png)

####Using the field calculator 

Next open the attribute table of US_county_1870_UTM10_PopJoin. Notice the Dens_AlbKm field. This stands for population density per square kilometer calculated using the Albers projection. We will now calculate a similar field by under the UTM Zone 10 projection in order to compare these two and notice the impact of the change in area on population density. 

In the attribute table select the `Open field calculator` button 

![add](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData02/15_CalculateField.png)

Using the field calculator we will be able to add an additional column to the attribute table for this layer and calculate a value for it based on the geometry of the features as well as values in the attribute table.

The field calculator functions nearly identically to the select features using an expression tool that we used in the previous exercise. 

Calculate population density per square kilometer of each county based on the new area under the UTM Zone 10N projection, save this information in a new field called Dens_UTKm. Be sure to change the output field type to `decimal number (real)`. Set the output field width to 10, and the precision to 3. And construct the expression shown below. (Note: we have divided the area by 1,000,000 because the units of the UTM projection are square meters). Click `OK`.

![add](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData02/14_AreaCalc.png)

Now click the toggle editing mode to save the new field. Sort the attribute table by the Albers Equal Area projection population density (do this by clicking on Area_AlbKm) and compare these values with the UTM Zone 10N population density. You’ll notice they’re vastly different.  

![add](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData02/16_ToggleEdit.png)

Close the attribute table. 

####Expressing differences in population density in a choropleth map

Next we’ll create two choropleth maps which highlight the differences between these two calculations of population density. One for the Albers population density and the other for the UTM Zone 10 Population Density. 

**Right-click** the US_county_1870_PopJoin_UTAlb layer and select `Duplicate`. Open the properties menu for US_county_1870_PopJoin_UTAlb and in the style tab choose `graduated` as the symbol type and create a choropleth map based on the Dens_AlbKm layer. Choose `natural breaks (jenks)` as the mode and choose 5 as the number of classes into which we will group our data values. 

In order to compare the two maps of population density values we will need the classes or buckets into which our data is grouped to be the same. One easy way to do this is to save a layer style based on this symbology.Save the style in your Mapping Data folder as DensityAlbersJenks5

![add](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData02/17_Style.png)

Next open the properties menu of US_county_1870_UTM10_PopJoin copy, load the layer style we just saved but change the column that is being symbolized to Dens_UTkm. 

**Save** your map project.

Toggle the two layers back and forth and note the areas of the US with the greatest change in population density. 

Create a new print composer with a legend, scale bar, and titles of the U.S. population density by county in 1870 calculated using the UTM Zone 10 projection. Export this as a PDF. Then repeat for the population density calculated using the Albers projection.

Because we have gone over the basics of using the print composer in Mapping Data 01 we will not go through these steps explicitly. (If you need a refresher on the major functions of the print composer refer to the detailed instructions in [Mapping Data 01](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/2_MappingData01.md)).

![add](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData02/PopulationbyCounty_Albers.pdf)

![add](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData02/PopulationbyCounty_UTM.pdf)


