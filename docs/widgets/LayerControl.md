# Layer Control

A layer control widget for CMV. Just don't call it a TOC.

## Features

- Toggle layer visibility
- Layer menu with Zoom To Layer, Transparency and Layer Swipe
- Capabilities to create custom dynamic sublayer menus
- Legends for ArcGIS layers
- Sublayer/folder structure and toggling for ArcGIS dynamic layers

  - can be disabled
  - single layer map services display legend in expand area

- Layer reordering in map and LayerControl widget

- Separate vector and overlay layers (required for layer reordering)

- Support for several layer types:

  - dynamic
  - feature
  - tiled
  - image

## LayerControl in CMV

LayerControl can be easily loaded with CMV's widget loader. CMV creates an array with a `LayerInfo` object for each layer with parameters and options specific to the layer and its associated Control. `layerControlLayerInfos: true` tells the widget loader to include the `LayerInfos` array. LayerControl can also be used in your widget. See below for more Class information.

```javascript
layerControl: {
    include: true,
    id: 'layerControl',
    type: 'titlePane',
    path: 'gis/dijit/LayerControl',
    title: 'Layers',
    open: true,
    position: 0,
    options: {
        map: true, //required
        layerControlLayerInfos: true //required
    }
}
```

## Widget Options

Parameter           | Type    | Description
------------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
`map`               | Object  | Set to `true` in CMV to pass the map. `esri/map` instance. Required.
`layerInfos`        | Array   | Set `layerContrlLayerInfos: true` in CMV to pass the layer infos array. Array of `LayerInfos`. Required. See LayerInfos.
`separated`         | Boolean | Separate vector and overlay layer types. Required for `vectorReorder`, `vectorLabel`, `overlayReorder` and `overlayLabel`. Default is `false`.
`vectorReorder`     | Boolean | Enable reordering of vector layers in map and Layer Control. Default is `false`.
`vectorLabel`       | Mixed   | Label for vector layers. Default is `false`. Pass the label or html for quick easy custom styling of label text.
`overlayReorder`    | Boolean | Enable reordering of overlay layers in map and Layer Control. Default is `false`.
`overlayLabel`      | Mixed   | Label for overlay layers. Default is `false`. Pass the label or html for quick easy custom styling of label text.
`noLegend`          | Boolean | When `true` no legend is created for all layers. Can be overridden for specific layer(s) with `noLegend` layer option.
`noZoom`            | Boolean | When`true`removes "Zoom to Layer" menu item for all layers. Can be overridden for specific layer(s) with`noZoom` layer option.
`noTransparency`    | Boolean | When `true` removes "Transparency" menu item for all layers. Can be overridden for specific layer(s) with `noTransparency` layer option.
`swipe`             | Boolean | When `true` adds "Layer Swipe" menu item for all layers. Can be overridden for specific layer(s) with `swipe` layer option.
`swiperButtonStyle` | String  | CSS for positioning "Exit Layer Swipe" button in the map. Must include `position:absolute;` and a `z-index`. Default is `position:absolute;top:20px;left:120px;z-index:50;`.
`menu`              | Object  | An object consisting of a key value pairs where they key is a layer type and the value is an array of menu items
`subLayerMenu`      | Object  | An object consisting of a key value pairs where they key is a layer type and the value is an array of menu items

Each layer has its own Control widget in LayerControl. Additional Control specific options can be specified with `layerControlLayerInfos`. See [Layer Control Options below](#layer-control-options). The similarity/difference in names is a bit confusing. A future release of CMV will use a different system for widgets to obtain layer options. Not only will core widgets like LayerControl and Identify no longer need a tie in with CMV's Controller class, developers will be able to specify custom options objects through CMV's layer loader for use with their own widgets.

**CMV Dynamic Layer Example**

```javascript
{
    type: 'dynamic',
    url: 'http://sampleserver1.arcgisonline.com/ArcGIS/rest/services/PublicSafety/PublicSafetyOperationalLayers/MapServer',
    title: 'Louisville Public Safety',
    options: {},
    layerControlLayerInfos: {

        // layer control options
        sublayers: false,
        noTransparency: true
    }
}
```

**CMV Feature Layer Example**

```javascript
{
    type: 'feature',
    url: 'http://services1.arcgis.com/g2TonOxuRkIqSOFx/arcgis/rest/services/MeetUpHomeTowns/FeatureServer/0',
    title: 'STLJS Meetup Home Towns',
    options: {},
    layerControlLayerInfos: {

        // layer control options
        noLegend: true,
        noZoom: true
    }
}
```

## Layer Control Options

All layer types have common options while some options are specific to certain layer types. In CMV, these options are passed using the `layerControlLayerInfos` object.

Option               | Type    | Description                                                                                                                                                                                                    | Affects
-------------------- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------
`exclude`            | Boolean | When `true` a layer control will not be added to the widget. Using `exclude` for a layer with layer reordering enabled which is not above or below all included layers will result in layer reordering issues. | all types
`noLegend`           | Boolean | When `true` no legend is created. Set to `false` to override `noLegend: true` widget parameter.                                                                                                                | dynamic, feature and tiled
`noZoom`             | Boolean | When `true` removes "Zoom to Layer" menu item. Set to `false` to override `noZoom: true` widget parameter.                                                                                                     | all types
`noTransparency`     | Boolean | When `true` removes "Transparency" menu item. Set to `false` to override `noTransparency: true` widget parameter.                                                                                              | all types
`swipe`              | Boolean | When `true` adds "Layer Swipe" menu item. Set to `false` to override `swipe: true` widget parameter.                                                                                                           | all types
`swipeScope`         | Boolean | When `true` adds Scope option to Layer Swipe menu. Default is `false`.                                                                                                                                         |
`expanded`           | Boolean | When `true` expands top level exposing sublayers or legend.                                                                                                                                                    | dynamic, feature & tiled
`sublayers`          | Boolean | When `false` dynamic folder/sublayer structure is not created.                                                                                                                                                 | dynamic
`metadataUrl`        | Boolean | When `true` and layer has `url` property (ArcGIS layers) links to service URL. When a URL links to said URL.                                                                                                   | all types
`allSublayerToggles` | Boolean | When `false` toggle all sublayers on/off layer menu items will not be included.                                                                                                                                | dynamic
`menu`               | Object  | An object consisting of menu item properties                                                                                                                                                                   | all types
`subLayerMenu`       | Object  | An object consisting of menu item properties                                                                                                                                                                   | dynamic

## Menu Items

All layers can have custom menu items added via the `menu` property.The menu system is set up using dojo/topic so that another widget can listen to when a menu item is clicked, and manipulate or add functionality to the app. Each menu item in the array will apply to each layer of the type specified in the key. Each menu item inside the array has the following properties:

- `label` - the string to display in the menu item
- `iconClass` - the icon class to add to the menu
- `topic` - the topic to publish when the menu item is clicked (see topics below)

Dynamic sublayers can have their own menu via the `subLayerMenu` property.

```javascript
menu: {

  // gives all feature layers the custom menu item 'Open Table...'
  feature: [{
    label: 'Open table...',
    iconClass 'fa fa-search fa-fw',
    topic: 'openTable'
  }]
},

// gives all dynamic layers the subLayerMenu items
subLayerMenu: {
  dynamic: [{
      label: 'Query Layer...',
      iconClass: 'fa fa-search fa-fw',
      topic: 'queryLayer'
  }, {
      label: 'Open Attribute Table',
      topic: 'openTable',
      iconClass: 'fa fa-table fa-fw'
  }]
 }
}
```

The menus can be completely overridden on a per layer basis also using the layers' `layerControlLayerInfos` property.

```javascript
layerControlLayerInfos: {

  // gives only this layer the custom menu item
  menu: [{
    label: 'Open Attribute Table',
    topic: 'openTable',
    iconClass: 'fa fa-table fa-fw'
  }],

  // gives only this layer's sublayers the menu item
  subLayerMenu: [{
    label: 'Say Hello',
    topic: 'sayHello',
    iconClass: 'fa fa-smile-o'
    }]
}
```

## Topics

The layer control publishes and subscribes to several `dojo/topic` items. 

Subscribe to any of the following topics. CMV aims to please, so let us know if you would like a topic published for a particular user action, or layer/layer control state change.

`layerControl/layerToggle` is published when layer visibility changes via the layer checkbox.

```javascript
topic.subscribe('layerControl/layerToggle', function (r) {
    console.log(r.id); //layer id
    console.log(r.visible); //layer visibility (true/false)
});
```

`layerControl/setVisibleLayers` is published when visible layers are set on a dynamic layer.

```javascript
topic.subscribe('layerControl/setVisibleLayers', function (r) {
    console.log(r.id); //layer id
    console.log(r.visibleLayers); //array of set visible layer ids
});
```

`layerControl/menuItemTopic` is published when a menu item is clicked.

```javascript
topic.subscribe('layerControl/menuItemTopic', function (r) {
    console.log(r.layer); //layer id
    console.log(r.subLayer); //array of set visible layer ids
    console.log(r.iconNode); //a domNode to toggle font awesome classes on
    console.log(r.menuItem); //the clicked menu item object in case you want to modify it

    //modify the iconNode to show that something happened to this layer
    if (r.iconNode) {
        if (domClass.contains(r.iconNode, 'fa-fire')) {
            domClass.remove(r.iconNode, 'fa-fire');
        } else {
            domClass.add(r.iconNode, 'fa-fire');
        }
    }
});
```

## LayerControl Class - Standalone outside of CMV

```javascript
require(['gis/dijit/LayerControl'], function (LayerControl) {
    var layerControl = new LayerControl({
        map: map,
        separated: true,
        vectorReorder: true,
        overlayReorder: true
        layerInfos: [
            // see LayerInfos
        ]
    }, srcRefNode);
});
```

**LayerInfo Parameters**

   Parameter     |  Type  | Description
:--------------: | :----: | -----------------------------------------------------------------------------------------------------
    `layer`      | Mixed  | A layer object OR layer id string.
     `type`      | String | Supports `dynamic`, `tiled`, `image` and `feature`. Additional layer types coming soon.
    `title`      | String | Title for the control. When loaded with CMV's widget loader this is the `title` option for the layer.
`controlOptions` | Object | Additional options for the layer control. See Control Options.

**LayerInfos**

The `layerInfo` object contains configuration options for each layer control. LayerControl initializes each layer control using these parameters.

```javascript
{
    layer: layer,
    type: 'dynamic',
    title: 'EPA TMDL 303d Reaches',
    controlOptions: {
        // see Control Options
    }
}
```

**Methods**

Method            | Description
----------------- | --------------------
`showAllLayers()` | Turn all layers on.
`hideAllLayers()` | Turn all layers off.
