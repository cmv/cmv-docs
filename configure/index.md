# Configuration

Use the configuration files in the `/js/config` folder to customize your own map layers, task urls and widgets. The base configuration file is [viewer.js](./viewer) and the majority of your work will be here.

Multiple cmv apps may be created by using several different config files, the default is `viewer.js`. This offers flexibility if you want to deploy more than one CMV on your site by using a url to call different configs within different `viewer.js` files. For example `http://YourServerName/viewer/?config=viewer2` to load a separate config file in config folder or to a completely different folder `http://YourServerName/viewer/?config=./js/newconfig/viewer`

Sometimes the configuration object for a widget can be quite involved and length. In those cases, it often makes it easier to separate that widget's configuration into a separate file. Configurations for the [Basemaps](./basemaps) and [Identify](./identify) widgets are frequently maintained this way.
