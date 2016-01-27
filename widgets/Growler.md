# Growler

A notification system using `dojo/topic`.

##Topic Usage
By including the growler widget and using `topic.publish` you can create new growlers. This widget subscribes to the `'growler/growl'` topic.

####Example usage:
```javascript
geocoder.on('select', function(results){
    topic.publish('growler/growl', {
        title: 'Address found',
        message: 'Your address will appear on the map as a blue dot.'
        level: 'success', //possible classes are default, warning, success, error, info
        timeout: 10000,
        opacity: 0.5

    });
});
```

#### Example Config Object
``` javascript
growler: {
    include: true,
    id: 'growler',
    type: 'domNode',
    path: 'gis/dijit/Growler',
    srcNodeRef: 'growlerDijit',
    options: {}
},
```
