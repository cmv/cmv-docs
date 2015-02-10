# Bookmarks

A Bookmark represents individual spatial locations of a geographic area. You can use bookmarks to highlight areas on your map you want the user to quickly see. A predefined list of bookmarks can appear in the widget or you may allow the user to add their own bookmarks. Modify `\config\bookmark.js` to create a predefined list for the user. In 'config\viewer.js' you can choose to display the widget as well set the option to allow the user to edit bookmarks.

You can use David Spriggs' [JS Extent Helper](http://psstl.esri.com/apps/extenthelper/) to obtain extents to modify the `viewer\js\config\bookmarks.js` file. You can add default bookmarks as you wish for the end user to utilize when the app loads. Also, you can allow the end user to edit the bookmarks as well. To allow the end user to modify the bookmarks set `editable:` to true. 

## Example Configuration File

``` javascript
define({
	map: true,
	editable: true,
	bookmarks: [
		{
			name: 'Alachua',
			extent: {
				xmin: 2585305.000345871,
				ymin: 266868.2628403753,
				xmax: 2640795.4403458685,
				ymax: 311100.00284036994,
				spatialReference: {
					wkid: 102660
				}
			}
		},
		{
			name: 'Archer',
			extent: {
				xmin: 2586339.0203458667,
				ymin: 193589.25284036994,
				xmax: 2605705.230345875,
				ymax: 211638.83284036815,
				spatialReference: {
					wkid: 102660
				}
			}
		},
		{
			name: 'Gainesville',
			extent: {
				xmin: 2628433.292845875,
				ymin: 223701.73534037173,
				xmax: 2691781.912845865,
				ymax: 289218.2578403652,
				spatialReference: {
					wkid: 102660
				}
			}
		},
		{
			name: 'Hawthorne',
			extent: {
				xmin: 2728213.900345877,
				ymin: 209241.0128403753,
				xmax: 2745459.1903458685,
				ymax: 233347.00284036994,
				spatialReference: {
					wkid: 102660
				}
			}
		},{
			name: 'High Springs',
			extent: {
				xmin: 2556964.4703458697,
				ymin: 276958.33284036815,
				xmax: 2591340.980345875,
				ymax: 317286.4528403729,
				spatialReference: {
					wkid: 102660
				}
			}
		},
		{
			name: 'Lacrosse',
			extent: {
				xmin: 2627223.6203458756,
				ymin: 304157.0428403616,
				xmax: 2651389.5403458774,
				ymax: 318795.72284036875,
				spatialReference: {
					wkid: 102660
				}
			}
		},
		{
			name: 'Micanopy',
			extent: {
				xmin: 2671081.475345865,
				ymin: 188239.75034037232,
				xmax: 2678538.290970877,
				ymax: 193685.25284036994,
				spatialReference: {
					wkid: 102660
				}
			}
		},{
			name: 'Newberry',
			extent: {
				xmin: 2553863.030345872,
				ymin: 199531.5128403753,
				xmax: 2596468.000345871,
				ymax: 274733.9928403646,
				spatialReference: {
					wkid: 102660
				}
			}
		},
		{
			name: 'Waldo',
			extent: {
				xmin: 2703015.000345871,
				ymin: 290415.78284037113,
				xmax: 2715093.350345865,
				ymax: 305948.00284036994,
				spatialReference: {
					wkid: 102660
				}
			}
		}
	]
});
```