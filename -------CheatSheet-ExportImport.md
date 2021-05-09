## Purpose: Remind myself the differences on Import/Export between CommonJS (CJS) and ES Module (ESM)

1. [Explains Various](https://www.jvandemo.com/a-10-minute-primer-to-javascript-modules-module-formats-module-loaders-and-module-bundlers/)
1. [Explains CommonJS](https://www.sitepoint.com/understanding-module-exports-exports-node-js/)
1. [module.exports vs. exports](https://www.hacksparrow.com/nodejs/exports-vs-module-exports.html)

*Note2Self: This is not done, need to read above 3 articles to understand better to compile md notes ....*

> A module is a reusable piece of code that encapsulates implementation details 
and exposes a public API so it can be easily loaded and used by other code.

Earlier JavaScript editions were not designed with modules in mind.  
Developers came up with different patterns to simulate modular design in JS.  
[This article shows the various patterns with code example](https://www.jvandemo.com/a-10-minute-primer-to-javascript-modules-module-formats-module-loaders-and-module-bundlers/)
> A module format is basicallly the syntax we use to define a module.  
Both CommonJS and ES Module are module formats.

CommonJS (CJS)
- standard format used in Node.js
- npm ecosystem is built upon this format
- require('./xxxxx')
- exports.xxxxxx 
- module.exports xxxxxxx
```js 
const fs = require('fs');     //built-in/native JS modules

fs.someMethod(someArguments);
```
```js 
const aFunc = () => {
   return 'string';
};

exports.aFunc = aFunc;
```
```js
const funcFile = require('./FuncExportFileName.js');        //??? not sure if this is totally correct???

console.log(`Using import: ${funcFile.aFunc()}`);           //??? not sure if this is totally correct???
```
```js
//index.js
const funcOne = () =>{
   //...
}
const funcTwo = () => {
   return "something";
}

module.exports = funcTwo;
```
```js

const funcTwo = require('./index.js');
funcTwo();
```


ES Module (ESM)
- From JavaScript ES6 (ES2015) 
- this is the JS native module formt
- uses `export` or `export default` token to export a module's public API
- uses `import` token to import module
```js
// this filename: lib.js
// Export this function
export function thisFunc(){
   console.log('Print to log');
}

// Do not export this function
function otherPrivateFunc(){
   // ...
}
```
```js
import { thisFunc } from './lib';   

thisFunc();
```
```js
import { thisFunc as runThis } from './lib';    //give import an alias using as

runThis();
```
```js
import * as lib from './lib';                   //load an entire module as obj

lib.thisFunc();
```
```js
export default function thisDefaultFunc(){      //ESM format supports default exports
   console.log("print");
}

export function anotherOne(){                   //export non-default function
   console.log("log");
}
```
```js
import thisDefaultFunc, { anotherOne } from './lib';   //import default without {}; else import with {}

thisFunc();
anotherOne();
```
```js
//can export primitive values or obj
// lib.js

// Export default function
export default function sayHello(){  
  console.log('Hello');
}

// Export non-default function
export function sayGoodbye(){  
  console.log('Goodbye');
}

// Export simple value
export const apiUrl = '...';

// Export object
export const settings = {  
  debug: true
}
```
```js
const reactFunction = () =>{
   //...
}

export default reactFunction;
```

