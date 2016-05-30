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

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze37.png)

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze38.png)

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze39.png)

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze310.png)

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze311.png)

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze312.png)

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze313.png)

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze314.png)

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze315.png)

![AnalyzingData]( https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/AnalyzingData03/Analyze316.png)


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

