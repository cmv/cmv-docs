2016-02-08
==========

  * Merge pull request [#505](https://github.com/cmv/cmv-app/issues/505) from mgd722/master
    Added 'draggable' property to identify config object

2016-02-07
==========

  * Added 'draggable' property to identify config object
    After looking through CMV docs, it seemed most appropriate to just put
    this property here.  The sample config object in the docs is for
    viewer.js or custom info windows and this is a pretty straightforward
    setting.

2015-07-18
==========

  * update version number to 1.3.4

2015-07-16
==========

  * Merge pull request [#432](https://github.com/cmv/cmv-app/issues/432) from cmv/feature/exclude-feature-layers-from-editor-widget
    exclude feature layers from Editor widget. Closes [#221](https://github.com/cmv/cmv-app/issues/221)
  * Merge pull request [#435](https://github.com/cmv/cmv-app/issues/435) from cmv/feature/upgrade-to-v3.14
    Update to JS API v 3.14
  * Merge pull request [#433](https://github.com/cmv/cmv-app/issues/433) from cmv/bug/mapinfo-widget-setScale-error
    avoid occasional error in `number.format` in mapInfo widget
  * Merge pull request [#424](https://github.com/cmv/cmv-app/issues/424) from roemhildtg/add-icon-to-menu-topic
    Add icon to menu topic
  * Update to JS API v 3.14

2015-07-14
==========

  * avoid occasional error in `number.format` by checking for a non-numeric scale.
  * exclude feature layers from Editor widget. Closes [#221](https://github.com/cmv/cmv-app/issues/221)

2015-06-08
==========

  * Remove uneeded subMenus
  * Remove unecessary PopupMenuItem
  * Add iconNode to the template and pass it as a parameter to the topic.publish method. Allow widget developers to change the icon of the iconNode when the menu item is clicked.

2015-06-07
==========

  * Merge pull request [#420](https://github.com/cmv/cmv-app/issues/420) from cmv/feature/geocoder-map-extent
    limit geocoder search to map extent

2015-05-27
==========

  * limit geocoder search to map extent
  * Merge pull request [#401](https://github.com/cmv/cmv-app/issues/401) from roemhildtg/develop
    Add menu to Layer Controller sub-layers
  * Merge pull request [#419](https://github.com/cmv/cmv-app/issues/419) from roemhildtg/add-identify-popup-content
    Allow the use of the popup's setContent method.

2015-05-26
==========

  * check for a content value in the popup identify config and if it exists, call the setContent method on the popup after initializing it.

2015-05-19
==========

  * Merge pull request [#407](https://github.com/cmv/cmv-app/issues/407) from cmv/feature/add-additional-layer-types
    Add support for additional layer types
  * Merge pull request [#408](https://github.com/cmv/cmv-app/issues/408) from cmv/feature/directions-widget-error-with-v3.13
    Add additional code to hide map click button with JS API version 3.13
  * Merge pull request [#409](https://github.com/cmv/cmv-app/issues/409) from cmv/feature/fix-floating-window-drag-not-releasing
    Add mouseup and touchend events to document to release dragging movable.
  * Merge pull request [#410](https://github.com/cmv/cmv-app/issues/410) from cmv/feature/find-widget-enhancements
    Feature/find widget enhancements

2015-05-03
==========

  * Merge pull request [#402](https://github.com/cmv/cmv-app/issues/402) from cmv/feature/add-support-for-hiding-oplayers-in-legend
    add support for hiding operational layers in the legend

2015-04-30
==========

  * Add mouseup and touchend events to document to release dragging movable.

2015-04-28
==========

  * Add additional code to hide map click button with JS API version 3.13
  * Add support for the following layer types to CMV Controller and
    the layerControl widget:
    * WebTiledLayer
    * ArcGISImageServiceVectorLayer (with legend)
    * RasterLayer
    * StreamLayer (with Legend)
    Add support for the following layer types to Controller:
    * DataAdaptorFeatureLayer (untested)
  * Remove splitter on left pane for consistency with current demo app
  * Revert title of Find widget back to "Find" and set it to not open at start
  * move "Find exact matches only" checkbox back to main form
    allow options button to be hidden and hide by default
    change label for options button to "Options" to better reflect it's purpose
  * Format code for consistency with other modules

2015-04-19
==========

  * Remove unused showInLegend param
  * Add support for additional legend layerInfos params (layerInfo param)
    https://developers.arcgis.com/javascript/jsapi/legend-amd.html#legend1
  * implement tmcgee's suggestion for consistency with other configuration options.
  * add support for hiding operational layers in the legend (legendLayerInfos array)

2015-04-14
==========

  * Add subLayerMenu to LayerControl class to avoid undefined errors
  * If a layer control has a submenu, style it blue.
  * Add a subLayerMenu property to LayerControl options. Pass a subset of this menu object to the sub layer control using the type. Modify DynamicSublayer to add a menu.

2015-03-03
==========

  * Merge pull request [#388](https://github.com/cmv/cmv-app/issues/388) from cmv/feature/update-to-JS-API-v-3.13
    Update to JS API v 3.13
  * Merge pull request [#389](https://github.com/cmv/cmv-app/issues/389) from cmv/feature/add-slack-hook-to-.travis.yml
    Add Slack Notification hooks to .travis.yml

2015-03-02
==========

  * Rename: AdvancedFind -> Find
  * remove existing find widget
  * Add Slack Notification hooks to .travis.yml

2015-03-01
==========

  * Update to JS API v 3.13
    Update to Font-Awesome v 4.3.0
    Update to Proj4JS v 2.3.3

2015-02-19
==========

  * remove README
    moving to docs repo
  * add options for controlling zoom, new options btn
    Add checkboxes to control zooming on select/deselect.  Move checkboxes to Options dropdown.
  * make extent scaling factor configurable
  * rename method
  * remove white space
  * refactoring - clean up complex conditionals

2015-02-18
==========

  * log event object
  * add a customGridEventHandlers example
  * attempt to fix travis  build issue
    failed JSHint [ 'Fcode' ] better written in dot notation.  However, this will likely fail due to camel casing.
  * initial readme documentation
    This still needs lots of work!
  * add sample configuration for advanced find
  * add advanced find widget

2015-02-09
==========

  * Update README.md
    Fix the documentation icons.
  * Merge pull request [#377](https://github.com/cmv/cmv-app/issues/377) from cmv/feature/update-for-read-the-docs
    Update README for new documentation
  * Clean up the README
  * Additional edits to README
  * Update README for new documentation
    Remove 3 *.md files that are now in documentation
    Update package.json to version 1.3.3 & current year.

2015-01-27
==========

  * Merge pull request [#365](https://github.com/cmv/cmv-app/issues/365) from cmv/patch/directionsFix
    Patch/directions fix
  * Revert "3.12 added a new map click feature which does not work with CMV. I deactivated this default feature and hid the botton in the dom until we can better address this (need an update to the API)."
    This reverts commit d98c00854f72af70d791c15442c5d46c9ac7c446.
  * 3.12 added a new map click feature which does not work with CMV. I deactivated this default feature and hid the botton in the dom until we can better address this (need an update to the API).

2015-01-22
==========

  * Merge pull request [#356](https://github.com/cmv/cmv-app/issues/356) from cmv/feature/find-widget-zoom-on-click
    zoom on row click instead of select

2015-01-21
==========

  * fix build error: line [#377](https://github.com/cmv/cmv-app/issues/377)
  * zoom on row click or keyboard navigation
    add event handler to zoom to feature selected vai keyboard navigation.
    extract method to return feature from row event.
  * zoom on row click instead of select
    use the .dgrid-row:click to handle zooming to clicked feature.  This handles the case where the user has clicked on a feature, then manually panned the map.  Now clicking on the selected feature will pan the map back to the selected feature.

2015-01-11
==========

  * Merge pull request [#344](https://github.com/cmv/cmv-app/issues/344) from cmv/issues/341-fix
    fix for issue [#341](https://github.com/cmv/cmv-app/issues/341)
  * fix for issue [#341](https://github.com/cmv/cmv-app/issues/341)
    locate button displays html tags in message as text.  Also, cleans up altitude accuracy label in locate button template.

2014-12-24
==========

  * Merge pull request [#333](https://github.com/cmv/cmv-app/issues/333) from cmv/feature/keep-track-of-floating-widget-sidebar-position
    Keep track of floating widget sidebar position. Use full titlebar for docking/moving widgets.
  * Merge pull request [#331](https://github.com/cmv/cmv-app/issues/331) from cmv/feature/update-to-JS-API-v-3.12
    Update the JavaScript API from version 3.11 to 3.12

2014-12-15
==========

  * fixed formatting
  * Added support for undocking and moving the floating widgets using the
    entire titlebar which should be more intuitive.

2014-12-14
==========

  * Update the JavaScript API from version 3.11 to 3.12
    ** Note: This is untested. Version 3.12 has not been officially
    announced at the time of this commit. **
  * keep track of floating widget's position in sidebar when undocked
    so it will be re-docked in the same position.

2014-12-02
==========

  * Merge pull request [#325](https://github.com/cmv/cmv-app/issues/325) from cmv/feature/draggable-info-window
    allow info window for identified features to be temporarily dragged
  * Merge pull request [#326](https://github.com/cmv/cmv-app/issues/326) from cmv/fix/sidebar-splitter-and-IE10
    fixes [#322](https://github.com/cmv/cmv-app/issues/322)
  * fixes [#322](https://github.com/cmv/cmv-app/issues/322)
  * allow info window for identified features to be temporarily dragged
    away from the identify location. Once a new feature is selected via the
    previous/next arrow icons or a new identify is executed the window
    bounces back to the proper identify location.
  * Merge pull request [#324](https://github.com/cmv/cmv-app/issues/324) from cmv/patch/LayerControl-1.3.2
    Add kml legend

2014-12-01
==========

  * Add kml legend

2014-11-30
==========

  * Merge pull request [#321](https://github.com/cmv/cmv-app/issues/321) from cmv/fix/use-innerHTML-to-set-header-and-subheader
    Use innerHTML instead of innerText to set configurable header/subheader.
  * Use innerHTML instead of innerText to set configurable header/subheader.
  * Merge pull request [#320](https://github.com/cmv/cmv-app/issues/320) from cmv/update/LayerControl-1.3.2
    Update/layer control 1.3.2

2014-11-29
==========

  * Dynamic sublayer control updates on external setVisibleLayers()
  * Fix dynamic noLegend bug with sublayers.
  * Add KML control.
  * Merge branch 'develop' into update/LayerControl-1.3.2

2014-11-20
==========

  * Merge pull request [#313](https://github.com/cmv/cmv-app/issues/313) from cmv/feature/1.3.2-nls
    Feature/1.3.2 nls
  * geocoder nls support
  * Merge branch 'develop' into 1.3.2/nls
  * nls support
    broke template string out into separate file
  * nls support
  * Merge pull request [#312](https://github.com/cmv/cmv-app/issues/312) from cmv/widget-updates/print-handle-async-errors
    Print Widget: handle async errors
  * missing semicolon
  * handle async errors

2014-11-14
==========

  * Merge pull request [#302](https://github.com/cmv/cmv-app/issues/302) from cmv/widget-updates/identify
    Identify Widget: nls support
