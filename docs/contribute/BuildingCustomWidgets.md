# Building Custom Widgets

##Overview 
This application has been designed with the the goal of allowing users (a.ka. App Admins) to configure widgets without having to write code. Programmers can add new configurable widgets, by following the rules required to fit in to the viewer framework. Knowledge of [ESRI's JavaScript API] (https://developers.arcgis.com/javascript/) and [dojo] (https://developers.arcgis.com/javascript/jshelp/inside_dojo.html) are required.
 
##Summary of Steps 
1. Create a new widget `viewer/js/gis/dijit/Widget.js`
2. Create any dependent widget folders (optional) in `viewer/js/gis/dijit/Widget` 
   * `viewer/js/gis/dijit/Widget/templates/Widget.html`
   * `viewer/js/gis/dijit/Widget/css/Widget.css`
   * `viewer/js/gis/dijit/Widget/images/WidgetPicture.png`
3. If your widget offers widget specific configurations for the App Admin to utilize then create a config file in `viewer/js/config/widget.js`

**Note** the naming convention used for consistency across core CMV widgets and contributed widgets. Use proper case name for the widget here `viewer/js/gis/dijit/Widget.js` and lowercase name for the supporting configuration file here `viewer/js/config/widget.js`

##Widget Configuration
All widgets are configured by the App Admin in [viewer/js/config/viewer.js] (https://github.com/cmv/cmv-app/blob/master/viewer/js/config/viewer.js). Optional supporting widget configuration files that you as the developer provide can be configured by the App Admin here `viewer/js/config/widget.js`.

The `viewer.js` passes [inherited properties](https://github.com/cmv/cmv-app/wiki/Configuration-file-viewer.js#widget-section) as well as your widget specific properties by way of `viewer/js/viewer/Controller.js`. You will not need to modify `viewer/js/viewer/Controller.js`. This file does the heavy lifting of incorporating your widget into CMV.

##Widget Definition
Refer to existing core CMV widgets to help you build your new widget. The skeleton of a widget is as follows.

    define([
        "dojo/_base/declare",
        "dijit/_WidgetBase",
        "dijit/_TemplatedMixin",
        "dojo/text!./templates/MyWidget.html"
	], function(declare, _WidgetBase, _TemplatedMixin, template) {
	 
        return declare([_WidgetBase, _TemplatedMixin], {
            templateString: template
        });
    });

##Useful Resources
These links are helpful for those unfamiliar with dijits.
* [Creating Custom Widgets](http://dojotoolkit.org/documentation/tutorials/1.8/recipes/custom_widget/)
* [Creating templated widgets](http://dojotoolkit.org/documentation/tutorials/1.8/templated/)
* [ESRI custom widget tutorial](https://developers.arcgis.com/javascript/jshelp/intro_custom_dijit.html)