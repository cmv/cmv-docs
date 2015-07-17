# Find

The Find widget allows you to configure multiple searches against an ArcGiS map service.  These searches can be conducted on:

* a single field of a single layer
* many fields of a single layer
* or on many fields of many layers

## Important concepts

When configuring the various options, it's important to remember that the widget is based on the [FindTask](https://developers.arcgis.com/javascript/jsapi/findtask-amd.html) and all results will be a FindResult object.  A FindResult object will contain a **feature** attribute which is a Graphic object.  This means it will have an **attributes** object with the properties of each result as specified by the layer in the base service.

It is important to recognize that the attribute names in this **attributes** property will be the field aliases specified for each field in the service definition and not the actual field name.

It is also important to understand that different layers in a map service can have very different attributes but the grid columns you specify apply to all layers included in the search.  It is therefore recommended to achieve best results that you either limit the layers included in each search to layers that have similar attributes *or*, limit the columns you specify to fields shared by all layers in a search.

## Tips

If you can control the service, it may be useful to use common aliases for fields in different layers.  For example:

```
PDNAME -> Name
```

```
FDNAME -> Name
```

```
RESNAME -> Name
```

You can also use a `get` function (detailed below) to compute and store a value on each FindResult item in your results.  A get function will be invoked and passed the FindResult object.  You can test for different properties to format the returned string.


## Specifying columns

There are two ways to specify columns.  Each has it's own benefits but follows the rules outlined in the [dgrid documentation](https://github.com/SitePen/dgrid/blob/v0.3.15/doc/components/core-components/Grid.md#specifying-grid-columns) for specifying grid structures.

Using an the array approach gives more flexibility but the object form is a handy shortcut for simple configurations.

### As an array of objects

Add a 'gridColumns' property to the search object.  The value should be an array of objects with the following properties:

- 'field': this is the field alias of the column to get the value from.
- 'get': this should be a function that accepts a find result item as the only argument and returns a string to display.
- 'label': The column heading
- 'resizable' <true/false>: whether or not the column can be resized
- 'visible' <true/false>: set to false to compute and store a value on each FindResult item without displaying it in a column.  This is useful for sorting.
- 'width': initial width of the column


### As an object

This is a handy shortcut for specifying column defininitons but is much less flexible.  Check the dgrid documentation for details.

Another way to specify a column is to use the get function.  Using this approach, the underlying dgrid instance will call the function you specify as the *get* property of a column object.  This function will receive the FindResult object and should return a string.  Check the Dgrid documentation for more information.

You can specify a visible property for each property.  Setting this to false is a useful way of computing and storing a property which can be specified as a attribute to sort on but will not be shown in the grid:

#### Get Function

The get function can be used to compute and return a string to display in a column or use as a sort attribute.  The partial example below uses a get function to to create a column that is not displayed in the grid but is used to sort the results.

```
gridColumns: [
    { field: 'SORT_VAL', visible: false, get: function ( item ) {
        return String( '0000' + item.feature.attributes.ASSET_NO ).slice( -4 );
    } }
],
sort: [
    {
        attribute: 'SORT_VAL',
        descending: false
    }
]
```


## Prompt

You can add a **prompt** property to each query object to set the placeholder or prompt text in the search input for the query.

## Selection mode

You can add a **selectionMode** property to control what results users can select in the results grid.  You need to specify any of the dgrid Selection mixin modes.

You can set this both for all queries (specify as a sibling of the **queries** property and optionally override for each query

## Symbology

You can add a **resultsSymbols** property to override the default symbology of each FindResult.  You can also add a **selectedSymbols** property to override the symbology used to depict selected find results in the map.

Each is an object with

* point
* polygon
* polyline

properties.  Each of which must be a fully formed JSON symbol definition appropriate to the geometry type.  Check viewer.js for examples.


## Custom grid event functions

You can add custom handlers for dgrid events by adding a **customGridHandlers** property which should be an array of objects:

```
customGridHandlers: [
  {
    event: '.dgrid-row:click',
    handler: function ( event ) {}
  }
]
```



#### Example Config Object
``` 
find: {
    include: true,
    id: 'find',
    type: 'titlePane',
    path: 'gis/dijit/Find',
    title: 'Find',
    open: false,
    position: 8,
    options: {
    map: true,
        queries: [
            {
                description: 'Buildings',
                url: 'https://localhost/arcgis/rest/services/Buildings/MapServer',
                layerIds: [ 0 ],
                searchFields: [ 'BUILDING', 'NAME' ],
                minChars: 2,
                prompt: 'Bldg# or name',
                gridColumns: [
                    { field: 'BUILDING', label: 'Building', resizable: false, width: 75, visible: true },
                    { field: 'NAME', label: 'Name', visible: true, get: function ( result ) {
                        var name = result.feature.attributes.NAME;
                        if ( result.feature.attributes.STATUS !== 'ACTIVE' ) {
                            name += ' ( ' + result.feature.attributes.STATUS + ' )';
                        }
                        return name;
                    } }
                ],
                sort: [
                    {
                        attribute: 'BUILDING',
                        descending: false
                    }
                ]
            },
            {
                description: 'Building Entrances',
                url: 'https://localhost/arcgis/rest/services/BuildingEntrances/MapServer',
                layerIds: [ 0 ],
                searchFields: [ 'BUILDING_DOOR_SEARCH' ],
                minChars: 2,
                prompt: 'Bldg# Door#',
                gridColumns: [
                    { field: 'EQUIPMENT', label: 'Equipment No', resizable: false, width: 75 },
                    { field: 'BUILDING', label: 'Building', resizable: false, width: 75 },
                    { field: 'FLOOR', label: 'Floor', resizable: false, width: 50 },
                    { field: 'ASSET_NO', label: 'Door No', resizable: false, width: 50 },
                    { field: 'SORT_VAL', visible: false, get: function ( item ) {
                        return String( '0000' + item.feature.attributes.ASSET_NO ).slice( -4 );
                    } }
                ],
                sort: [
                    {
                        attribute: 'SORT_VAL',
                        descending: false
                    }
                ],
                customGridEventHandlers: [
                    {
                        event: 'dgrid-select',
                        handler: function ( event ) {
                            var result = event.rows;
                            console.log( result );
                        }
                    }
                ],
                selectionMode: 'single'
            }
        ],
        selectionSymbols: {
            polygon: {
                type: 'esriSFS',
                style: 'esriSFSSolid',
                color: [ 255, 0, 0, 62 ],
                outline: {
                    type: 'esriSLS',
                    style: 'esriSLSSolid',
                    color: [ 255, 0, 0, 255 ],
                    width: 3
                }
            },
            point: {
                type: 'esriSMS',
                style: 'esriSMSCircle',
                size: 25,
                color: [ 255, 0, 0, 62 ],
                angle: 0,
                xoffset: 0,
                yoffset: 0,
                outline: {
                    type: 'esriSLS',
                    style: 'esriSLSSolid',
                    color: [ 255, 0, 0, 255 ],
                    width: 2
                }
            }
        },
        selectionMode: 'extended'
    }
},
```
