# Identify

### Identify widget configuration file
The file can be found here `viewer/js/config/identify.js`. CMV comes with examples inside this file. Review this file on how to configure the widget for your use.

**Note** CMV uses the [PopupTemplate Class](https://developers.arcgis.com/javascript/jsapi/popuptemplate-amd.html) for the Identify widget. The  [ArcGIS JS API Documentation](https://developers.arcgis.com/javascript/jshelp/intro_popuptemplate.html) needs revision to clarify the use of the `fieldInfos:` array when using the PopupTemplate Class. On the page linked above the section named "fieldInfo structure:" states that `fieldName:` comes from the name of the field. This is vague and is clarified below.

To display your identify results with attribute values you must **use the _field alias_ as defined in the map service rest end point** and _do not use any other field name or alias defined in the geodatabase_. 

You can not reliably use the field name or the alias as defined in the geodatabase. Nor can you reliably use the field name as defined in the map service. You must use the field alias as defined in the map service. Here are some situations as to why you can not reliably use the _field name_ as defined in the map service:

* The geodatabase administrator may not use an alias for the field name, so by default the alias and field name are the same.

* The geodatabase administrator may use an alias for the field name and, obviously, the names are different.

* The publisher of the map service may alter the alias within the MXD prior to publishing. This impacts situations one and two above.

* The publisher of the map service may exclude certain fields of a feature class in the geodatabase prior to publishing.

Please see the example below for clarity:

The following screen shots will demonstrate the various situations above as well the results of this `viewer/js/config/identify.js` configuration

``` javascript
electric: {
    1: {
	title: 'Pole',
	fieldInfos: [{
            //geodatabase field name is 'FACILITYID'
            //geodatabase field alias is not defined therefore defaults to 'FACILITYID'
            //MXD altered the field alias to 'Pole Number', therefore attribute value will not be displayed
            //'fieldName:' must match the MXD's field alias
            fieldName: 'FACILITYID',
            label: 'Facility ID',
            visible: true
	},{
            //geodatabase field name is 'MATERIAL'
            //geodatabase field alias is not defined therefore defaults to 'MATERIAL'
            //MXD altered the field alias to 'Material', note case change
            //'fieldName:' must match the MXD's field alias and is case sensitive
            //attribute value is displayed
            fieldName: 'Material',
            visible: true					
	},{
            //geodatabase field name is 'POLESIZE'
            //geodatabase field alias is not defined therefore defaults to 'POLESIZE'
            //MXD altered the field alias to 'PoleSize', note case change, and attribute value is not displayed
            //'fieldName:' must match the MXD's field alias and is case sensitive
            fieldName: 'PoleSize',
            visible: true					
	},{
            //geodatabase field name is 'BACKBONEINDICATOR'
            //geodatabase field alias is not defined therefore defaults to 'BACKBONEINDICATOR'
            //MXD did not alter the field alias
            //attribute value is displayed
            //You can use 'label:' to display an alias in a PopupTemplate
            fieldName: 'BACKBONEINDICATOR',
            label: 'Back Bone',
            visible: true					
	},{
            //geodatabase field name is 'AGREEMENT'
            //geodatabase field alias is not defined therefore defaults to 'AGREEMENT'
            //MXD then defaults field alias to 'AGREEMENT'
            //MXD excludes this field prior to publishing
            //Attribute value is not be displayed in a PopupTemplate, even though 'fieldName:' matches alis in MXD
            fieldName: 'AGREEMENT',
            visible: true					
	}]
    }
},
```

![Identify Results](https://edop.gru.com/IdentifyResults.PNG)
![FACILITYID](https://edop.gru.com/FacilityID.PNG)
![Material](https://edop.gru.com/Material.PNG)
![PoleSize](https://edop.gru.com/PoleSize.PNG)
![Agreement](https://edop.gru.com/Agreement.PNG)
