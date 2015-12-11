# j2c-pocketgrid

A [j2c](http://j2c/py.gy) port of [PocketGrid](http://arnaudleray.github.io/pocketgrid/) v1.1.0.

IMO the best way to use grids with j2c.

## Installation

```Shell
$ npm install --save j2c-pocketgrid
```

## Usage

The wonderful [PocketGrid documentation](http://arnaudleray.github.io/pocketgrid/docs/) applies in full to `j2c-pocketgrid` as well. Learning to use PocketGrid means learning CSS, rather than non-portable grid framework knowledge.

This documentation assumes you want to create a scoped/localized grid.

```JavaScript
var j2c = require('j2c');
var grid = j2c.sheet(require('j2c-pocketgrid'));

// Put `grid` in a style element and add it to the DOM (see the j2c docs for the details).
```

Now you can use `grid.block` and `grid.blockgroup` as class names in your JS views (they hold the localized names. don't use literally `"grid.block"` and `"grid.blockgroup"` See [the j2c docs](https://github.com/pygy/j2c/#usage) for a longer explanation).

### IE <= 7 compatibility:

To work in prehistoric browsers, PocketGrid requires a `box-sizing: border-box;` polyfill. You can find one [in the PocketGrid repo](https://github.com/arnaudleray/pocketgrid/blob/master/js/boxsizing-pocketgrid.htc) (LGPL-licensed). Then, assuming you defined `grid` as above:

```JS
var compatgrid = j2c.sheet(grid, {
    ".blockgroup, .block": {
        "&, &:before, &:after": "*behavior: url(path/to/your/local/boxsizing-pocketgrid.htc);"
    }
});
```

Then insert `compatgrid` in a style element in the DOM.

This uses a [\*CSS hack](http://browserhacks.com/#hack-6d49e92634f26ae6d6e46b3ebc10019a) to restrict the polyfill to the appropriate targets. Other browsers will not download the file.

### ... and for a global style sheet?

```JavaScript
var j2c = require('j2c');
var grid = j2c.sheet({"@gobal": require('j2c-pocketgrid')});
var compatgrid = j2c.sheet({
    "@global": {
        ".block-group, .block": {
            "&, &:before, &:after": "*behavior: url(path/to/your/local/boxsizing-pocketgrid.htc);"
        }
    }
});
```

Then put `grid` or optionally `grid + compatgrid` in a style element and insert it in the DOM. Now you can use, literally, `'blockgroup'` and `'block'` as class names.

## License

MIT