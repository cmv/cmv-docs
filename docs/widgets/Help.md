# Help

##Available Options

| Property name         | Type      | Description                              |
|-----------------------|-----------|------------------------------------------|
| draggable             | boolean   | Enables dragging of the help window      |
| domTarget             | string    | Id of the dom node to place the help link|
| html                  | string    | HTML for the help link                   |
| title                 | string    | Title for the help dialog                |

## Example config

```javascript
help: {
    include: true,
    id: 'help',
    type: 'floating',
    path: 'gis/dijit/Help',
    title: 'Help',
    options: {}
}
```
