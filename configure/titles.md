# Titles Section of viewer.js

### Set Page Title, Header and Subheader
You can override the default titles in your `index.html`

``` javascript
titles: {
    header: 'Yours',
    subHeader: 'Mine!',
    pageTitle: 'Ours'
},
```

This offers flexibility if you want to deploy more than one CMV on your site by using a url to call different configs within different `viewer.js` files. For example http://YourServerName/viewer/?config=viewer2 to load a separate config file in config folder or to a completely different folder http://YourServerName/viewer/?config=./js/newconfig/viewer.js

