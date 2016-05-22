##Making Data 03

###Geocoding Exercise

In this exercise you are going to map locations related to music in the borough of the Bronx by geocoding – converting tabular data into spatial mapping files. First, you will take geographic coordinates and display them visually.  Then you will take a list of street addresses and locate them by using a geolocation service, matching up the addresses against a database of locations. 
First, you will find businesses in the music industry located throughout the Bronx.  You are going to use the ReferenceUSA business directory to identify these businesses.  ReferenceUSA is a comprehensive database of business locations throughout the US.  Columbia Libraries maintains a subscription to this service. 

Go to the CU Libraries’ homepage and search for “ReferenceUSA” in the quicksearch bar:
![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode1.png)

The first result should provide a link to ReferenceUSA:
![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode2.png)

Open the database and click on the “U.S. Businesses/ Employers” database: 
![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode3.png)

Click on the advanced search tab.  Here, you have a variety of tools to limit the business search.  First you will limit by geography.  Check “county” in the geography list and select “New York.”  Add “Bronx, NY” to the search selections: 
![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode4.png)

Next, you will search by business type.  Choose the “Keyword/SIC/NACIS” option under business type. Select “search all NACIS” (a business classification system created by the census department).  All of the businesses in the directory will have at least one of these classifications.  You can search for classification entries by keyword and add them to your search limits.  Below I have added all of the NACIS classifications including the terms “Musical,” “Music,” and “Sound.”  When I click on “Update Count” on the right it finds 129 entries:
![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode5.png)

You may opt to use a somewhat different list of classifications, but if so, try not to use a search that finds more than 200 results as there are some limitations to how many results ReferenceUSA allows to be downloaded at once.  Once finished click on “View Results”:
![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode6.png)

The results screen only shows 25 results per page.  To download all results, you will have to check each entry. You can select the whole page by using the topmost selection box by “company name,” but you will have to toggle thorough all 6 pages to do them all:
![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode7.png)

Once all the businesses have been selected, click on “download.”  Select comma delimited as the file format.  Under level of detail select “custom,” ReferenceUSA provides a wealth of detail for each business, actually too much for our purposes, so you will select the attributes manually. You should be given the company name and address information by default, be sure to add the “latitude” and “longitude” fields at a minimum: 
![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode8.png)

Feel free to add any more attributes that interest you.  Once finished, download the file.  Save it as MusicBusinessesBronx.csv in your project directory.  If you open it, you can see that the results should be very clean, with delimited address fields and coordinates in decimal degrees: 
![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode9.png)

Next, open QGIS: 
![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode10.png)

You are once again going to use OpenStreetMap as our reference data for the geocoding process.   You can access the OpenStreetMap service through the MMQGIS plugin.  This plugin does not come pre-installed with QGIS, so you will likely need to install it.  Under the plugins menu, select  “Manage and Install Plugins…” 
![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode11.png)

The plugins dialog opens.  Search for “MMQGIS”, highlight it, and click “Install plugin”: 
![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode12.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode13.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode14.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode15.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode16.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode17.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode18.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode19.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode20.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode21.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode22.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode23.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode24.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode25.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode26.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode27.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode28.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode29.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode30.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode31.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode32.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode33.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode34.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode35.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode36.png)

![GeocodingExercise](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MakingData02/Geocode37.png)
