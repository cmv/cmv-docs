# Editor

A CMV friendly wrapper for the Esri editor widget. Accepts a `settings` property which is described on the Esri Javascript API page for the [Editor Widget](https://developers.arcgis.com/javascript/jsapi/editor-amd.html).

Feature layers are added by default to the editor widget. Feature layers with editing disabled will automatically be hidden.

## Example Config Object

```Javscipt
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
