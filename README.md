# browser-tiff.js

browser-tiff.js is a direct clone of tiff.js, but with require() methods removed, so it can work without errors during 'import' and compilation for web projects.

Below are the only changes to tiff.min.js, basically Function.prototype() act like noop()

From:

```js
... = require(...)

```
To:

```js
... = Function.prototype(...)

```

## Example Usage in Angular

1. Copy browser-tiff.d.ts to your project root folder (This is for Typescript type definition)
2. In your Angular component, use import like this:
```js
import * as Tiff from 'browser-tiff.js';
```   
3. Use normally as describe in original tiff.js usage below.


# Original tiff.js Readme below


# tiff.js

tiff.js is a port of the LibTIFF by compiling the LibTIFF C code with Emscripten.

## [Demo](http://seikichi.github.io/tiff.js/)

- [view TIFF files](http://seikichi.github.io/tiff.js/basic.html)
- [view a TIFF file using a web worker](http://seikichi.github.io/tiff.js/worker.html)
- [view a multipage TIFF file](http://seikichi.github.io/tiff.js/multipage.html)
- [view your TIFF file](http://seikichi.github.io/tiff.js/upload.html)

## Usage

### Browser

Download tiff.min.js and load the script by yourself:

```js
var xhr = new XMLHttpRequest();
xhr.responseType = 'arraybuffer';
xhr.open('GET', "url/of/a/tiff/image/file.tiff");
xhr.onload = function (e) {
  var tiff = new Tiff({buffer: xhr.response});
  var canvas = tiff.toCanvas();
  document.body.append(canvas);
};
xhr.send();
```

### Node.js

```sh
$ npm install tiff.js
```

Example

```js
// Usage: node this-file.js input.tiff
var Tiff = require('tiff.js');
var fs = require('fs');

var filename = process.argv[2];
var input = fs.readFileSync(filename);
var image = new Tiff({ buffer: input });
console.log(filename + ': width = ' + image.width() + ', height = ' + image.height());
```

## API

see tiff.d.ts

## Note

- ~~This library does not support JPEG-based compressed TIFF files~~
  - Fixed by [Tetedeiench](https://github.com/seikichi/tiff.js/issues/15#issuecomment-257103842)
- When you load large tiff file, you will see the error message "Cannot enlarge memory arrays in asm.js"
  - in such case, please call 'Tiff.initialize({TOTAL_MEMORY: ... })' before you create a Tiff instance
- This JavaScript library uses only some parts of the LibTIFF features
  - To be more precise, I use following functions only
  - TIFFOpen, TIFFClose, TIFFGetField, TIFFReadRGBAImage, TIFFSetDirectory, TIFFCurrentDirectory, TIFFReadDirectory

## Alternatives

- [photopea/UTIF.js](https://github.com/photopea/UTIF.js)
- [image-js/tiff](https://github.com/image-js/tiff)

## License

The LibTIFF is LibTIFF Software License, zlib and additional code are zlib License.
