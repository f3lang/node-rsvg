# Node.JS Binding for LibRSVG with prebuilt binaries

**LibRSVG** is a SVG rendering library, which parses SVG files and renders them in various formats. The formats include:

 *  PNG
 *  PDF
 *  SVG
 *  Raw memory buffer image

This repository is fork of https://github.com/2gis/node-rsvg with prebuilt binaries. It will be rebased on a regular basis.
After spending days on getting the compilation to work under windows, i decided to publish prebuilt binaries of this project.

Currently available binary releases are:

| Node ABI Version | win32(ia32) | win32(x64) | darwin(ia32) | darwin(x64) | linux(ia32) | linux(x64) |
|:----------------:|:-----------:|:----------:|:------------:|:-----------:|:-----------:|:----------:|
|51                |:white_check_mark:|:white_check_mark:|:x:|:white_check_mark:|:x:|:white_check_mark:|
|48                |:x:          |:white_check_mark:|:x:|:white_check_mark:|:x:|:white_check_mark:|
|47                |:x:          |:white_check_mark:|:x:|:white_check_mark:|:x:|:white_check_mark:|
|46                |:x:          |:white_check_mark:|:x:|:white_check_mark:|:x:|:white_check_mark:|
|45                |:x:          |:white_check_mark:|:x:|:white_check_mark:|:x:|:white_check_mark:|
|44                |:x:          |:white_check_mark:|:x:|:white_check_mark:|:x:|:white_check_mark:|
|43                |:x:          |:white_check_mark:|:x:|:white_check_mark:|:x:|:white_check_mark:|
|42                |:x:          |:white_check_mark:|:x:|:white_check_mark:|:x:|:white_check_mark:|
|14                |:x:          |:white_check_mark:|:x:|:white_check_mark:|:x:|:white_check_mark:|
|11                |:x:          |:white_check_mark:|:x:|:white_check_mark:|:x:|:white_check_mark:|

## Contributing

You have a cool idea/feature/pull request? Great! But please head over to https://github.com/2gis/node-rsvg since all changes should be made there.

## Basic Usage

Here is a simple example. Look in `index.js` for more documentation.

```javascript
var Rsvg = require('librsvg').Rsvg;
var fs = require('fs');

// Create SVG render instance.
var svg = new Rsvg();

// When finishing reading SVG, render and save as PNG image.
svg.on('finish', function() {
  console.log('SVG width: ' + svg.width);
  console.log('SVG height: ' + svg.height);
  fs.writeFile('tiger.png', svg.render({
    format: 'png',
    width: 600,
    height: 400
  }).data);
});

// Stream SVG file into render instance.
fs.createReadStream('tiger.svg').pipe(svg);
```

## Possible breaking changes

Before v0.6.0 in case of error `getBaseURI` returned `null`.
Since v0.6.0 possibly breaking change was introduced: now `getBaseURI` method always returns string. In case of error an empty string is returned, so it might affect user code that relies on strict equality to `null`. 

## Installation

If you are not using windows, you nees to install the librsvg library first. You can find instructions for different operating systems below. After that, you simply run:

```bash
npm install librsvg-prebuilt
```

Library versions known to work:

 *  LibRSVG 2.26+
 *  Cairo 1.8.8+

#### Ubuntu:

```bash
sudo apt-get install librsvg2
```

#### RedHat / OpenSUSE:

```bash
sudo yum install librsvg2
```

#### Mac OS X:

```bash
brew install librsvg
```

If, after installing LibRSVG through homebrew you are experiencing issues installing this module, try manually exporting the package config with this command:

```bash
export PKG_CONFIG_PATH=/opt/X11/lib/pkgconfig
```

Then try reinstalling this module. For further information, [see this thread](https://github.com/Homebrew/homebrew/issues/14123).

#### Windows:

All nessecary files are bundled in the binary (yes, even the vc runtime)
