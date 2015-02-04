# Viewer configuration file
The file can be found here `\viewer\js\config\viewer.js` Use this file to configure CMV and "Make it your own".

### esriConfig Section
Set esri config options you may need such as proxy


### Set Page Title, Header and Subheader
You can modify `viewer/js/config/viewer.js` to override the default settings in `viewer/index.html` 

In `return{}` add 
``` javascript
titles: {header: 'Yours', subHeader: 'Mine!', pageTitle: 'Ours'},
```
This offers flexibility if you want to deploy more than one CMV on your site by using a url to call different configs within different `viewer.js` files. For example http://YourServerName/viewer/?config=viewer2 to load a separate config file in config folder or to a completely different folder http://YourServerName/viewer/?config=./js/newconfig/viewer.js

### Default Map Click Mode

### Map Options
* set initial basemap, initial map center, zoom level, and sliderStyle. See [Map Constructor](https://developers.arcgis.com/javascript/jsapi/map-amd.html#map1) parameters for all of the options available.
* **Copyright Note For Your Map Services:** CMV uses the compact build of the ArcGIS JavaScript API. This effects the `showAttribution:` option where the compact build sets it to `false` by default. The result is that your copyright information will not be displayed on the map. In `mapOptions:{}` add `showAttribution: true` to override the default setting when using the compact build of the API. See the three examples below on how to use `showAttribution:` if you need to display a copyright with your map services.

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

## Operational layers Section
Layers to load on top of the basemap. See [Class: Layer] (https://developers.arcgis.com/javascript/jsapi/layer-amd.html) for more information on types of layers and [Layer options] (https://developers.arcgis.com/javascript/jsapi/layer-amd.html#layer1).
### Example
See [operational layers section in viewer.js] (https://github.com/cmv/cmv-app/blob/master/viewer/js/config/viewer.js#L63) for examples.

The following list indicates tested and untested layers that can be used in CMV
* `type: csv // 'CSV'`
* `type: dynamic // 'ArcGISDynamicMapService'`
* `type: feature // 'Feature'`
* `type: georss // 'GeoRSS'`
* `type: image // 'ArcGISImageService'`
* `type: kml // 'KML'`
* `type: label // 'Label', untested`
* `type: mapimage // 'MapImage', untested`
* `type: osm // 'OpenStreetMap'`
* `type: tiled // 'ArcGISTiledMapService'`
* `type: wms // 'WMS'`
* `type: wmts // 'WMTS', untested`

---
## Widget section
Widgets can have the following properties:
```javascript
{
    //load this widget definition
	include: true,
	
	//can be: floating, titlePane, contentPane, map, domNode, invisible
	type: 'titlePane',
       // titlePane type can undock from sidebar allowing user to position widget within browser 
        canFloat: true
      
       //if titlePane type, additional pane locations are available: top, right, bottom
       //uncomment panes:{} section
       placeAt: 'right'

	//class file path to the widget
	path: 'gis/dijit/Print',
	
	//id for widget must be unique
	id: 'print',
	
	//title for widget, will be used in titlePane and floating 
	title: 'Print',
	
	//if titlePane, will be open or closed by default
	open: false,
	
	//if titlePane type, the order in the sidebar when application is first opened
	position: 5,
	
	//the dom node id to place the widget in for type domNode
	srcNodeRef: 'nodeId',
	
	//options object will be passed into the widget class on creation
	options: {
	
		//if you need a map reference true, if not false
		map: true,
		
		// if you need the map click mode object
		mapClickMode: true,
		
		// if you need the legend layer array
		legendLayerInfos: true,
		
		// if you need the toc layer array
		tocLayerInfos: true, 

		// if you need the edit layer array
		editorLayerInfos: true,
		
		// any other property:value to pass into widget that you may need
		property: 'value'
	}
}
```
---
## Widgets:

### basemaps
You can choose to display the basemap widget in the application by setting `include: true` in `config\viewer.js`. To set the list of basemaps to appear in the widget modify `config\basemap.js`

More details about the basemap widget can be found [here](Configuration-file-basemaps.js).
***



### bookmarks
A Bookmark represents individual spatial locations of a geographic area. You can use bookmarks to highlight areas on your map you want the user to quickly see. A predefined list of bookmarks can appear in the widget or you may allow the user to add their own bookmarks. Modify `\config\bookmark.js` to create a predefined list for the user. In 'config\viewer.js' you can choose to display the widget as well set the option to allow the user to edit bookmarks.

***


### directions
Optimize order checkbox appears for end user after 4 or more stops are created
#### Example Config Object
``` javascript
directions: {
	include: true,
	id: 'directions',
	type: 'titlePane',
	path: 'gis/dijit/Directions',
	title: 'Directions',
	open: false,
	position: 7,
	options: {
		map: true,
		options: {
                        routeTaskUrl: http://sampleserver3.arcgisonline.com/ArcGIS/rest/services/Network/USA/NAServer/Route',
			routeParams: {
				directionsLanguage: 'en-US',
				directionsLengthUnits: units.MILES
			}
		}
	}
},
```

---
### draw
#### Example Config Object
``` javascript
draw: {
	include: true,
	id: 'draw',
	type: 'titlePane',
	path: 'gis/dijit/Draw',
	title: 'Draw',
	open: false,
	position: 4,
	options: {
		map: true,
		mapClickMode: true
	}
},
```

---
### editor
#### Example Config Object
``` javascript
editor: {
	include: true,
	id: 'editor',
	type: 'titlePane',
	path: 'gis/dijit/Editor',
	title: 'Editor',
	open: false,
	position: 8,
	options: {
		map: true,
		mapClickMode: true,
		editorLayerInfos: true,
		settings: {
			toolbarVisible: true,
			showAttributesOnClick: true,
			enableUndoRedo: true,
			createOptions: {
				polygonDrawTools: ['freehandpolygon', 'autocomplete']
			},
			toolbarOptions: {
				reshapeVisible: true,
				cutVisible: true,
				mergeVisible: true
			}
		}
	}
},
```

---
### find
The search can be conducted on:
* a single field of a single layer
* many fields of a layer
* or on many fields of many layers

Modify `\config\find.js` to query layers.

More details about the find widget can be found [here](https://github.com/cmv/cmv-app/wiki/Widget-find.js).

---
### geocoder
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
---
### growler
#### Example Config Object
``` javascript
growler: {
	include: true,
	id: 'growler',
	type: 'domNode',
	path: 'gis/dijit/Growler',
	srcNodeRef: 'growlerDijit',
	options: {}
},
```

---
### homeButton
#### Example Config Object
``` javascript
homeButton: {
	include: true,
	id: 'homeButton',
	type: 'domNode',
	path: 'esri/dijit/HomeButton',
	srcNodeRef: 'homeButton',
	options: {
		map: true,
		extent: new Extent({
			xmin: -180,
			ymin: -85,
			xmax: 180,
			ymax: 85,
			spatialReference: {
				wkid: 4326
			}
		})
	}
},
```

---
### identify
Modify `\config\identify.js' if you want a utilize [PopupTemplate] (https://developers.arcgis.com/javascript/jsapi/popuptemplate-amd.html)
#### Example Config Object
``` javascript
identify: {
   include: true,
   id: 'identify',
   type: 'invisible',
   path: 'gis/dijit/Identify',
   options: 'config/identify'
			},
```

---
### legend
#### Example Config Object
``` javascript
legend: {
	include: true,
	id: 'legend',
	type: 'titlePane',
	path: 'esri/dijit/Legend',
	title: 'Legend',
	open: false,
	position: 0,
	options: {
		map: true,
		legendLayerInfos: true
	}
},
```

---
### locateButton
This widget is a wrapper around [LocateButton] (https://developers.arcgis.com/javascript/jsapi/locatebutton-amd.html).
Centers map to user's location. You can suppress GPS data that will appear in a [InfoTemplate] (https://developers.arcgis.com/javascript/jsapi/infotemplate-amd.html)
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
---
### measure
#### Example Config Object
``` javascript
measure: {
	include: true,
	id: 'measurement',
	type: 'titlePane',
	path: 'gis/dijit/Measurement',
	title: 'Measurement',
	open: false,
	position: 5,
	options: {
		map: true,
		mapClickMode: true,
		defaultAreaUnit: units.SQUARE_MILES,
		defaultLengthUnit: units.MILES
	}
},
```

---
### overviewMap
#### Example Config Object
``` javascript
overviewMap: {
	include: true,
	id: 'overviewMap',
	type: 'map',
	path: 'esri/dijit/OverviewMap',
	options: {
		map: true,
               // location overview map will appear on Map object 
		attachTo: 'bottom-right',
		color: '#0000CC',
		height: 100,
		width: 125,
		opacity: 0.30,
		visible: false
	}
},
```

---
### print
#### Example Config Object
``` javascript
print: {
	include: true,
	id: 'print',
	type: 'titlePane',
	path: 'gis/dijit/Print',
	title: 'Print',
	open: false,
	position: 6,
	options: {
		map: true,
		printTaskURL: 'http://sampleserver6.arcgisonline.com/arcgis/rest/services/Utilities/PrintingTools/GPServer/Export%20Web%20Map%20Task',
		copyrightText: 'Copyright 2014',
		authorText: 'Me',
		defaultTitle: 'Viewer Map',
		defaultFormat: 'PDF',
		defaultLayout: 'Letter ANSI A Landscape'
	}
},
```

---
### scalebar
See [Class : Scalebar] (https://developers.arcgis.com/javascript/jsapi/scalebar-amd.html) for parameters
#### Example Config Object
``` javascript
scalebar: {
	include: true,
	id: 'scalebar',
	type: 'map',
	path: 'esri/dijit/Scalebar',
	options: {
		map: true,
		attachTo: 'bottom-left',
		scalebarStyle: 'line',
		scalebarUnit: 'dual'
	}
},
```

---
### streetview
#### Example Config Object
``` javascript
streetview: {
	include: true,
	id: 'streetview',
	type: 'floating',
	path: 'gis/dijit/StreetView',
	title: 'Google Street View',
	options: {
		map: true,
		mapClickMode: true,
		openOnStartup: true
	}
}
```

---
### TOC
The TOC widget was replaced by the LayerControl widget at v1.3.0 but is still available. However it may be deprecated in a future CMV release.
#### Example Config Object
``` javascript
TOC: {
	include: true,
	id: 'toc',
	type: 'titlePane',
	path: 'gis/dijit/TOC',
	title: 'Layers',
	open: false,
	position: 1,
	options: {
		map: true,
		tocLayerInfos: true
	}
},
```
---