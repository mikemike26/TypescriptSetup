# Typescript Setup

This is some basic information on installing and general usage of typescript with Angular 1.x.

## Setup
We need to install Typescript globally on our machine.
```sh
$ npm install -g typescript
```
Create a tsconfig.json (or copy from this repo) in your root client directory with the following contents
```sh
{
  "compilerOptions": {
    "noImplicitAny": false, //allows the use of type: any
    "removeComments": false,
    "preserveConstEnums": true,
    "target": "ES5",
    "sourceMap": true,
    "listFiles": false //shows files on transpile in the terminal
  }
}
```
#### Rename your files!
We also need to rename all our js files to .ts files.  You can do this quickly in the finder by selecting all your js files and clicking "rename".

### Running the transpiler
We can start the typescript transpiler with the following command:
```sh
$ tsc -p yourJsDirectory
```
If we just run the tsc command alone and specify a file, it will only transpile that file.  Running this with the -p flag lets us transpile a whole directory.  This targeted directory must contain your tsconfig.json file

If you are in an Angular 1.x project, you'll most likely get a "cannot find name angular" error.  The compiler doesn't know what the angular variable is.  Typescript has type definition files that help remedy this.

### Type Definition files
These are d.ts files.

Check out https://github.com/typings/typings.  This is the command line tool to install our type definitions.

Install tsd globally
```sh
$ npm install typings --global
```

Then install your needed definition files in your project
```sh
$ typings install angular --ambient --save
$ typings install jquery --ambient --save
$ typings install angular-ui-router --ambient --save
```
Notice that this created a typings directory and a typings.json in your root.

We can search for type definition files at http://definitelytyped.org/tsd/.  
**THE TSD TOOL IS DEPRECIATED, PLEASE USE THE TYPINGS SYNTAX.**  If you use a type definition from tsd, you need to use the --ambient flag.  Most definitions will still be coming from tsd.


If you add your own type definitions, don't add them to the typings directory.  Currently that directory gets over written whenever you add anything to it.

Add the /typings directory to your .gitignore, we do not want to version this. Run:
```sh
$ typings install
```
to install your definitions.  This is similar to npm modules.

## TSLint
SLint checks your TypeScript code for readability, maintainability, and functionality errors.  This will help us make the transition to typescript and help enforce some code style conventions.

Install globally 
```sh
$ npm install tslint -g
```
Generate the tslint config file
```sh
tslint --init
```
add a tslint.json file to your root directory, see the file in this repo.

To enable TSLint in webstorm click:
- webstorm > preferences > languages and frameworks > typescript > TSLint
- select enable
- point the TSLint package to /usr/local/lib/node_modules/tslint
  * If you click the dropdown, it should populate
- make sre "Search for tslint.json" selected

## Transpiling your project

To enable transpiling in webstorm click: 
- webstorm > preferences > languages and frameworks > typescript 
- check the box "Enable Typescript compiler".  
- Make sure to check the setting to "Use tsconfig.json".
