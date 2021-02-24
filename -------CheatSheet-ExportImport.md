## Purpose: Remind myself the differences on Import/Export between CommonJS (CJS) and ES Module (ESM)

1. [Explains CommonJS](https://www.sitepoint.com/understanding-module-exports-exports-node-js/)
1. [Explains Various](https://www.jvandemo.com/a-10-minute-primer-to-javascript-modules-module-formats-module-loaders-and-module-bundlers/)
1. [module.exports vs. exports](https://www.hacksparrow.com/nodejs/exports-vs-module-exports.html)

>> Note2Self: This is not done, need to read above 3 articles to understand better to compile md notes ....

CommonJS (CJS)
- standard used in Node.js
- npm ecosystem is built upon this format
- require('./xxxxx)
- exports.xxxxxx 
- module.exports xxxxxxx
```js 
const fs = require('fs');

fs.someMethod(someArguments);
```
```js 
const aFunc = () => {
   return 'string';
};

exports.aFunc = aFunc;
```
```js
const funcFile = require('./FuncExportFileName');

console.log(`Using import: ${funcFile.aFunc()}`);
```


ES Module (ESM)
- From JavaScript ES6 (ES2015) 
- supports a native module formt
- uses `export` to export a module's public API
- uses `import` to import module
```js
```