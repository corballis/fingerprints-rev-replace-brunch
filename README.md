## fingerprints-rev-replace-brunch
Brunch plugin to replace reved asset URLs in compiled files.

[![Build Status](https://travis-ci.org/corballis/fingerprints-rev-replace-brunch.svg?branch=master)](https://travis-ci.org/corballis/fingerprints-rev-replace-brunch)
[![codecov](https://codecov.io/gh/corballis/fingerprints-rev-replace-brunch/branch/master/graph/badge.svg)](https://codecov.io/gh/corballis/fingerprints-rev-replace-brunch)

## Usage
Install the plugin via npm with `npm install --save-dev fingerprints-rev-replace-brunch`.

This plugin is intended to be used with [fingerprint-brunch](https://github.com/dlepaux/fingerprint-brunch). Please make
sure it is also installed.

This plugin will use the assets file generated by fingerprint-brunch to replace URLs in the contents of files.

## Configuration

Configure the plugin in the following section of your brunch-config file:

```
plugins: {
    fingerprintsRevReplace: {
            
    }
}
```

#### options.canonicalUris
Type: `boolean`

Default: `true`

Use canonical Uris when replacing filePaths. I.e. when working with file paths
with non forward slash (`/`) path separators, we replace them with forward slash.

#### options.replaceInExtensions
Type: `Array`

Default: `['.js', '.css', '.html']`

Only substitute in new file names in files of these types.

#### options.prefix
Type: `string`

Default: ``

Add the prefix string to each replacement.

#### options.manifest
Type: `string`

Default: `./public/assets.json`

The manifest file's path written out by the fingerprint-brunch plugin.

#### options.modifyUnreved, options.modifyReved
Type: `Function`

Modify the name of the unreved/reved files before using them. The file name is
passed to the function as the first argument.

For example, if in your manifest you have:

```js
{"js/app.js.map": "js/app-98adc164.js.map"}
```

If you wanted to get rid of the `js/` path just for `.map` files (because they
are sourcemaps and the references to them are relative, not absolute), you could
do the following:

```js
function replaceJsIfMap(filename) {
    if (filename.indexOf('.map') > -1) {
        return filename.replace('js/', '');
    }
    return filename;
}
```

And then in your brunch configuration:
```js
plugins: {
    fingerprintsRevReplace: {
        modifyUnreved: replaceJsIfMap,
        modifyReved: replaceJsIfMap    
    }
}
```

## Credits
This plugin was based on [gulp-rev-replace](https://github.com/jamesknelson/gulp-rev-replace).

## License

The MIT License (MIT)

Copyright (c) 2016 Corballis Consulting Ltd. (http://corballis.ie)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
