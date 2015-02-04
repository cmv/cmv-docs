# Basemaps

#### Example configuration to use custom basemaps displayed in the Basemap Gallery

`config/basemaps.js`

``` javascript
define([
    'esri/dijit/Basemap',
    'esri/dijit/BasemapLayer'
    'esri/layers/osm'
], function (Basemap, BasemapLayer, osm) {
    return {
        map: true,
        mode: 'custom', //must be either 'agol' or 'custom'
        title: 'Basemaps',
        // use this as the start basemap when application first opens
        mapStartBasemap: 'BaseMap1',
        //this is the list of basemaps to show in the BaseMap Gallery.
        basemapsToShow: ['BaseMap1', 'BaseMap2','BaseMap3'],  
        basemaps: {
            BaseMap1: {
                title: 'My First Basemap', //appears as basemap title in Gallery
                basemap: new Basemap({
                    id: 'basemap1',
                    layers: [new BasemapLayer({
                        url: 'http://ServerName/arcgis/rest/services/BaseMapName/MapServer'
                    })]
                })
            },
            BaseMap2: {
                title: 'My Second Basemap', //appears as basemap title in Gallery
                basemap: new Basemap({
                    id: 'basemap2',
                    layers: [new BasemapLayer({
                        url: 'http://ServerName/arcgis/rest/services/BaseMapName/MapServer'
                    })]
                })
            },
            BaseMap3: {
                title: 'My Third Basemap', //appears as basemap title in Gallery
                basemap: new Basemap({
                    id: 'basemap3',
                    layers: [new BasemapLayer({
                        url: 'http://ServerName/arcgis/rest/services/BaseMapName/MapServer'
                    })]
                })
            }
        }
    };
});
```