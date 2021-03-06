# admesh-parser

[![Build Status](https://travis-ci.org/ArtskydJ/admesh-parser.svg?branch=master)](https://travis-ci.org/ArtskydJ/admesh-parser)

# description

This module returns a function that takes an STL file and returns a JavaScript object containing information about the file. 

# you can't use this until you download more stuff

To use this module, you will need [admesh](https://sites.google.com/a/varlog.com/www/admesh-htm). This module just parses admesh's output, it does not include admesh. (Well, technically, it does, in the test folder, but it only will work for windows.)

You will also need an STL file to run this on. Two files are included in the 'test' folder.

# install

Install with [NPM](http://nodejs.org)

	npm install admesh-parser

# api

```js
var AdmeshParser = require('admesh-parser')

var admeshParser = new AdmeshParser('C:\\Users\\Me\\NoWhiteSpace\\admesh.exe') //Admesh Directory
var admeshParser = new AdmeshParser('C:\\Users\\Me\\White space\\admesh.exe') //NO THIS WILL NOT WORK! (Note the space.)
var admeshParser = new AdmeshParser('"C:\\Users\\Me\\White space\\admesh.exe"') //This should work even with the space. (Note the double quotes.)
```

# `admeshParser(options, cb)`

### `options`
Must be an `Array` or a `String`.

If it is a `string`, it must be the input file directory.

If it is an `array`, the last element must be a string of the input file directory.

There are many options you can pass in. They are documented [here](http://www.varlog.com/admesh-htm/ADMESH_DOC.TXT?attredirects=0).

Valid forms of `options`:

```js
var options = [
	"--remove-unconnected",
	"--fill-holes",
	"C:\\Users\\Me\\Documents\\gear.stl"
]
```
or
```js
var options = ["C:\\Users\\Me\\Documents\\gear.stl"]
```
or
```js
var options =  "C:\\Users\\Me\\Documents\\gear.stl"
```

### `cb(err, result)`

- `err` is either `null`, or an `Error` object.
- `result` is an object if there is not an error. It should look like the following:

```js
{ x: { min: -1.334557, max: 1.370952 },
  y: { min: -1.377953, max: 1.37723 },
  z: { min: -1.373225, max: 1.242838 },
  facets: 
   { overall: { before: 3656, after: 3656 },
     disconnected1: { before: 18, after: 0 },
     disconnected2: { before: 3, after: 0 },
     disconnected3: { before: 0, after: 0 },
     disconnected: { before: 21, after: 0 },
     degenerate: 4,
     removed: 14,
     added: 3,
     reversed: 2 },
  edges: { fixed: 24, backwards: 0 },
  volume: 10.889216,
  parts: 1,
  normalsFixed: 12 }
```

# example

```js
var AdmeshParser = require('admesh-parser')
var admeshParser = new AdmeshParser('C:\\Users\\Me\\Documents\\admesh.exe') //Admesh Directory

var model = admeshParser("C:\\Users\\Me\\Documents\\gear.stl") //Options (model dir)

console.log("Number of parts: " + model.parts)
console.log("Min X: " + model.x.min)
console.log("Max X: " + model.x.max)
console.log("Num of facets, before: " + model.facets.overall.before)
console.log("Volume: " + model.volume)
```

# license

[MIT](http://opensource.org/licenses/MIT)
