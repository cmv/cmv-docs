# Print

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
        defaultLayout: 'Letter ANSI A Landscape',
        resultOrder: 'last' // can be first or last
    }
},
```
