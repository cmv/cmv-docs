# Identify

## Example Config Object
``` javascript
identify: {
   include: true,
   id: 'identify',
   type: 'invisible',
   path: 'gis/dijit/Identify',
   options: 'config/identify'
},
```

## Configuration File
The file can be found here `viewer/js/config/identify.js`. CMV comes with examples inside this file. Review this file on how to configure the widget for your use.

## Identify options

Property | Type | Description
---------|------|------------
`mapClickMode` | `Boolean` | In CMV, set this to `true` to enable the shared map click functionality.
`mapRightClickMenu` | `Boolean` | In CMV, set this to `true` to enable the right click identify menu Alternatively set this to `'identify'`
`identifyLayerInfos` | `Array<Object>` | In CMV, set this to `true` to enable the controller to pass the layer infos
`identifies` | `Object` | The identify info for each layer and sublayer. See [Identifies Object](#identifies-object)for more details
`draggable` | `Boolean` | Whether or not to enable the click/drag functionality of the popup
`identifyTolerance` | `Number` | The number of pixels to identify around a map click. The default is `5`

### Identifies object

An identifies object consists of the nested structure below where `layer` is the layer id, and
`0` is the id number of the sublayer.

```javascript
layer: {
  0: {
    // popup properties
  }
}
```

**Note:** CMV uses the [PopupTemplate Class](https://developers.arcgis.com/javascript/jsapi/popuptemplate-amd.html) for the Identify widget. The  [ArcGIS JS API Documentation](https://developers.arcgis.com/javascript/jshelp/intro_popuptemplate.html) needs revision to clarify the use of the field names when using the PopupTemplate Class. On the page linked above the section named "fieldInfo structure:" states that `fieldName:` comes from the name of the field. This is vague and is clarified below.

To display your identify results with attribute values you must **use the _field alias_ as defined in the map service rest end point** and _do not use any other field name or alias defined in the geodatabase_.

 - If a MXD alias is provided when the map service is published, the MXD alias is used as the field name
 - Otherwise, the geodatabase alias is used if it is provided
 - Finally, the geodatabase field name will be used

## Formatting values

Formatting values in the identify popup can be done using the `formatter` property in the `fieldInfos`. 

**Warning: By applying a formatter to a value, this will modify the feature's attribute value after it is identified. For instance `map.infoWindow.getSelectedFeature()` will return the modified feature. To avoid this, consider using virtual fields.**

**Formatter parameters:**

 - `value` - the value of the given field name. This will be an undefined value if
            the field name given does not exist. (useful for creating extra properties)
 - `attributes` - an object with all of the properties in the identified feature
 - `geometry` - the identified feature geometry

**Virtual fields**

Virtual fields are fields that don't exist in the map service, and instead are generated on the fly using a formatter. 

```javascript
fieldInfos: [{
    fieldName: 'pole_id',
    visible: true,
    formatter: function (value, attributes, geometry) {

        // create a link to a different app
        return '<a href="/poleapp/' + value + '">Pole App</a>';
    }
}, {
    // create a virtual field
    fieldName: 'My super cool field',
    visible: true,
    formatter: function(value, attributes, geometry) {
        // value is undefined here so we can only use attributes and geometry 
	return geometry.x + ', ' + geomtry.y;
    }
}]
```

## Images and Media

In general, images and other media like pie charts can be created using the
`mediaInfos` property of the popup definition. But in other advanced cases,
`formatter` may provide the functionality. In addition, the `content` property
may be used for other advanced cases. [See below.](#build-your-own-identify-popup)

## Build your own identify popup

The JavascriptAPI has [a nice tutorial](https://developers.arcgis.com/javascript/jshelp/intro_formatinfowindow.html) on formatting the info window content. Specifying a content formatter will allow you to do things like:

* Programatically generate html for the popup (bullet list)
* Alter field values (convert a image url to image)
* Embed other widgets like a tab container and chart/table in the popup window

The identify widget will check for a `content` property in each `identifies` object. This property can be either a **string or function**.
Example usage:
``` javascript
electric: {
    1: {
	title: 'Pole',
	content: formatterFunction //or html string
	}
}
```

In the example above, formatterFunction is a **global** function, which Esri recommends. However, there is a safer and better way to pass a function and avoid adding globals to the application.

Convert the identify.js into a config similar to the viewer.js:
```JavaScript
define([
	//include any widgets and dojo class paths you want to use here
], function (/* each widget you include should have a variable here */) {
	return {
		map: true,
	        mapClickMode: true,
	        mapRightClickMenu: true,
	        identifyLayerInfos: true,
	        identifyTolerance: 5,
	        identifies: {}
	};
});
```
Just before the return statement, create a local variable, lets call it formatters:
```JavaScript
var formatters = {
	link: function(identifyResults) {
		//add logic to format the results and return an html string or domNode
	}
};
```

Add a layer to the identifies and add the `content: formatters.link`

To add something more complex like a TabContainer to the identify window:
```JavaScript
var formatters = {
	attributeList: function (identifyInfo) {
            var listItem = '<li>{0}: {1}</li>';
            var html = ['<ul>'];
            for (var a in identifyInfo.attributes) {
                //make sure a is an own property
                if (identifyInfo.attributes.hasOwnProperty(a)) {
                    html.push(lang.replace(listItem, [a, identifyInfo.attributes[a]]));
                }
            }
            html.push('</ul>');
            return html.join('');
        },
	tabContainer: function(identifyResults) {
		var container = new TabContainer(
			style: 'height: 100%; width: 100%;'
                }, domConstruct.create('div'));
		container.addChild(new ContentPane({
			title: 'my title',
			content: 'You clicked a feature. The results are in the next tab'
		});
		container.addChild(new ContentPane({
			title: 'Attributes',
			content: formatters.attributeList(identifyresults)
		});
		return container.domNode;
	}
};
```

The final identify result:
```JavaScript
define([
    'dojo/_base/lang',
    'dijit/layout/TabContainer',
    'dijit/layout/ContentPane',
    'dojo/dom-construct',
], function (lang, Container, ContentPane, domConstruct) {
    var formatters = {
        attributeList: function (identifyResults) {
            var listItem = '<li>{0}: {1}</li>';
            var html = ['<ul>'];
            for (var a in identifyResults.attributes) {
                //make sure a is an own property
                if (identifyResults.attributes.hasOwnProperty(a)) {
                    html.push(lang.replace(listItem, [a, identifyResults.attributes[a]]));
                }
            }
            html.push('</ul>');
            return html.join('');
        },
	tabContainer: function(identifyResults) {
		var container = new TabContainer(
			style: 'height: 100%; width: 100%;'
                }, domConstruct.create('div'));
		container.addChild(new ContentPane({
			title: 'my title',
			content: 'You clicked a feature. The results are in the next tab'
		});
		container.addChild(new ContentPane({
			title: 'my title',
			content: formatters.attributeList(identifyresults)
		});
		return container.domNode;
	}
    };
    return {
        map: true,
        mapClickMode: true,
        mapRightClickMenu: true,
        identifyLayerInfos: true,
        identifyTolerance: 5,
        identifies: {
	        electric: {
		    1: {
			title: 'Pole',
			content: formatters.tabContainer
			}
		}
        }

    };
});
```
