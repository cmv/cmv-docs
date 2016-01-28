# Widgets Section of viewer.js

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


#### Core Widgets
The documentation for core CMV widgets is located [here](../widgets/).
