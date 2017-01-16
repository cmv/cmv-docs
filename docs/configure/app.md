# App Mixin and Config

In CMV, the application has been split into several different pieces. Each of these
mixins can be customized to enable loading different sources of configs, different
layout types, or even an entirely different dojo application.

#### Controller Base

The base loading mixin. This should generally come first in the list of mixins.

#### Config Mixin

The config loading logic.

#### Layout Mixin

The mixin that sets up the layout and dom.

#### Map Mixin

The mixin that sets up and loads the map and layers. 
