# StreetView

### Host Your Own Projection File
If desired, you can load a projection file from your own server instead of using one from spatialreference.org 
i.e., http://YourServer/projections/102642.js. 

This is necessary if your server cannot access external sites. 

The following steps will guide you:
 
1. Go to http://spatialreference.org/
2. Browse the reference you need, for example ESRI, http://spatialreference.org/ref/esri/
3. Search for your WKID, for example 102660, http://spatialreference.org/ref/esri/?search=102660&srtext=Search
4. Click on the result you require, for the above search the result is http://spatialreference.org/ref/esri/102660/
5. Click the Proj4js Format link, http://spatialreference.org/ref/esri/102660/proj4js/
6. Save the file in *.js format on your server
7. Modify the line in `viewer/js/gis/dijit/StreetView.js` where `proj4CustomURL:null,`
8. Enter your site address and the location of the file you saved above, `proj4CustomURL: 'http://YourServer/projections/102660.js',`