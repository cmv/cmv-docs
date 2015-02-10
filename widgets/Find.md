# Find
The search can be conducted on:
* a single field of a single layer
* many fields of a layer
* or on many fields of many layers

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

### Example layer to query

``` javascript
{
   // description value will appear in the drop-down list and sets the url used to query the map service
   description: 'Electric',
   url: 'http://ServerName/arcgis/rest/services/MapServiceName/MapServer',
   // layerIds are the intger values of each layer in the rest service of the map service you want to query   
   layerIds: [0,1,2,3,4,5,6],
   // fields in layerIds above to search upon
   searchFields: ['OWNER', 'BILLINGGROUP', 'INSTALL_NUM', 'POLENUMBER', 'STREETADDRESS', 'DEVICEID'],
   // minimum number of characters the user is required to enter before the Find widget will start the search
   minChars: 2
}
```

### Modify Default "Find Exact Matches Only" Checkbox Value
If you do not want the box checked by default to find exact matches then edit the file located in `viewer/js/gis/dijit/Find/templates/Find.html` 
from

``` html
<input type="checkbox" checked data-dojo-attach-point="containsSearchText" data-dojo-type="dijit.form.CheckBox" data-dojo-props="class:'containsCheck'"/>
```

to

``` html
<input type="checkbox" data-dojo-attach-point="containsSearchText" data-dojo-type="dijit.form.CheckBox" data-dojo-props="class:'containsCheck'"/>
```

Notice the value `checked` was removed in the template following `<input type="checkbox"`.

### Expose the Field Name in Results Grid
If you want the third and final column (the field name) that is available for display in the results grid you can modify the /dijit/Find/css/find.css.

Change the existing css from 

``` css
.gis_FindDijit .dgrid .field-value {
	width: 70%;
}
.gis_FindDijit .dgrid .field-foundFieldName {
	display: none;
}
```

to values that will work for your project, for example:

``` css
.gis_FindDijit .dgrid .field-value {
	width: 30%;
}

.gis_FindDijit .dgrid .field-foundFieldName {
	width: 30%;
}
```

### Change Default Sort Colunm
You can change the default sorting by altering the `Grid` `sort:` option by replacing with one of the other `columns:` name. The default sort is by `value:` which appears as the "Result" column to the end-user. You could sort by 'layerName:' which appears as "Layers" to the end user. 

In /dijit/Find.js under `createResultsGrid: function ()`

```
sort: [{
    attribute: 'layerName',
    descending: false
}]
```