# Locate Button

This widget is a wrapper around [LocateButton](https://developers.arcgis.com/javascript/jsapi/locatebutton-amd.html).
Centers map to user's location. You can suppress GPS data that will appear in a [InfoTemplate](https://developers.arcgis.com/javascript/jsapi/infotemplate-amd.html)

#### Example Config Object
``` javascript
locateButton: {
   include: true,
   id: 'locateButton',
   type: 'domNode',
   path: 'gis/dijit/LocateButton',
   srcNodeRef: 'locateButton',
   options: {
      map: true,
      scale: 2400 /* https://developers.arcgis.com/javascript/jsapi/locatebutton-amd.html#scale */
      // show GPS data in a InfoTemplate
      publishGPSPosition: true,
      highlightLocation: true,
      // move map when new GPS location is obtained
      useTracking: true,
      // uncomment the next block if you want the user's location to appear on the map when app loads
      // end-user may have to allow permissions within the browser to interact with app's location request
      /*startup: function(){
            this.locate();
      },*/
      geolocationOptions: {
         maximumAge: 0,
         timeout: 15000,
         enableHighAccuracy: true
      }
   }
}
```
