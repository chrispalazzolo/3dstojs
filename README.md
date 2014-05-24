3dstojs
=======

A nodejs module to parses .3ds files to js or JSON.

Overview
--------
Parse 3D Studio file (.3ds) to a javascript object or JSON.

Option to save the parsed data to a JSON file or break down the data to segments and save each segment to it's own JSON file (Materials, Objects/Mesh, Key Framer, etc...).

Due to .3ds file specifications not being public this parse does not parse everything in a .3ds file.  To help with unknown chunks logs can be created during parsing and configured to capture unparseable to help update parsing ability.

Installation
------------
> npm install 3dstojs

Usage:
-------
Returns a js object.
```javascript
var parser = require("3dstojs");
var data = parser.parse("C:/3d/models/sample.3ds");
```
Returns a JSON string.
```javascript
var parser = require("3dstojs");
var jsonStr = parser.parseToJson("C:/3d/models/sample.3ds");
```

Note: Both `parse()` and `parseToJson()` are synchronous calls

Methods
-------
Parse - Takes in a filepath and optional options object.  Returns a js objected of the parsed data. Options to save JSON and log information to a file. For options See below

`parse(file, [options])`

ParseToJson - Takes in a filepath and optional options.  Returns a JSON string of the parsed data. Options to save JSON and log information to a file.  For Options see below.

`parseToJson(file, [options])`

Help - Writes help text to the console.  Same content as what is found in the "Options" section below.

`help()`

Parameters
----------
These are the parameters for methods...

`parse(file, options)` and `parseToJson(file, options)`

file - <string> - full path to the .3ds file.");
options - <object> - flags for events such as logging, saving to JSON files, etc...

Options
-------
Is a js object that contains configurations for logging, saving JSON files, etc...

saveJson - `bool` (default: `false`) - flag to save parsed object to a JSON file.<br />
saveOptions - `object` - Contains the following properties for saving to files (JSON, log, etc...)<br />
&nbsp;path - `string` (default: `string` directory of 3ds file.) - Location to save files.<br />
&nbsp;jsonPerItem - `bool` (default: `false`) - Save objects as separate JSON files.<br />
&nbsp;unparsedToFile - `bool` (default: `false`) - Saves the unparsable chunk to a file.<br />
logging - `bool` (default: `false`) - Creates a log file of parsing events.<br />
logOptions - `object` - Contains the follow flags on what is to be logged.<br />
&nbsp;read - `bool` (default: `true`) - Logs header chunks read from the file.<br />
&nbsp;parsing - `bool` (default: `true`) - Logs parsing of identifiable chunks.<br />
&nbsp;unparsed - `bool` (default: `true`) - Logs identifiable ids but not enough info to parse.<br />
&nbsp;unknown - `bool` (default: `true`) - Logs unknown chunk ids.<br />
&nbsp;jumping - `bool` (default: `false`) - Logs any position movement in the read file.<br />
&nbsp;files - `bool` (default: `true`) - Logs the json files saved to disk.<br />
verbose - `bool` (default: `false`) - Prints the parsing progress and stats to the console.<br />
verboseOptions - `object` - Contains the follow flags on what to write to the console.<br />
&nbsp;onlyStats: `bool` (default: `false`) - Shows only the stats on completion.<br />
trackUnparsed - `bool` (default: `false`) - returns an object

Default Option object if the options parameter is omitted...
```javascript
options = {
  saveJson: false,
  saveOptions:{
	  path: '<directory of 3ds file>',
	  jsonPerItem: false,
	  unparsedToFile: false
 	},
 	logging: false,
  logOptions:{
	  read: true,
    parsing: true,
    unparsed: true,
    unknown: true,
    jumping: false,
    files: true
  },
 	verbose: false,
 	verboseOptions:{
	  onlyStats: false
 	},
  trackUnparsed: false
}
```

Notes
-----
Since the .3ds file format isn't publicly available this parser might not parse all data in your .3ds file.  If you feel like not all of the data in the file was parse; use the `options` parameter to help figure out what chunks were not parsed.

The best option setup for unparsed/unkown chunks:
```javascript
var options = {
  saveToJson: true,
  saveOptions: {
    unparsedToFile:true
  },
  logging: true,
  logOptions: {
    unparsed: true,
    unknown: true
  }
}
```

License
-------
MIT
