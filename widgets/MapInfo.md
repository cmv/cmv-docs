# Map Info

Map Info is a simple widget for displaying mouse coordinates. Optionally map scale and zoom level can also be displayed.

### HTML
CMV includes a dom node for the widget in `mapOverlay.html`:

```html
<div style="position:absolute;bottom:0;left:0;z-index:40;">
    <div id="mapInfoDijit">
    </div>
</div>
```

### Config
In `viewer/config.js`:

```javascript
mapInfo: {
	include: true,
	id: 'mapInfo',
	type: 'domNode',
	path: 'gis/dijit/MapInfo',
	srcNodeRef: 'mapInfoDijit',
	options: {
		map: true, //required
		mode: 'dms', //'map', 'dec' or 'dms'
		firstCoord: 'y', //which coord to display first ('x')
		unitScale: 2, //coord decimal places (2)(affects seconds in 'dms' format)
		showScale: true, //show map scale (false)
		showZoom: false, //show zoom level (false)
		xLabel: 'X:', //label for x coord ('X:')
		yLabel: 'Y:', //label for y coord ('Y:')
		scaleLabel: '1:', //label for map scale ('1:')
		zoomLabel: 'Z', //label for zoom level ('Z')
		minWidth: 286, //minimum width in pixels of widget (0)(when 0 widget fits content)
		proj4Catalog: 'EPSG', //'ESRI', 'EPSG' or 'SR-ORG' **
		proj4Wkid: 2992 //wkid of the map **
	}
}
```

Defaults are shown in parenthesis.

** `proj4Catalog` and `proj4Wkid` are only used and required when using a non Web Mercator or WGS projection and mode is `dec` or `dms`.

###CSS
MapInfo loads its own CSS and can be found in `js/gis/dijit/MapInfo/css/MapInfo.css`