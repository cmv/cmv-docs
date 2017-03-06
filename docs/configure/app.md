# App Mixin and Config

In CMV, the application has been split into several different pieces. Each of these mixins can be customized to enable loading different sources of configs, different layout types, or even an entirely different dojo application.

In addition, new pieces can be added and replaced as necessary when building custom configurations of cmv.

The file `config/app.js` is used to bootstrap and load cmv's config, layout, map, and widgets. `app.js` loads the required components and creates a new application from the components. It uses `dojo/declare` to call each mixin's methods.

**The first mixins on the list will be the last ones called. In the example below, `_ControllerBase` is called first.**

```javascript
var App = declare([

    // add custom mixins here...note order may be important and
    // overriding certain methods incorrectly may break the app
    // First on the list are last called last, for instance the startup
    // method on _ControllerBase is called FIRST, and _LayoutMixin is called LAST
    // for the most part they are interchangeable, except _ConfigMixin
    // and _ControllerBase
    //
    _LayoutMixin,
    _WidgetsMixin,
    _MapMixin,

    // configMixin should be right before _ControllerBase so it is
    // called first to initialize the config object
    _ConfigMixin,

    // controller base needs to be last
    _ControllerBase
]);

// create an instance of the custom app
var app = new App({

  // options
});

// start the app 
app.startup();
```

## Mixin Methods

Each mixin may implement one or all of these methods depending on its needs. The cmv app loads in 3 stages:

1. Load Config - Load and modify the config by fetching any files necessary and perform any config validation
2. Post Config - The config has been loaded, perform any variable initialzing and pre-loading before the app starts up
3. Startup - Startup the map, widgets, layers, etc

### `loadConfig(wait)`

Loads or modify the config object before the app begins initializing. If the method performs any async processes, it should return pass a deferred to `this.inherited` and return the value of `this.inherited` or the deferred if null.

**Parameters:**

`wait` - an optional deferred object that needs to resolve before processing can continue to the current mixin.

**Returns:**

A deferred object or `this.inherited()`.

**Example:**

```javascript
loadConfig: function (wait) {

    // this will be used to make any inherited methods 'wait'
    var waitDeferred = new Deferred();

    if (wait) {

        // if we need to wait for a previous deferred
        // wait for it,
        wait.then(lang.hitch(this, function () {

          // do any config processing then resolve the waitDeferred

        }));
    } else {

      // do any config processing then resolve the waitDeferred

    }

    // call any inherited methods
    // pass our waitDeferred
    // or if the inherited returns nothing, return our deferred
    return this.inherited(arguments, [waitDeferred]) || waitDeferred;
},
```

### `postConfig(wait)`

A method that is run after all async config loading is finished. This method can startup widgets that need to load before the app starts or initialize any variables on the app. It is similar to the `loadConfig` function in that if the method performs any async processes, it should return pass a deferred to `this.inherited` and return the value of `this.inherited` or the deferred if null.

`loading` type widgets are loaded at this time.

**Parameters:**

`wait` - an optional deferred object that needs to resolve before processing can continue to the current mixin.

**Returns:**

The value of `this.inherited()` or a deferred object.

### `startup`

The startup method for the mixin. This is the final stage of loading the app.

## Default Mixin Details

The following mixins are provided with cmv by default.

### `_ControllerBase`

The base loading mixin. **This should come last in the list of mixins.**

### `_ConfigMixin`

The config loading logic.

**Options**

The following options are added by the default config mixin:

Key             | Type     | Description
--------------- | -------- | ----------------------------------------------------------------------------
`defaultConfig` | `String` | The name of the default config file to load. The default value is `'viewer'`

### `_LayoutMixin`

The mixin that sets up the layout and dom.

### `_MapMixin`

The mixin that sets up and loads the map and layers.
