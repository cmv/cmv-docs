# Geocoder

You can use the default ArcGIS [Class:Geocoder] (https://developers.arcgis.com/javascript/jsapi/geocoder-amd.html) or a custom geocoder
#### Example Config Object for default Geocoder
``` javascript
geocoder: {
    include: true,
    id: 'geocoder',
    type: 'domNode',
    path: 'esri/dijit/Geocoder',
    srcNodeRef: 'geocodeDijit',
    options: {
        map: true,
        mapRightClickMenu: true,
        geocoderOptions: {
          autoComplete: true,
          arcgisGeocoder: {
             placeholder: 'Enter an address or place'
          }
        }
    }
},
```
If the width of the search box for the geocoder widget is not wide enough you can alter `viewer\js\gis\dijit\Geocoder\css\Geocoder.css`

Try using (or altering) both of the width values below that will work for your implementation
``` css
.gis_GeocoderDijit .searchContainer {
    position: absolute;
    top: 0;
    left: 100%;
    width: 250px;
}
.gis_GeocoderDijit .esriGeocoderResults {
    display: none;
    z-index: 99;
    width: 279px;
    position: absolute;
    left: 0;
    top: 100%;
    margin: -3px 0 0 -31px;
    border: 1px solid #57585A;
    border-top: 0;
    padding: 0;
    background: #fff;
    -webkit-border-radius: 0 0 5px 5px;
    border-radius: 0 0 5px 5px;
}
```
#### Example Config Object for custom Geocoder
``` javascript
geocoder: {
    include: true,
    id: 'geocoder',
    type: 'domNode',
    path: 'gis/dijit/Geocoder',
    srcNodeRef: 'geocodeDijit',
    options: {
        map: true,
        mapRightClickMenu: true,
        geocoderOptions: {
            autoComplete: true,
            arcgisGeocoder: true, //if true a pick list showing your custom geocoder(s) below and the ESRI widget will appear for the end user to select
                zoomScale: 1000,
                placeholder: 'Search for an address',
                // name below will appear in widget pick list if arcgisGeocoder:true
                geocoders: [{ url: 'http://ServerName/arcgis/rest/services/GeocodeServiceName/GeocodeServer',
                      name: 'My Address Points'
               }]
        }
    }
},
```
