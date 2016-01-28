This file comes with the standard ESRI basemaps already configured to work with the application. Should you want to use your own custom basemaps or mash them up with ESRI basemaps there are a couple of ways to do this.

## What Options Are Available?
1. In an effort to not duplicate documentation it is strongly recommended you become familiar with the ArcGIS API for Javascript.

2. To understand the different parameters or options available to you.

 a) For further customizing your Basemap please refer to  the [ArcGIS API for Javascript -- Basemap](https://developers.arcgis.com/javascript/jsapi/basemap-amd.html).

 b) For further customizing your BasemapLayer please refer to the [ArcGIS API for Javascript -- BasemapLayer](https://developers.arcgis.com/javascript/jsapi/basemaplayer-amd.html).

## Getting Started with custom basemaps
1. In the file `\viewer\js\config\basemaps.js` change `mode: 'agol',` to `mode: 'custom',`

2. Block Comment the preconfigured AGOL basemaps so you can use your custom basemaps.
``` javascript
/*streets: {
      title: 'Streets'
  },
  satellite: {
      title: 'Satellite'
  },
  hybrid: {
      title: 'Hybrid'
  },
  topo: {
      title: 'Topo'
  },
  gray: {
      title: 'Gray'
  },
  oceans: {
      title: 'Oceans'
  },
  'national-geographic': {
      title: 'Nat Geo'
  },
  osm: {
      title: 'Open Street Map'
  }
*/
```
3. **It is recommended when getting started to not delete code right away. By commenting the code you have something you can refer back to.**

##  Implementing your custom basemaps
1. Remove the Block Comment in the example section of `\viewer\js\config\basemaps.js` for custom basemaps.
``` javascript
// examples of custom basemaps

            streets: {


                title: 'Streets',
                basemap: new Basemap({
                    id: 'streets',
                    layers: [new BasemapLayer({
                        url: 'http://services.arcgisonline.com/ArcGIS/rest/services/World_Street_Map/MapServer'
                    })]
                })
            },
            satellite: {
                title: 'Satellite',
                basemap: new Basemap({
                    id: 'satellite',
                    layers: [new BasemapLayer({
                        url: 'http://services.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer'
                    })]
                })
            },
            hybrid: {
                title: 'Hybrid',
                basemap: new Basemap({
                    id: 'hybrid',
                    layers: [new BasemapLayer({
                        url: 'http://services.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer'
                    }), new BasemapLayer({
                        url: 'http://services.arcgisonline.com/ArcGIS/rest/services/Reference/World_Boundaries_and_Places/MapServer',
                        isReference: true,
                        displayLevels: [0, 1, 2, 3, 4, 5, 6, 7]
                    }), new BasemapLayer({
                        url: 'http://services.arcgisonline.com/ArcGIS/rest/services/Reference/World_Transportation/MapServer',
                        isReference: true,
                        displayLevels: [8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19]
                    })]
                })
            },
            lightGray: {
                title: 'Light Gray Canvas',
                basemap: new Basemap({
                    id: 'lightGray',
                    layers: [new BasemapLayer({
                        url: 'http://services.arcgisonline.com/ArcGIS/rest/services/Canvas/World_Light_Gray_Base/MapServer'
                    }), new BasemapLayer({
                        url: 'http://services.arcgisonline.com/ArcGIS/rest/services/Canvas/World_Light_Gray_Reference/MapServer',
                        isReference: true
                    })]
                })
            }
```
2. Replace `title:` and `id:` and `url:` as necessary to match the custom basemaps array you want to display.
 a) Special note about the basemap function name - Notice this name matches a string in the `basemapToShow:[]`. This is important because the name given to the function must correspond to a name in the array. For example;

```javascript
streets: {
    title: 'Streets',
    basemap: new Basemap({
        id: 'streets',
        layers: [new BasemapLayer({
            url: 'http://services.arcgisonline.com/ArcGIS/rest/services/World_Street_Map/MapServer'
        })]
    })
},
```

**Note:** If you were to change the function name from `streets:{}` to `streetscustom:{}` then you would also need to add or change the name in the `basemapsToShow:[]` array to match the name of your function. An example of how this might be done is below.

### Example configuration to use custom basemaps displayed in the Basemap Gallery

```javascript
// at CMV version 1.3.0 the three defines below are included and commented out.
// uncomment each define to use custom basemaps
// at CMV v1.2.0 you will need to add the following in define([], and in function()
define([
    'esri/dijit/Basemap',
    'esri/dijit/BasemapLayer',
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

## Advanced Topics

1. The first BasemapLayer added in a Basemap will define the scales or levels of detail.

2. To mashup multiple tiled services the scales or levels of detail from both services must be the same.

3. If your tiled services have scales or levels of detail that go in beyond the Esri scales, you can still take advantage of those scales but continue using Esri basemap services albeit with a little more customization.


### Zooming in beyond Esri default scales or levels of detail.

**There might be multiple ways to do this so if there are other examples please share. But here is one example.**

* Create a map service and enable caching using your scales, but choose the option to generate tiles manually.

* This will publish a service with your scales or levels of detail. While it appears like a cache service     there was no time spent creating the tiles. It is merely being used to define your scales or levels of detail.

* In this example, the service defining scales or levels of detail is called **LODS**. Notice it is the first service defined in Basemap as a BasemapLayer. Therefore the streets Basemap should assume the scales or levels of detail of the **LODS** service. Although we still need to make some other customizations.

```javascript

//basemaps.js
 streets: {
    title: 'Clermont County Streets',
    basemap: new Basemap({
        id: 'streets',
        layers: [new BasemapLayer({
            url: 'http://maps.clermontauditor.org/arcgis/rest/services/WMAS/LODS/MapServer'
        }), new BasemapLayer({
            url: 'http://services.arcgisonline.com/ArcGIS/rest/services/World_Street_Map/MapServer'
        }), new BasemapLayer({
            url: 'http://maps.clermontauditor.org/arcgis/rest/services/WMAS/Streetmap/MapServer'
        })]
    })
},
```

* By design the template is built to work with Esri basemaps. So the first basemap which gets loaded in the ``` viewer.js ``` file is **streets**. So even if you follow the above steps in ``` basemaps.js ``` the scales will not be honored until some customizations are made to **viewer.js**.

* Around line 23 look for the block of code below. This is what you will need to customize so your scales or levels of detail will be honored when the application loads.

```javascript
// viewer.js

mapOptions: {
  	basemap: 'streets',
  	center: [-96.59179687497497, 39.09596293629694],
  	zoom: 5,
  	sliderStyle: 'small'
},
```

* You will need to create a Basemap and add a BasemapLayer which references your scales.

  * You must define or add 2 references for this example ```'esri/dijit/Basemap'``` & ```'esri/dijit/BasemapLayer'```

  * Your define statement might look like the code below, around line 7 ``` viewer.js```

```javascript
define(['esri/InfoTemplate',
        'esri/units',
        'esri/geometry/Extent',
        'esri/config',
        'esri/tasks/GeometryService',
        'esri/dijit/Basemap',
        'esri/dijit/BasemapLayer'],
```

  * Next add references in your function, around line 14 ``` viewer.js```

```javascript
function (a, b, c, d, e, Basemap, BasemapLayer) {
```

  * Next create your basemap as shown below, around line 18 ``` viewer.js```

```javascript
 mapOptions: {
                    basemap: new Basemap({
                        layers: [new BasemapLayer({
                            url: 'http://maps.clermontauditor.org/arcgis/rest/services/WMAS/LODS/MapServer'
                        })]
                    }),
                    center: [-84.138794, 39.055701],
                    zoom: 11,
                    sliderStyle: 'small'
                },
```

  * The above code will ensure the application assumes your scales or level of detail when it loads.

  * You might notice the map looks blank when the application initially loads because the service being loaded  was an empty cache. Once the application assumes the scales it will then load your custom basemaps.
