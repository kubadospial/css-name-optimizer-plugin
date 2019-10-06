# css-name-optimizer-plugin

This is a webpack plugin for Angular to optimize CSS class names to 6 random charactes in patern of "\_AbcDe". This helps to decrease the size of output style file by reducing number of characters.

---

This plugin is compatibile with Angular 7 and up.

### Example output:

![alt text](https://user-images.githubusercontent.com/24934035/66254740-03aa5900-e77b-11e9-8511-17ebb751de3a.png)

```
** NOTE **
Plugin wil run only when you build/serve app with --prod flag!!!
If You use CDN styles then plugin won't remap class names.
We're working on Chrome extension to revert css mapping on production environment for development purposes.
```

# How to use

To use this plugin you need to:

- add custom webpack config
  [alligator.io: Custom webpack config](https://alligator.io/angular/custom-webpack-config/).
- create webpack.config.js:

```js
var CssNameOptimizerPlugin = require("./node_modules/css-name-optimizer-plugin");

module.exports = {
  plugins: [new CssNameOptimizerPlugin()]
};
```

You can pass options to the plugin:

```js
var CssNameOptimizerPlugin = require("./node_modules/css-name-optimizer-plugin");

// object below represents default state of options
var options = {
    isSourceMapEnabled = false,
    sourceMapPath = "./",
    isSourceMapNameVersioned: false,
    isVerboseEnabled: false
};

module.exports = {
  plugins: [
      new CssNameOptimizerPlugin(options)
  ]
};
```

# Options

plugin can generate a map of changed css classes

```js
options.isSourceMapEnabled

// map example:
{
  "tag-pill": "_kVFrc",
  "page-link": "_pbKeX",
  "logo-font": "_NOVyt",
  "test": "_xVkLe",
  "red": "_tqsTf",
  "dark": "_NoMhS"
}
// { originalName: generatedName }
```

you can provide path relatively to project folder

```
options.sourceMapPath
```

to avoid overwritting source map, timestamp can be added to file name

```js
options.isSourceMapNameVersioned;

// when false: css-name.map.json
// when true: css-name.1570282598325.map.json
```

if true you will see which classes aren't remapped

```js
options.isVerboseEnabled;

// verbose example:
// *** [CssNameOptimizer]: Cannot find .form-control-lg in CSS/SCSS files. It might be a vendor's class or it isn't used. It won't be optimized. ***
```
