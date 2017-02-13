# Widgets Section of viewer.js

## Widget Properties

Key          | Type      | Description
------------ | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------
`include`    | `Boolean` | Whether or not to include this widget. The default is `false`
`type`       | `String`  | The widget type. See [Widget Types](#widget-types) below
`canFloat`   | `Boolean` | Whether or not to display a float arrow which when clicked allows the widget to be dragged around the cmv app
`placeAt`    | `String`  | The pane to place the widget. The default is `'left'`
`path`       | `String`  | The path to the widget. For cmv widgets, this is typically `'gis/dijit/Widgetname'`. Other widget paths can be configured using `dojoConfig`
`id`         | `String`  | A unique identifier used to create a unique dom node for this widget. If not provided, the object key is used
`title`      | `String`  | The title to display for `'titlePane'` type widgets
`iconClass`  | `String`  | The font awesome icon class to use in `titlePane` type widgets. Example: `'fa-picture-o'`
`open`       | `Boolean` | Whether or not this widget should be open by default. This is used for `'titlePane'` type widgets
`position`   | `Number`  | A number representing the order to display widgets in the pane. The larger numbers will be placed towards the end, while `0` will be first
`srcNodeRef` | `String`  | A string "id" for a dom node.Used for `'domNode'` type widgets.
`options`    | `Object`  | Widget options passed to the widget constructor. These options will override default properties and methods. See [Widget Options](#widget-options) below for details

### Widget Types

Type            | Description
--------------- | -------------------------------------------------------------------------------------------------------------------------------------------
`'titlePane'`   | The collapsible widget type with a title and optional floating capability
`'contentPane'` | An content pane with no additional content or functionality. The widget will always be visible and not 'toggle-able'
`'floating'`    | Displays the widget in a floating type dialog when its `show` method is called. Set this widgets option `open` to `true` to show by default
`'domNode'`     | Place this widget in a specific dom node by id. To use this type, `srcNodeRef` must be included
`'invisible'`   | Used for widgets that don't have a UI, but instead perform background functions like modifying the map
`'map'`         | Widgets that load after the map is loaded
`'layer'`       | Widgets that load after the layers are loaded
`'layout'`      | Widgets that load after the layout (panes) has completed but before the map is loaded
`'loading'`     | Widgets that load as soon as possible

### Widget Options

CMV has several built in widget options. In addition each widget can generally accept several options as well, these properties are documented in each widget's documentation.

The builtin properties are listed below. These properties are all boolean flags that tell the CMV widget loader to pass the object to the widget. For example, setting `map: true` in the widgets options will pass the cmv map object to the widget using the key `map`

Key                      | Description
------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
`map`                    | Pass the main map object to the widget
`mapRightClickMenu`      | Pass a menu object to the widget that allows the widget to modify the maps right click menu by adding new options
`mapClickMode`           | Pass the current map click mode to the widget. This allows widgets to "share" the map click by ensuring not all widgets are active when the map is clicked. For example, you wouldn't want to identify features when you are drawing
`legendLayerInfos`       | Pass the array of legend layer infos to the widget. This is a custom array built inside cmv that is generally only used for the Esri legend widget
`layerControlLayerInfos` | Pass the layer control structured layers to the widget. This is often used by the layer control as well as custom widgets that require access to the layers
`identifyLayerInfos`     | Pass the identify structured layers to the widget. This is generally only used by the identify widget

Additionally, some properties are passed by cmv automatically. These properties can be accessed by custom and cmv widgets.

Key            | Type     | Description
-------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------
`parentWidget` | `Object` | The parent widget object, for example in title pane widget types, the parent widget will be the `dijit/layout/TitlePane` object

## Example Widget Config

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

## Core Widgets

The documentation for core CMV widgets is located [here](../widgets/).
