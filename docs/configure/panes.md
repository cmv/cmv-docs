# Panes Section of viewer.js

Basic guide for placing widgets in panes

First add a bottom pane. Something like this near the top of your `viewer.js`:

``` javascript
panes: {
    left: {
        id: 'sidebarLeft',
        placeAt: 'outer',
        collapsible: true,
        region: 'left'
    },
    bottom: {
        id: 'sidebarBottom',
        placeAt: 'outer',
        splitter: true,
        collapsible: true,
        region: 'bottom'
    }
},
```

Then place your widget there by using `placeAt` in the widget options:

```javascript
widget: {
    ...
    type: 'contentPane',
    placeAt: 'bottom'
}
```

That will work for widgets of type `titlePane` and `contentPane`. If you want to use a type of `domNode` you need some content in your pane to attach to:

```javascript
content: '<div id="myWidgetContainer"></div>'
```

Then include the reference to that domNode in the widget options:

```javascript
widget: {
    ...
    type: 'domNode',
    srcNodeRef: 'myWidgetContainer'
}
```

There are some gotchas when using dijits like a TabContainer dijit. Here's a discussion about using a TabContainer that also touches on the widget placement in panes: [Gitub #214](https://github.com/cmv/cmv-app/issues/214)
