# MapOptions Section of viewer.js

* set initial basemap, initial map center, zoom level, and sliderStyle. See [Map Constructor](https://developers.arcgis.com/javascript/jsapi/map-amd.html#map1) parameters for all of the options available.

* **Copyright Note For Your Map Services:** CMV uses the compact build of the ArcGIS JavaScript API. This effects the `showAttribution:` option where the compact build sets it to `false` by default. The result is that your copyright information will not be displayed on the map. In `mapOptions:{}` add `showAttribution: true` to override the default setting when using the compact build of the API. See the three examples below on how to use `showAttribution:` if you need to display a copyright with your map services.

#### Example: mapOptions using a basemap from ArcGIS Online:
``` javascript
mapOptions: {
   basemap: 'streets',
   center: [-98, 40],
   zoom: 5,
   sliderStyle: 'small',
   showAttribution: true
}
```
#### Example: mapOptions using a custom basemap:
In the `define()` add references to `'esri/dijit/Basemap'`, `'esri/dijit/BasemapLayer'` and `'esri/geometry/Point'`
``` javascript
mapOptions: {
   basemap: new Basemap({
        id: 'basemap1',
        layers: [new BasemapLayer({
        url: 'http://ServerName/arcgis/rest/services/BaseMapName/MapServer'
        })]
    }),
    center: new Point({
        x: 6356023.515330248,
        y: 1917313.443425702,
        spatialReference: {
            wkid: 102642
        }
    }),
    zoom: 5,
    sliderStyle: 'small',
    showAttribution: true
}
```

#### Important Chrome Browser Tweak
If you notice or experience the map or the application flashing while zooming in & out, or panning here is a workaround.

In ``` config/viewer.js ``` under Map Options add ```navigationMode: 'classic'```

Example
```javascript
mapOptions: {
   navigationMode: 'classic',
   center: [-84.138794, 39.055701],
   zoom: 11,
   sliderStyle: 'small',
   showAttribution: true
}
```
Here is a [link](https://developers.arcgis.com/javascript/jsapi/map-amd.html#navigationmode) to the ArcGIS Javascript API docs for a more detailed explanation.
 
