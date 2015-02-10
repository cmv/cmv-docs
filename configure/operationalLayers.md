# Operational Layers Section of viewer.js

Layers to load on top of the basemap. See [Class: Layer] (https://developers.arcgis.com/javascript/jsapi/layer-amd.html) for more information on types of layers and [Layer options] (https://developers.arcgis.com/javascript/jsapi/layer-amd.html#layer1).

### Example
See [operational layers section in viewer.js] (https://github.com/cmv/cmv-app/blob/master/viewer/js/config/viewer.js#L63) for examples.

The following list indicates tested and untested layers that can be used in CMV
* `type: csv // 'CSV'`
* `type: dynamic // 'ArcGISDynamicMapService'`
* `type: feature // 'Feature'`
* `type: georss // 'GeoRSS'`
* `type: image // 'ArcGISImageService'`
* `type: kml // 'KML'`
* `type: label // 'Label', untested`
* `type: mapimage // 'MapImage', untested`
* `type: osm // 'OpenStreetMap'`
* `type: tiled // 'ArcGISTiledMapService'`
* `type: wms // 'WMS'`
* `type: wmts // 'WMTS', untested`