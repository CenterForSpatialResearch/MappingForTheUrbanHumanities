###Analyzing Data 03: Schools, Libraries and Raster Analysis

###Premise
We will return to the analysis of schools and libraries we were conducting in Part One of this exercise however now we will now use raster analysis tools to answer similar questions through slightly different means and for the entirely of New York City. We want to know which parts of New York City have the greatest access to schools and libraries. We’ll answer this using a raster-based decision map.

###Notes on the data

### Topics/Steps

Open QGIS:
![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze31.png)

With the Add Vector Layer tool ![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze32.png), add the NYC_Libraries.shp and NYC_Schools.shp layers from the MappingForTheUrbanHumanities-master\Class_Data\3_AnalyzingData\Shape directory. 

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze33.png)

These point layers represent primary and secondary schools and public libraries throughout New York City. 
Since you will be conducting a raster based proximity analysis, you will first convert these point based features to a raster layer.  Under the raster layer, choose conversion>Rasterize.

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze34.png)

The rasterize window opens:

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze35.png)

First, you will convert the libraries to a raster format.  Since you are not mapping any attribute values, choose the “raster” field as the attribute value.  Choose NYC_Libraries as the input file.   Save the output as NYCLibraryRaster.tif in the shape directory for this exercise. You will have to choose a raster resolution for the output map.  Since the datasets are in state plane, with the units expressed in feet, it is intuitive to use the “raster resolution in map units per pixel” option.  Enter a resolution for 50 units (or feet) for both the horizontal and vertical options:

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze36.png)

There is one more step that you need to address before running the tool. For raster analysis you need to define the processing extent for the output file.  In essence, you need to tell the software what area to run the calculation for.  Otherwise, the tool would continue to run for the entire Earth!  By default, the rasterize tool will use the extent of the input file (NYC_Libraries).  This is not a good choice for two reasons.  First, you will want to make sure that your analysis will run for the entire city, even if those areas are outside the library extents.  Second, you want to be sure that all the rasters that you are using for this exercise have the identical extent and resolution. Thus, you must specify the processing extent.
Unfortunately, there are no automated methods to specify the processing extent in this toll.  You will need to specify it directly into the GDAL command line, the text box in the bottom on the tool. Click on the edit ![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze39.png)
button to edit the GDAL command line.  You can enter the processing extent in the line after “gdal_rasterize.”  You will use the “–te” statement to define the extent, this statement takes the form “-te xmin ymin xmax ymax” Enter the statement as follows: “-te 550000 600000 730000 770000”. Your window should look like this:

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze37.png)

The raster will add to the map.  It may look like a solid field, this is fine.  Each library location will appear as a single raster with avalue of one and they may be imperceptable at this extent.

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze38.png)

Run the rasterize tool again for the NYC_Schools Layer.  Choose NYC_Schools as the input file. Again, choose the “raster” field as the attribute value. Save the output as NYCSchoolRaster.tif in the shape directory for this exercise. You will have to choose a raster resolution for the output map.  Choose the “raster resolution in map units per pixel” and enter a resolution of 50 units for both the horizontal and vertical options.  Click on the edit![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze39.png) button to edit the GDAL command line and enter the statement “-te 550000 600000 730000 770000” after “gdal_rasterize”:

 ![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze310.png) 
 
 Click OK:
 
![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze311.png)
Next, you will create a proximity based raster layers representing the distances to libraries and schools. First, you will calculate distances to the nearest library.  
Under the raster menu, click on Analysis>Proximity:

![AnalyzingData]( https://git
Use NYCLibraryRaster as the input file and save the output file as NYCLibraryDistance.tif in the tutorial directory. Make sure to select “geo” for dist units:

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze313.png)

You should not need to specify the extent this time as the tool will automatically use the extent of the input file.  Click OK.

The resultant raster will represent the distance in feet to the nearest library:

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze314.png)
Next, you will calculate distances to the nearest school using the same process.  
Under the raster menu, click on Analysis>Proximity:

Use NYCSchoolRaster as the input file and save the output file as NYCSchoolDistance.tif in the tutorial directory. Make sure to select “geo” for dist units:

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze315.png)
Click OK: 


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze316.png)

Now you will generalize these proximity based rasters into discrete distance classes.  Specifically, you will classify the proximity based rasters into classes of 0-1/4 mile, ¼-½, mile, ½ - ¾ mile and above ¾ mile distances.

Unfortunately there are no simple to use tools for this in QGIS.  You will need to use one of the built in GRASS tools for this. Open the processing toolbar by choosing Toolbox under the processing menu:


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze317.png)


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze318.png)


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze319.png)


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze320.png)


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze321.png)


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze322.png)


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze323.png)


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze324.png)


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze325.png)


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze326.png)


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze327.png)


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze328.png)


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze329.png)


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze330.png)


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze331.png)


![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze332.png)

