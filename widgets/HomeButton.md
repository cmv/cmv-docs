# Home Button

Esri's out-of-the-box home button widget. See `esri/dijit/HomeButton` [documentation](https://developers.arcgis.com/javascript/jsapi/homebutton-amd.html)

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
