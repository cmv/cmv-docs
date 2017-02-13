2017-02-10
==========

  * Merge pull request [#666](https://github.com/cmv/cmv-app/issues/666) from roemhildtg/use-inherited-mixins
    Use inherited mixins
  * remove extra promiseAll reference
  * pass null to create 'all' widgets
  * Merge branch 'use-inherited-mixins' of https://github.com/roemhildtg/cmv-app into HEAD
  * Cleanup https://github.com/cmv/cmv-app/pull/666

2017-02-06
==========

  * Merge branch 'develop' into use-inherited-mixins
  * Merge pull request [#664](https://github.com/cmv/cmv-app/issues/664) from roemhildtg/identify-graphics-and-dynamic-layers
    Override api's default graphic identify function and identify dynamic layers additionally

2017-01-31
==========

  * reset viewer.js to develop
  * rename preStartup to postConfig for clarity
  * call `createPanes` when `mapDeferred` resolves
  * fix lint errors
  * fix lint error
  * Merge branch 'develop' into develop
  * Override api's default graphic identify function and identify dynamic layers additionally

2017-01-22
==========

  * Merge pull request [#663](https://github.com/cmv/cmv-app/issues/663) from cmv/feature/move-titlePane-icons-to-config
    Make the icons for the tilePanes configurable
  * Make the icons for the tilePanes configurable in viewer.js and remove the classes from the css.

2017-01-18
==========

  * add documentation and fix typo
  * remove console.log
  * override createMap method if mixin returns a deferred
    - as a result, order is not important with map/webmap mixins
  * use createMap method to allow mixins to modify map before resolving deferred

2017-01-17
==========

  * async loading of loadConfig and preStartup methods

2017-01-15
==========

  * implement an 'init' and 'startup' method in mixins and utilize deferreds for async ops

2017-01-09
==========

  * Merge pull request [#661](https://github.com/cmv/cmv-app/issues/661) from cmv/fix/adjustments-to-loading-pane-widgets
    Adjustments to loading of pane widgets
  * Make sure the first pane widget is at position 0 to avoid error.
  * correctly avoid the 'outer' and 'center' panes.
  * Ensure that all titlePane and contentPane widgets have a placeAt parameter so they are loaded first.
  * Merge pull request [#660](https://github.com/cmv/cmv-app/issues/660) from roemhildtg/fix-legend-layer-visibility
    FIX: update legend when maps `update-end` event is fired
  * Merge remote-tracking branch 'origin/develop' into develop
  * FIX: update legend when maps `update-end` event is fired
    - adds new gis/dijit/Legend widget from https://github.com/cmv/cmv-app/issues/659
    - fixes https://github.com/cmv/cmv-app/issues/340
    - fixes https://github.com/cmv/cmv-app/issues/294

2016-12-31
==========

  * Merge pull request [#655](https://github.com/cmv/cmv-app/issues/655) from cmv/feature/formatters-for-feature-layers
    Enable identify formatters for feature layers.

2016-12-25
==========

  * The Esri geometryEngine can mess with the geometry passed to it so we will clone it first.

2016-12-21
==========

  * Enable identify formatters for feature layers.
    Pass the feature geometry to formatter to allow for calculated area/length/position/etc.

2016-12-17
==========

  * Merge pull request [#652](https://github.com/cmv/cmv-app/issues/652) from cmv/fix/styling-esri-directions-print-button
    fix the styling of print button in the Esri directions widget
  * Merge branch 'develop' into fix/styling-esri-directions-print-button
  * Merge pull request [#651](https://github.com/cmv/cmv-app/issues/651) from cmv/feature/print-results-order
    Allow option for print results to sort from newest to oldest.
  * fix the styling of print button in the Esri directions widget
  * Merge branch 'develop' into feature/print-results-order
  * Merge pull request [#648](https://github.com/cmv/cmv-app/issues/648) from roemhildtg/identify-layer-add-topic
    make identify listen for new layer contol layer adds
  * allow option for print results to sort from newest to oldest.
    add a timestamp to title attribute of print results.

2016-12-11
==========

  * add missing jsdoc comments
  * make identify listen for new layer adds topic
  * Merge pull request [#649](https://github.com/cmv/cmv-app/issues/649) from cmv/feature/update-to-esri-jsapi-3.19
    Update to Esri JS API upcoming version 3.19
  * remove specific package references for put and xstyle. Esri now includes the updated versions with the JS API so the prior work-around is no longer necessary.
  * Update to proj4js version 2.3.15
  * update to Font-Awesome version 4.70
  * update to Esri JS API upcoming version 3.19

2016-12-04
==========

  * Merge pull request [#645](https://github.com/cmv/cmv-app/issues/645) from cmv/feature/add-widget-loading-indicator
    Add a simple loading indicator for titlePane and contentPane widgets.
  * Merge branch 'develop' into feature/add-widget-loading-indicator
  * Merge pull request [#644](https://github.com/cmv/cmv-app/issues/644) from cmv/fixes/adjust-streeview-stylesheet
    Fix StreetView Stylesheet and allow Google API version to be configured.
  * Merge branch 'develop' into fixes/adjust-streeview-stylesheet
  * Merge pull request [#643](https://github.com/cmv/cmv-app/issues/643) from cmv/feature/new-widget-types
    adds 3 new widget types: loading, layout and layer.

2016-12-03
==========

  * Add a simple loading indicator for titlePane and contentPane widgets.

2016-12-02
==========

  * Add position:relative to the widget's container div so the absolutely positioned button doesn't appear at the top of the page.
    All the version of the Google API to be set in the app configuration file.
  * remove some braces that should not have been there.
  * adds 3 new widget types: loading, layout and layer.
    adds 3 new entry points within the Controller when widgets can be created.
    use the widget's key internally when no id is available

2016-11-18
==========

  * Merge pull request [#634](https://github.com/cmv/cmv-app/issues/634) from cmv/fix/add-back-basemaps-widget-config
    basemaps widget config should not have been removed from viewer.js
  * basemaps widget config should not have been removed from viewer.js

2016-11-15
==========

  * Merge pull request [#632](https://github.com/cmv/cmv-app/issues/632) from roemhildtg/fix-628-contentPane-sidebar
    fixes https://github.com/cmv/cmv-app/issues/628
  * fixes https://github.com/cmv/cmv-app/issues/628

2016-11-01
==========

  * Merge pull request [#626](https://github.com/cmv/cmv-app/issues/626) from cmv/feature/add-support-for-webmaps
    Add support for webmaps
  * Merge branch 'develop' into feature/add-support-for-webmaps
  * Merge pull request [#625](https://github.com/cmv/cmv-app/issues/625) from cmv/feature/add-basemap-gallery-widget
    Add new basemap gallery widget
  * Merge branch 'develop' into feature/add-basemap-gallery-widget
  * Merge pull request [#624](https://github.com/cmv/cmv-app/issues/624) from cmv/feature/basemap-widget-combine-all-basemaps-as-one
    basemap widget - support custom and agol basemaps at the same time

2016-10-31
==========

  * Add support for webmaps
  * support combined custom and agol basemaps. `mode` is no longer necessary.
  * include custom basemap as example.
  * Let Esri handle the i18n title for Esri basemaps. Still can be overridden in config

2016-10-30
==========

  * new BasemapGallery widget
  * cleanup the bottom border for titlepanes
  * Merge pull request [#622](https://github.com/cmv/cmv-app/issues/622) from cmv/fix/floating-titlepane-chrome-55
    Fix titlePane issue effecting IE 11/M.S. Edge and now Chrome v 55
  * Merge branch 'develop' into fix/floating-titlepane-chrome-55
  * Merge pull request [#621](https://github.com/cmv/cmv-app/issues/621) from cmv/fix/identify-widget-checkVisibilityRecursive-use-sublayer's-id
    Identify widget - account for hard-coded sublayer IDs in checkVisibilityRecursive

2016-10-29
==========

  * Account for hard-coded sublayer IDs
    the id may not be the same as the index.to layerInfos array
  * fix issue in dojo mover class causing IE and now Chrome v 55 to not let go of the titlePane when mouse is released.

2016-10-09
==========

  * Merge pull request [#618](https://github.com/cmv/cmv-app/issues/618) from roemhildtg/proposal-custom-identify-formatter
    Add the ability to add custom field formatters
  * Cleanup
  * Mixin default popup template options with user provided options.
  * adds default formatters where possible
  * Fix indent
  * Merge remote-tracking branch 'origin/develop' into proposal-custom-identify-formatter

2016-10-08
==========

  * Add the ability to add custom field formatters
  * Merge pull request [#617](https://github.com/cmv/cmv-app/issues/617) from roemhildtg/fix-603-sublayer-menu
    Fixes sublayer menu not appearing for single dynamic layer
  * Fix linting issues.

2016-10-07
==========

  * fix typo
  * Fixes https://github.com/cmv/cmv-app/issues/603 and adds menu examples in viewer config

2016-10-05
==========

  * Merge pull request [#613](https://github.com/cmv/cmv-app/issues/613) from roemhildtg/fix-broken-pane-toggle
    Fix broken pane toggle
  * add third argument suppressEvent to togglePane function
  * Merge remote-tracking branch 'origin/develop' into fix-broken-pane-toggle
  * Merge pull request [#615](https://github.com/cmv/cmv-app/issues/615) from cmv/feature/make-flat-theme-the-default
    Make dojo flat the default theme
  * Merge branch 'develop' into feature/make-flat-theme-the-default
  * Merge pull request [#614](https://github.com/cmv/cmv-app/issues/614) from cmv/fix/revert-using-our-own-drag-delay
    remove use of our own (unreliable) drag delay for floating windows

2016-10-04
==========

  * 2 adjustments to theme css.
  * switch to flat theme
  * this removes the use of our own (unreliable) drag delay for floating windows.
    dojo included with ESRI JS API 3.17+ adds detection for MS Edge browser so
    we can use that as a more reliable approach to solving the original issue [#379](https://github.com/cmv/cmv-app/issues/379)
    with dragging floating windows in Internet Explorer and Edge browsers.
  * Fix broken toggle pane buttons

2016-10-03
==========

  * Merge pull request [#609](https://github.com/cmv/cmv-app/issues/609) from cmv/feature/update-package.json-for-2.0.0-beta.1
    update package dependencies and bump the version number.

2016-10-02
==========

  * update package dependencies and bump the version number.
  * Merge pull request [#608](https://github.com/cmv/cmv-app/issues/608) from roemhildtg/fix-find-widget-missing-button
    Add missing require for Find widget which periodically causes WidgetsInTemplate error
  * Merge branch 'develop' into fix-find-widget-missing-button
