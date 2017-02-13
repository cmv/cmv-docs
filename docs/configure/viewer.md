# Viewer.js configuration file
Use this file to configure CMV and "Make it your own".

The following sections are contained within the viewer.js configuration file.

#### [Header Section](./header.md)

Various Config and Preloading Scripts

#### Config Definition

The config definition is a plain javascript object that accepts the following properties:

 Key | Type | Description
 ----|------|------------
 `isDebug` | `Boolean` | Used to enable "debug mode" in cmv
 `defaultMapClickMode` | `String` | Sets a default "map click mode" in cmv. Values allowed can vary by what widgets are included. For example, the identify widget uses the map click mode `identify`. If the map click mode is not set to `identify`, the widget will not be activated by default.
 `mapOptions` | `Object` | See [Map Options](./mapOptions.md)
 `titles` | `Object` | See [Titles](./titles.md)
 `panes` | `Object` | See [Panes](./panes.md)
 `webMapId` | `String` | The web map ID to use from ArcGIS Online, example: `'ef9c7fbda731474d98647bebb4b33c20'`
 `webMapOptions` | `Object` | See [Web Map Options](https://developers.arcgis.com/javascript/3/jsapi/esri.arcgis.utils-amd.html)
 `layerTypes` | `Object<String, String>` | A simple object that allows you to use new layer types in CMV. The key is a string that corresponds to the layers `type` referenced in the cmv operational layers and the value is the path to the custom layer module.
 `widgetTypes` | `Object<String, String>` | Similar to `layerTypes` but lets you use new widget types in CMV other than the default `'titlePane'`, etc.
 `operationalLayers` | `Array<Object>` | See [Operational Layers](./operationalLayers.md)
 `widgets` | `Object` | See [Widgets](./widgets.md)
