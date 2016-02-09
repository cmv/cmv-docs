# MapOptions Section of viewer.js

* set initial basemap, initial map center, zoom level, and sliderStyle. See [Map Constructor](https://developers.arcgis.com/javascript/jsapi/map-amd.html#map1) parameters for all of the options available.

* **Copyright Note For Your Map Services:** CMV uses the compact build of the ArcGIS JavaScript API. This effects the `showAttribution:` option where the compact build sets it to `false` by default. The result is that your copyright information will not be displayed on the map. In `mapOptions:{}` add `showAttribution: true` to override the default setting when using the compact build of the API. See the three examples below on how to use `showAttribution:` if you need to display a copyright with your map services.

* If you want to have the large zoom slider in your map like this `sliderStyle: 'large'`, you will need to use the full build of the JavaScript API,  CMV uses the compact build by default.

## Example: mapOptions using a basemap from ArcGIS Online:
``` javascript
mapOptions: {
   basemap: 'streets',
   center: [-98, 40],
   zoom: 5,
   sliderStyle: 'small',
   showAttribution: true
}
```
## Example: mapOptions using a custom basemap:
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

## Manually setting the levels of detail (LODs)
If you want to zoom in beyond the default levels of detail provided by your map services, you can manually set them by adding the "lods" property to your mapOptions object.
```javascript
mapOptions: {
    basemap: 'streets',
    center: [-96.59179687497497, 39.09596293629694],
    zoom: 5,
    sliderStyle: 'small',
    lods: [
        {
            'level'     : 0,
            'resolution': 156543.03392800014,
            'scale'     : 591657527.591555
        },
        {
            'level'     : 1,
            'resolution': 78271.51696399994,
            'scale'     : 295828763.795777
        },
        {
            'level'     : 2,
            'resolution': 39135.75848200009,
            'scale'     : 147914381.897889
        },
        {
            'level'     : 3,
            'resolution': 19567.87924099992,
            'scale'     : 73957190.948944
        },
        {
            'level'     : 4,
            'resolution': 9783.93962049996,
            'scale'     : 36978595.474472
        },
        {
            'level'     : 5,
            'resolution': 4891.96981024998,
            'scale'     : 18489297.737236
        },
        {
            'level'     : 6,
            'resolution': 2445.98490512499,
            'scale'     : 9244648.868618
        },
        {
            'level'     : 7,
            'resolution': 1222.992452562495,
            'scale'     : 4622324.434309
        },
        {
            'level'     : 8,
            'resolution': 611.4962262813797,
            'scale'     : 2311162.217155
        },
        {
            'level'     : 9,
            'resolution': 305.74811314055756,
            'scale'     : 1155581.108577
        },
        {
            'level'     : 10,
            'resolution': 152.87405657041106,
            'scale'     : 577790.554289
        },
        {
            'level'     : 11,
            'resolution': 76.43702828507324,
            'scale'     : 288895.277144
        },
        {
            'level'     : 12,
            'resolution': 38.21851414253662,
            'scale'     : 144447.638572
        },
        {
            'level'     : 13,
            'resolution': 19.10925707126831,
            'scale'     : 72223.819286
        },
        {
            'level'     : 14,
            'resolution': 9.554628535634155,
            'scale'     : 36111.909643
        },
        {
            'level'     : 15,
            'resolution': 4.77731426794937,
            'scale'     : 18055.954822
        },
        {
            'level'     : 16,
            'resolution': 2.388657133974685,
            'scale'     : 9027.977411
        },
        {
            'level'     : 17,
            'resolution': 1.1943285668550503,
            'scale'     : 4513.988705
        },
        {
            'level'     : 18,
            'resolution': 0.5971642835598172,
            'scale'     : 2256.994353
        },
        {
            'level'     : 19,
            'resolution': 0.29858214164761665,
            'scale'     : 1128.497176
        },
        {
            'level'     : 20,
            'resolution': 0.14929107082380833,
            'scale'     : 564.248588
        },
        {
            'level'     : 21,
            'resolution': 0.07464553541190416,
            'scale'     : 282.124294
        }
    ]
},
```

## Important Chrome Browser Tweak
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
