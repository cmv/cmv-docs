# Directions

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
