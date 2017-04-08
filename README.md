# api documentation for  argv (v0.0.2)  [![npm package](https://img.shields.io/npm/v/npmdoc-argv.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-argv) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-argv.svg)](https://travis-ci.org/npmdoc/node-npmdoc-argv)
#### CLI Argument Parser

[![NPM](https://nodei.co/npm/argv.png?downloads=true)](https://www.npmjs.com/package/argv)

[![apidoc](https://npmdoc.github.io/node-npmdoc-argv/build/screenCapture.buildNpmdoc.browser.%252Fhome%252Ftravis%252Fbuild%252Fnpmdoc%252Fnode-npmdoc-argv%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-argv/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-argv/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-argv/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Corey Hart",
        "email": "corey@codenothing.com"
    },
    "dependencies": {},
    "description": "CLI Argument Parser",
    "devDependencies": {
        "munit": "0.0.5",
        "nlint": "0.0.4"
    },
    "directories": {},
    "dist": {
        "shasum": "ecbd16f8949b157183711b1bda334f37840185ab",
        "tarball": "https://registry.npmjs.org/argv/-/argv-0.0.2.tgz"
    },
    "engines": {
        "node": ">=0.6.10"
    },
    "keywords": [
        "cli",
        "argv",
        "options"
    ],
    "main": "./index.js",
    "maintainers": [
        {
            "name": "codenothing",
            "email": "corey@codenothing.com"
        }
    ],
    "name": "argv",
    "optionalDependencies": {},
    "readme": "# argv\n\nargv is a nodejs module that does command line argument parsing.  \n  \n[![Build Status](https://travis-ci.org/codenothing/argv.png?branch=master)](https://travis-ci.org/codenothing/argv)  \n\n### Installation\n\n'''bash\n$ npm install argv\n'''\n\n\n### Usage\n\n'''js\nvar argv = require( 'argv' );\nvar args = argv.option( options ).run();\n-> { targets: [], options: {} }\n'''\n\n\n### Run\n\nRuns the argument parser on the global arguments. Custom arguments array can be used by passing into this method\n\n'''js\n// Parses default arguments 'process.argv.slice( 2 )'\nargv.run();\n\n// Parses array instead\nargv.run([ '--option=123', '-o', '123' ]);\n'''\n\n\n### Options\n\nargv is a strict argument parser, which means all options must be defined before parsing starts.\n\n'''js\nargv.option({\n\tname: 'option',\n\tshort: 'o',\n\ttype: 'string',\n\tdescription: 'Defines an option for your script',\n\texample: \"'script --opiton=value' or 'script -o value'\"\n});\n'''\n\n\n### Modules\n\nModules are nested commands for more complicated scripts. Each module has it's own set of options that\nhave to be defined independently of the root options.\n\n'''js\nargv.mod({\n\tmod: 'module',\n\tdescription: 'Description of what the module is used for',\n\toptions: [ list of options ]\n});\n'''\n\n\n### Types\n\nTypes convert option values to useful js objects. They are defined along with each option.\n\n* **string**: Ensure values are strings\n* **path**: Converts value into a fully resolved path.\n* **int**: Converts value into an integer\n* **float**: Converts value into a float number\n* **boolean**: Converts value into a boolean object. 'true' and '1' are converted to true, everything else is false.\n* **csv**: Converts value into an array by splitting on comma's.\n* **list**: Allows for option to be defined multiple times, and each value added to an array\n* **[list|csv],[type]**: Combo type that allows you to create a list or csv and convert each individual value into a type.\n\n'''js\nargv.option([\n\t{\n\t\tname: 'option',\n\t\ttype: 'csv,int'\n\t},\n\t{\n\t\tname: 'path',\n\t\tshort: 'p',\n\t\ttype: 'list,path'\n\t}\n]);\n\n// csv and int combo\n$ script --option=123,456.001,789.01\n-> option: [ 123, 456, 789 ]\n\n// list and path combo\n$ script -p /path/to/file1 -p /path/to/file2\n-> option: [ '/path/to/file1', '/path/to/file2' ]\n'''\n\nYou can also create your own custom type for special conversions.\n\n'''js\nargv.type( 'squared', function( value ) {\n\tvalue = parseFloat( value );\n\treturn value * value;\n});\n\nargv.option({\n\tname: 'square',\n\tshort: 's',\n\ttype: 'squared'\n});\n\n$ script -s 2\n-> 4\n'''\n\n\n### Version\n\nDefining the scripts version number will add the version option and print it out when asked.\n\n'''js\nargv.version( 'v1.0' );\n\n$ script --version\nv1.0\n\n'''\n\n\n### Info\n\nCustom information can be displayed at the top of the help printout using this method\n\n'''js\nargv.info( 'Special script info' );\n\n$ script --help\n\nSpecial script info\n\n... Rest of Help Doc ...\n'''\n\n\n### Clear\n\nIf you have competing scripts accessing the argv object, you can clear out any previous options that may have been set.\n\n'''js\nargv.clear().option( [new options] );\n'''\n\n\n### Help\n\nargv injects a default help option initially and on clears. The help() method triggers the help printout.\n\n'''js\nargv.help();\n'''\n\n----\n### License\n\n'''\nThe MIT License\n\nCopyright (c) 2012-2013 Corey Hart\n\nPermission is hereby granted, free of charge, to any person obtaining a copy\nof this software and associated documentation files (the \"Software\"), to deal\nin the Software without restriction, including without limitation the rights\nto use, copy, modify, merge, publish, distribute, sublicense, and/or sell\ncopies of the Software, and to permit persons to whom the Software is\nfurnished to do so, subject to the following conditions:\n\nThe above copyright notice and this permission notice shall be included in\nall copies or substantial portions of the Software.\n\nTHE SOFTWARE IS PROVIDED \"AS IS\", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR\nIMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,\nFITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE\nAUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER\nLIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,\nOUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN\nTHE SOFTWARE.\n'''\n",
    "readmeFilename": "README.md",
    "scripts": {
        "test": "make test"
    },
    "url": "http://codenothing.github.com/argv/",
    "version": "0.0.2"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module argv](#apidoc.module.argv)
1.  [function <span class="apidocSignatureSpan">argv.</span>_run ( argv )](#apidoc.element.argv._run)
1.  [function <span class="apidocSignatureSpan">argv.</span>clear ()](#apidoc.element.argv.clear)
1.  [function <span class="apidocSignatureSpan">argv.</span>help ( mod )](#apidoc.element.argv.help)
1.  [function <span class="apidocSignatureSpan">argv.</span>info ( mod, description )](#apidoc.element.argv.info)
1.  [function <span class="apidocSignatureSpan">argv.</span>isArray ()](#apidoc.element.argv.isArray)
1.  [function <span class="apidocSignatureSpan">argv.</span>isBoolean ( object )](#apidoc.element.argv.isBoolean)
1.  [function <span class="apidocSignatureSpan">argv.</span>isDate ( object )](#apidoc.element.argv.isDate)
1.  [function <span class="apidocSignatureSpan">argv.</span>isError ( object )](#apidoc.element.argv.isError)
1.  [function <span class="apidocSignatureSpan">argv.</span>isFunction ( object )](#apidoc.element.argv.isFunction)
1.  [function <span class="apidocSignatureSpan">argv.</span>isNumber ( object )](#apidoc.element.argv.isNumber)
1.  [function <span class="apidocSignatureSpan">argv.</span>isObject ( object )](#apidoc.element.argv.isObject)
1.  [function <span class="apidocSignatureSpan">argv.</span>isRegExp ( object )](#apidoc.element.argv.isRegExp)
1.  [function <span class="apidocSignatureSpan">argv.</span>isString ( object )](#apidoc.element.argv.isString)
1.  [function <span class="apidocSignatureSpan">argv.</span>mod ( object )](#apidoc.element.argv.mod)
1.  [function <span class="apidocSignatureSpan">argv.</span>option ( mod, object )](#apidoc.element.argv.option)
1.  [function <span class="apidocSignatureSpan">argv.</span>run ( argv )](#apidoc.element.argv.run)
1.  [function <span class="apidocSignatureSpan">argv.</span>type ( name, callback )](#apidoc.element.argv.type)
1.  [function <span class="apidocSignatureSpan">argv.</span>version ( v )](#apidoc.element.argv.version)
1.  object <span class="apidocSignatureSpan">argv.</span>mods
1.  object <span class="apidocSignatureSpan">argv.</span>options
1.  object <span class="apidocSignatureSpan">argv.</span>short
1.  object <span class="apidocSignatureSpan">argv.</span>types
1.  string <span class="apidocSignatureSpan">argv.</span>description
1.  string <span class="apidocSignatureSpan">argv.</span>name

#### [module argv.types](#apidoc.module.argv.types)
1.  [function <span class="apidocSignatureSpan">argv.types.</span>boolean ( value )](#apidoc.element.argv.types.boolean)
1.  [function <span class="apidocSignatureSpan">argv.types.</span>csv ( value )](#apidoc.element.argv.types.csv)
1.  [function <span class="apidocSignatureSpan">argv.types.</span>float ( value )](#apidoc.element.argv.types.float)
1.  [function <span class="apidocSignatureSpan">argv.types.</span>int ( value )](#apidoc.element.argv.types.int)
1.  [function <span class="apidocSignatureSpan">argv.types.</span>list ( value, name, options )](#apidoc.element.argv.types.list)
1.  [function <span class="apidocSignatureSpan">argv.types.</span>listcsv-combo ( type )](#apidoc.element.argv.types.listcsv-combo)
1.  [function <span class="apidocSignatureSpan">argv.types.</span>path ( value )](#apidoc.element.argv.types.path)
1.  [function <span class="apidocSignatureSpan">argv.types.</span>string ( value )](#apidoc.element.argv.types.string)



# <a name="apidoc.module.argv"></a>[module argv](#apidoc.module.argv)

#### <a name="apidoc.element.argv._run"></a>[function <span class="apidocSignatureSpan">argv.</span>_run ( argv )](#apidoc.element.argv._run)
- description and source-code
```javascript
_run = function ( argv ) {
		var args = { targets: [], options: {} },
			opts = self.options,
			shortOpts = self.short,
			skip = false;

		// Allow for passing of arguments list
		argv = self.isArray( argv ) ? argv : process.argv.slice( 2 );

		// Switch to module's options when used
		if ( argv.length && ristarget.exec( argv[ 0 ] ) && self.mods[ argv[ 0 ] ] ) {
			args.mod = argv.shift();
			opts = self.mods[ args.mod ].options;
			shortOpts = self.mods[ args.mod ].short;
		}

		// Iterate over arguments
		argv.forEach(function( arg, i ) {
			var peek = argv[ i + 1 ], option, index, value;

			// Allow skipping of arguments
			if ( skip ) {
				return ( skip = false );
			}
			// Full option '--option'
			else if ( rddash.exec( arg ) ) {
				arg = arg.replace( rddash, '' );

				// Default no value to true
				if ( ( index = arg.indexOf( '=' ) ) !== -1 ) {
					value = arg.substr( index + 1 );
					arg = arg.substr( 0, index );
				}
				else {
					value = 'true';
				}

				// Be strict, if option doesn't exist, throw and error
				if ( ! ( option = opts[ arg ] ) ) {
					throw "Option '--" + arg + "' not supported";
				}

				// Send through type converter
				args.options[ arg ] = option.type( value, arg, args.options, args );

				// Trigger onset callback when option is set
				if ( self.isFunction( option.onset ) ) {
					option.onset( args );
				}
			}
			// Shorthand option '-o'
			else if ( rdash.exec( arg ) ) {
				arg = arg.replace( rdash, '' );

				if ( arg.length > 1 ) {
					arg.split( '' ).forEach(function( character ) {
						if ( ! ( option = shortOpts[ character ] ) ) {
							throw "Option '-" + character + "' not supported";
						}

						args.options[ option.name ] = option.type( 'true', option.name, args.options, args );
					});
				}
				else {
					// Ensure that an option exists
					if ( ! ( option = shortOpts[ arg ] ) ) {
						throw "Option '-" + arg + "' not supported";
					}

					// Check next option for target association
					if ( peek && option.test && option.test( peek, option.name, args.options, args ) ) {
						value = peek;
						skip = true;
					}
					else if ( peek && ! option.test && ristarget.exec( peek ) ) {
						value = peek;
						skip = true;
					}
					else {
						value = 'true';
					}

					// Convert it
					args.options[ option.name ] = option.type( value, option.name, args.options, args );

					// Trigger onset callback when option is set
					if ( self.isFunction( option.onset ) ) {
						option.onset( args );
					}
				}
			}
			// Targets
			else {
				args.targets.push( arg );
			}
		});

		return args;
	}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.argv.clear"></a>[function <span class="apidocSignatureSpan">argv.</span>clear ()](#apidoc.element.argv.clear)
- description and source-code
```javascript
clear = function (){
		var version = self.options.version;

		// Clean out modes and reapply help option
		self.short = {};
		self.options = {};
		self.mods = {};
		self.option( helpOption );

		// Re-apply version if set
		if ( version ) {
			self.option( version );
		}

		return self;
	}
```
- example usage
```shell
...


### Clear

If you have competing scripts accessing the argv object, you can clear out any previous options that may have been set.

'''js
argv.clear().option( [new options] );
'''


### Help

argv injects a default help option initially and on clears. The help() method triggers the help printout.
...
```

#### <a name="apidoc.element.argv.help"></a>[function <span class="apidocSignatureSpan">argv.</span>help ( mod )](#apidoc.element.argv.help)
- description and source-code
```javascript
help = function ( mod ) {
		var output = [], name, option;

		// Printing out just a module's definitions
		if ( mod && ( mod = self.mods[ mod ] ) ) {
			output = [ '', mod.description, '' ];

			for ( name in mod.options ) {
				option = mod.options[ name ];

				output.push( "\t--" +option.name + ( option.short ? ', -' + option.short : '' ) );
				output.push( "\t\t" + option.description );
				if ( option.example ) {
					output.push( "\t\t" + option.example );
				}

				// Spacing
				output.push( "" );
			}
		}
		// Printing out just the root options
		else {
			output = [ '', self.description, '' ];

			for ( name in self.options ) {
				option = self.options[ name ];

				output.push( "\t--" +option.name + ( option.short ? ', -' + option.short : '' ) );
				output.push( "\t\t" + option.description );
				if ( option.example ) {
					output.push( "\t\t" + option.example );
				}

				// Spacing
				output.push( "" );
			}
		}

		// Print out the output
		console.log( output.join( "\n" ) + "\n\n" );
		return self;
	}
```
- example usage
```shell
...


### Help

argv injects a default help option initially and on clears. The help() method triggers the help printout.

'''js
argv.help();
'''

----
### License

'''
The MIT License
...
```

#### <a name="apidoc.element.argv.info"></a>[function <span class="apidocSignatureSpan">argv.</span>info ( mod, description )](#apidoc.element.argv.info)
- description and source-code
```javascript
info = function ( mod, description ) {
		if ( description === undefined ) {
			self.description = mod;
		}
		else if ( self.mods[ mod ] ) {
			self.mods[ mod ] = description;
		}

		return self;
	}
```
- example usage
```shell
...


### Info

Custom information can be displayed at the top of the help printout using this method

'''js
argv.info( 'Special script info' );

$ script --help

Special script info

... Rest of Help Doc ...
'''
...
```

#### <a name="apidoc.element.argv.isArray"></a>[function <span class="apidocSignatureSpan">argv.</span>isArray ()](#apidoc.element.argv.isArray)
- description and source-code
```javascript
function isArray() { [native code] }
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.argv.isBoolean"></a>[function <span class="apidocSignatureSpan">argv.</span>isBoolean ( object )](#apidoc.element.argv.isBoolean)
- description and source-code
```javascript
isBoolean = function ( object ) {
		return object !== undefined && object !== null && toString.call( object ) == match;
	}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.argv.isDate"></a>[function <span class="apidocSignatureSpan">argv.</span>isDate ( object )](#apidoc.element.argv.isDate)
- description and source-code
```javascript
isDate = function ( object ) {
		return object !== undefined && object !== null && toString.call( object ) == match;
	}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.argv.isError"></a>[function <span class="apidocSignatureSpan">argv.</span>isError ( object )](#apidoc.element.argv.isError)
- description and source-code
```javascript
isError = function ( object ) {
			return object && ( object instanceof Error );
		}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.argv.isFunction"></a>[function <span class="apidocSignatureSpan">argv.</span>isFunction ( object )](#apidoc.element.argv.isFunction)
- description and source-code
```javascript
isFunction = function ( object ) {
		return object !== undefined && object !== null && toString.call( object ) == match;
	}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.argv.isNumber"></a>[function <span class="apidocSignatureSpan">argv.</span>isNumber ( object )](#apidoc.element.argv.isNumber)
- description and source-code
```javascript
isNumber = function ( object ) {
		return object !== undefined && object !== null && toString.call( object ) == match;
	}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.argv.isObject"></a>[function <span class="apidocSignatureSpan">argv.</span>isObject ( object )](#apidoc.element.argv.isObject)
- description and source-code
```javascript
isObject = function ( object ) {
		return object !== undefined && object !== null && toString.call( object ) == match;
	}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.argv.isRegExp"></a>[function <span class="apidocSignatureSpan">argv.</span>isRegExp ( object )](#apidoc.element.argv.isRegExp)
- description and source-code
```javascript
isRegExp = function ( object ) {
		return object !== undefined && object !== null && toString.call( object ) == match;
	}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.argv.isString"></a>[function <span class="apidocSignatureSpan">argv.</span>isString ( object )](#apidoc.element.argv.isString)
- description and source-code
```javascript
isString = function ( object ) {
		return object !== undefined && object !== null && toString.call( object ) == match;
	}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.argv.mod"></a>[function <span class="apidocSignatureSpan">argv.</span>mod ( object )](#apidoc.element.argv.mod)
- description and source-code
```javascript
mod = function ( object ) {
		var mod;

		// Allow multi mod setup
		if ( self.isArray( object ) ) {
			object.forEach(function( value ) {
				self.mod( value );
			});
		}
		// Handle edge case
		else if ( ! self.isObject( object ) ) {
			throw new Error( 'No mod definition provided' );
		}
		// Force mod name
		else if ( ! object.mod ) {
			throw new Error( "Expecting 'mod' entry for module" );
		}
		// Create object if not already done so
		else if ( ! self.mods[ object.mod ] ) {
			self.mods[ object.mod ] = { mod: object.mod, options: {}, short: {} };
		}

		// Setup
		mod = self.mods[ object.mod ];
		mod.description = object.description || mod.description;

		// Attach each option
		self.option( mod.mod, object.options );

		return self;
	}
```
- example usage
```shell
...

### Modules

Modules are nested commands for more complicated scripts. Each module has it's own set of options that
have to be defined independently of the root options.

'''js
argv.mod({
	mod: 'module',
	description: 'Description of what the module is used for',
	options: [ list of options ]
});
'''
...
```

#### <a name="apidoc.element.argv.option"></a>[function <span class="apidocSignatureSpan">argv.</span>option ( mod, object )](#apidoc.element.argv.option)
- description and source-code
```javascript
option = function ( mod, object ) {
		if ( object === undefined ) {
			object = mod;
			mod = undefined;
		}

		// Iterate over array for multi entry
		if ( self.isArray( object ) ) {
			object.forEach(function( entry ) {
				self.option( mod, entry );
			});
		}
		// Handle edge case
		else if ( ! self.isObject( object ) ) {
			throw new Error( 'No option definition provided' + ( mod ? ' for module ' + mod : '' ) );
		}
		// Handle module definition
		else if ( object.mod ) {
			self.mod( object );
		}
		// Correct the object
		else {
			if ( ! object.name ) {
				throw new Error( 'No name provided for option' );
			}
			else if ( ! object.type ) {
				throw new Error( 'No type proveded for option' );
			}

			// Attach tester for value on booleans
			// to avoid false targets
			object.test = object.test || ( object.type == 'boolean' ? boolTest : null );
			object.description = object.description || '';
			object.type = self.isFunction( object.type ) ? object.type :
				self.isString( object.type ) && rlistcsv.exec( object.type ) ? self.types[ 'listcsv-combo' ]( object.type ) :
				self.isString( object.type ) && self.types[ object.type ] ? self.types[ object.type ] :
				self.types.string;

			// Apply to module
			if ( mod ) {
				if ( ! self.mods[ mod ] ) {
					self.mods[ mod ] = { mod: mod, options: {}, short: {} };
				}

				// Attach option to submodule
				mod = self.mods[ mod ];	
				mod.options[ object.name ] = object;

				// Attach shorthand
				if ( object.short ) {
					mod.short[ object.short ] = object;
				}
			}
			// Apply to root options
			else {
				self.options[ object.name ] = object;

				// Attach shorthand option
				if ( object.short ) {
					self.short[ object.short ] = object;
				}
			}
		}

		return self;
	}
```
- example usage
```shell
...
'''


### Usage

'''js
var argv = require( 'argv' );
var args = argv.option( options ).run();
-> { targets: [], options: {} }
'''


### Run

Runs the argument parser on the global arguments. Custom arguments array can be used by passing into this method
...
```

#### <a name="apidoc.element.argv.run"></a>[function <span class="apidocSignatureSpan">argv.</span>run ( argv )](#apidoc.element.argv.run)
- description and source-code
```javascript
run = function ( argv ) {
		try {
			return self._run( argv );
		}
		catch ( e ) {
			if ( ! self.isString( e ) ) {
				throw e;
			}

			console.log( "\n" + e + ". Trigger '" + self.name + " -h' for more details.\n\n" );
			process.exit( 1 );
		}
	}
```
- example usage
```shell
...
'''


### Usage

'''js
var argv = require( 'argv' );
var args = argv.option( options ).run();
-> { targets: [], options: {} }
'''


### Run

Runs the argument parser on the global arguments. Custom arguments array can be used by passing into this method
...
```

#### <a name="apidoc.element.argv.type"></a>[function <span class="apidocSignatureSpan">argv.</span>type ( name, callback )](#apidoc.element.argv.type)
- description and source-code
```javascript
type = function ( name, callback ) {
		if ( self.isObject( name ) ) {
			for ( var i in name ) {
				if ( self.isFunction( name[ i ] ) ) {
					self.types[ i ] = name[ i ];
				}
			}
		}
		else if ( callback === undefined ) {
			return self.types[ name ];
		}
		else if ( self.isFunction( callback ) ) {
			self.types[ name ] = callback;
		}
		else if ( callback === null && self.types.hasOwnProperty( name ) ) {
			delete self.types[ name ];
		}

		return self;
	}
```
- example usage
```shell
...
$ script -p /path/to/file1 -p /path/to/file2
-> option: [ '/path/to/file1', '/path/to/file2' ]
'''

You can also create your own custom type for special conversions.

'''js
argv.type( 'squared', function( value ) {
	value = parseFloat( value );
	return value * value;
});

argv.option({
	name: 'square',
	short: 's',
...
```

#### <a name="apidoc.element.argv.version"></a>[function <span class="apidocSignatureSpan">argv.</span>version ( v )](#apidoc.element.argv.version)
- description and source-code
```javascript
version = function ( v ) {
		self.option({
			_version: v,
			name: 'version',
			type: function(){ return true; },
			description: 'Displays version info',
			example: self.name + " --version",
			onset: function( args ) {
				console.log( v + "\n" );
				process.exit( 0 );
			}
		});

		return self;
	}
```
- example usage
```shell
...


### Version

Defining the scripts version number will add the version option and print it out when asked.

'''js
argv.version( 'v1.0' );

$ script --version
v1.0

'''
...
```



# <a name="apidoc.module.argv.types"></a>[module argv.types](#apidoc.module.argv.types)

#### <a name="apidoc.element.argv.types.boolean"></a>[function <span class="apidocSignatureSpan">argv.types.</span>boolean ( value )](#apidoc.element.argv.types.boolean)
- description and source-code
```javascript
boolean = function ( value ) {
			return ( value == 'true' || value === '1' );
		}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.argv.types.csv"></a>[function <span class="apidocSignatureSpan">argv.types.</span>csv ( value )](#apidoc.element.argv.types.csv)
- description and source-code
```javascript
csv = function ( value ) {
			return value.split( ',' );
		}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.argv.types.float"></a>[function <span class="apidocSignatureSpan">argv.types.</span>float ( value )](#apidoc.element.argv.types.float)
- description and source-code
```javascript
float = function ( value ) {
			return parseFloat( value, 10 );
		}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.argv.types.int"></a>[function <span class="apidocSignatureSpan">argv.types.</span>int ( value )](#apidoc.element.argv.types.int)
- description and source-code
```javascript
int = function ( value ) {
			return parseInt( value, 10 );
		}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.argv.types.list"></a>[function <span class="apidocSignatureSpan">argv.types.</span>list ( value, name, options )](#apidoc.element.argv.types.list)
- description and source-code
```javascript
list = function ( value, name, options ) {
			if ( ! options[ name ] ) {
				options[ name ] = [];
			}

			options[ name ].push( value );
			return options[ name ];
		}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.argv.types.listcsv-combo"></a>[function <span class="apidocSignatureSpan">argv.types.</span>listcsv-combo ( type )](#apidoc.element.argv.types.listcsv-combo)
- description and source-code
```javascript
listcsv-combo = function ( type ) {
			var parts = type.split( ',' ),
				primary = parts.shift(),
				secondary = parts.shift();

			return function( value, name, options, args ) {
				// Entry is going to be an array
				if ( ! options[ name ] ) {
					options[ name ] = [];
				}

				// Channel to csv or list
				if ( primary == 'csv' ) {
					value.split( ',' ).forEach(function( val ) {
						options[ name ].push( self.types[ secondary ]( val, name, options, args ) );
					});
				}
				else {
					options[ name ].push( self.types[ secondary ]( value, name, options, args ) );
				}

				return options[ name ];
			};
		}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.argv.types.path"></a>[function <span class="apidocSignatureSpan">argv.types.</span>path ( value )](#apidoc.element.argv.types.path)
- description and source-code
```javascript
path = function ( value ) {
			var end = value[ value.length - 1 ] == '/';

			if ( rhome.exec( value ) ) {
				value = PATH.normalize( process.env.HOME + '/' + value.replace( rhome, '' ) );
			}
			else if ( ! rroot.exec( value ) ) {
				value = PATH.normalize( process.cwd() + '/' + value );
			}

			return value + ( end && value[ value.length - 1 ] != '/' ? '/' : '' );
		}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.argv.types.string"></a>[function <span class="apidocSignatureSpan">argv.types.</span>string ( value )](#apidoc.element.argv.types.string)
- description and source-code
```javascript
string = function ( value ) {
			return value.toString();
		}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
