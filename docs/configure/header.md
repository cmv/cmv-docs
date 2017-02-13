# Header configuration in viewer.js

The header section is used to set up and configure various ArcGIS Javascript JS API options as well as anything else that needs to be set before the app begins loading. This includes items such as:

 * Proxy - URLS to proxy services 
 * Geometry Service
 * Google Maps API Key (for Google Streetview and other widgets that may require the Google API)
 * Other preinitialization logic

## Esri Configuration options in viewer.js

By default the following properties are set:
```javascript
    esriConfig.defaults.io.proxyUrl = 'proxy/proxy.ashx';
    esriConfig.defaults.io.alwaysUseProxy = false;
    esriConfig.defaults.geometryService = new GeometryService('https://tasks.arcgisonline.com/ArcGIS/rest/services/Geometry/GeometryServer');
```

You may also configure proxy rules by adding `'esri/urlUtils'` to your amd `define` block and function. Make sure the order of your module strings match the order of the modules listed in your function. 

For the full list of configuration options visit [the ArcGIS Javascript API documentation](https://developers.arcgis.com/javascript/3/jshelp/inside_defaults.html)

## Google API

By default the Google Maps loader is already imported to viewer.js, and you can set the key using the `KEY` property. 

```javascript
    // https://developers.google.com/maps/documentation/javascript/get-api-key
    GoogleMapsLoader.KEY = 'NOT-A-REAL-API-KEY';
```

## Other initialization scripts

If there are other initializations you would like to perform, the header area of the viewer.js is one option. For example, by default a `buildImageParameters` function is defined which is used later to help us create Dynamic Map Service layer [Image Parameters](https://developers.arcgis.com/javascript/3/jsapi/imageparameters-amd.html)

In addition, as an example we have added a topic registration. This demonstrates how the layer control's menu topic works. However in the real world, it is best to keep these extra functions minimal and perhaps separate them into a different module or even build a separate widget. This will increase your possibilities of reusing the code in other CMV and Dojo apps. 
