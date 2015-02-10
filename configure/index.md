# Configuration

Use the configuration files in the `/js/config` folder to customize your own map layers, task urls and widgets. The base configuration file is [viewer.js](configure/viewer) and the majority of your work will be here.

Sometimes the configuration object for a widget can be quite involved and length. In those cases, it often makes it easier to separate that widget's configuration into a separate file. Configurations for the [Basemaps](configure/basemaps) and [Identify](configure/identify) widgets are frequently maintained this way. 