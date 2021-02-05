## Purpose: Remind myself the nuances of JavaScript
_See FreeCodeCamp JS Basics for basics practices_  
&nbsp; <non-breaking-space>
    


### [`null` vs. `undefined`](https://www.tothenew.com/blog/difference-between-undefined-and-null-in-javascript/#:~:text='Null'%20in%20JavaScript,to%20a%20variable%20by%20JavaScript.)
---
- null
  - In JS, null is a value that can be assigned to a variable.
  - null === "no value" object (nonexistence of any value)
  - null is an object value
  - can shred a variable off its assigned value by assigning `null` to it

  ```js
  var null_item = null;
  console.log(null_item); //console will print 'null'
  ```

- undefined

  - undefined is when a variable _has been declared_ but nothing has been given/assigned to it (explicitly initialize or defined)
  - undefined === ????
  - undefined is a variable TYPE

- undefined

  - global var JS creates at run time
  - assigned to an obj when:
    - declared but NOT initialized and defined
    - array index or obj property that does not exist
    - a function param that has not been supplied
    - the return value of functions that have to but don't return a value

  ```js
  var item;
  console.log(item); //console will print 'undefined'
  ```

### Type Coercion (changing)
---
- int type mix with string type of data will convert the whole result into string type
- string takes precedence
- regardless of which data type goes first
  ```js
  let sum = 1 + 2;          //===3
  let cantSum = 5 + "10";   //===510
  let stillCant = "3" + 4;  //===34


### [Timing Events](https://www.w3schools.com/js/js_timing.asp)
---
- both functions are HTML DOM Window object allowing execution of code at specified time intervals
  > There are 1000 milliseconds in one second!
  
- `setTimeout(func, milliseconds-before-execution)`
  - Executes a function, after waiting a specified number of milliseconds
  - delay of execution
  - `clearTimeout()` stops the execution of the function specified in setTimeout(), using the var returned from setTimeout()
  ```html
  <button onclick="myVar = setTimeout(myFunc, 3000)"> Wait 3 Seconds! </button>
  <!-- Wait 3 seconds, then myFunc will be executed -->
  <button onclick="clearTimeout(myVar)">Stop it</button>
  ```

- `setInterval(func, milliseconds-between-executions)`
  - Executes a function, and repeats the execution of the function continuously after the specified number of milliseconds
  - repeats of execution
  - `clearInterval()` stops the executions of the function specified in the setInterval(), using the var returned from setInterval()
  ```html
  <p id="demo"></p>

  <button onclick="clearInterval(myVar)">Stop time</button>

  <script>
  var myVar = setInterval(myTimer, 1000);
  function myTimer() {
    var d = new Date();
    document.getElementById("demo").innerHTML = d.toLocaleTimeString();
  }
  </script>
  ```




### `++X` vs. `X++`
---
- X++ is post-increment - x is incremented _after_ being used/executed
- ++X is pre-increment - x is incremented _before_ being used/executed

```js
x = 5; //x++ = 6;  ++x = 6;
x++ + x++ = 5 + 6 = 11;
x++ + ++x = 5 + 7 = 12;
++x + ++x = 6 + 7 = 13;
```

- In for loop, however, both `x++` and `++x` would be the same. The loop evaluation and execution is done prior to either types of increments.

```js
for (let i = 0; i < 4; i++) {
  //do something with i
}
//equals to
for (let i = 0; i < 4; ++i) {
  //do something with i
}
```


### [slice() vs. splice()](https://www.freecodecamp.org/news/javascript-array-slice-vs-splice-whats-the-difference/)
---
- slice:
  - Array.prototype.slice()
  - does *not alter* the original array
  - slice an array from start to end, excluding end
  - returns the sliced items
  - if end is omitted, it is slicing all the way til the end of array
  - if start is negative value, the elements are counted from the end backwards
  ```js
  arr.slice(start, [end])
  ```

- splice:
  - Array.prototype.splice()
  - splice operates *in place* meaning it *alters* the original array
  - used for removing *and adding* elements to the array
  - returns the deleted items
  - if start is negative value, the elements are counted from the end backwards
  - if `deleteCount` is omitted, it is removing all the way til the end of array
  - if `itemsToInsert` is omitted, elements are only removed
  ```js
  arr.splice(start, [deleteCount, itemToInsert1, itemToInsert2, ...])
  ```


### string.split("") 
---
  - convert string to array
  - ("") separates each character out
    ```js
      'I can code'.split("")  //['I', ' ', 'c', 'a','n', ' ', 'c', 'o','d', 'e']
    ```
  - () puts the whole string as the first array item at index 0
    ```js
      'I can code'.split()  //[ 'I can code' ]
    ```
  - (" ") or (",") or (", ") separates depending on the structure of the string
    ```js
      'I can code'.split(" ") //[ 'I', 'can', 'code' ] - space in string as delimiter
      'I can code'.split(",") //[ 'I can code' ] - string doesn't have ',' so no such delimiter
      'I can code, too!'.split(",") //[ 'I can code', ' too!' ] - comma in stringas delimiter
      'Including, the, space, before, each, word'.split(",")  //[ 'Including', ' the', ' space', ' before', ' each', ' word' ] - using just (",")
      'Trimming, the, space, before, each, word'.split(", ")  //[ 'Trimming' , 'the' , 'space' , 'before' , 'each' , 'word' ] - using (",_")
    ```
  

### array.join("") ...
---
  - convert or concatenate all array items into one string, without space or comma separated
  - (), (",') or (" ") would add the specified char as seperated delimiter
    ```js
      ["I", "can", "develop"].join()      //I,can,develop - include default delimiter (,) between array items
      ["I", "can", "develop"].join(",")   //I,can,develop - specify using (,)
      ["I", "can", "develop"].join(", ")  //I, can, develop - include , and space as delimiter
    ```

    ```js
      ["I", "can", "develop"].join("") //Icandevelop - include no delimiter between array items
    ```

    ```js
      ["I", "can", "develop"].join(" ") //I can develop  - include space delimiter between array item
    ```

    ```js
      ["I", "can", "develop", " "].join("! ") //I! can! develop!  
    ```


### string.repeat(#)
---
```js
" ".repeat(5)   //_____   - 5 spaces
'*'.repeat(5)   //*****   - 5 stars
"/-".repeat(3)  ///-/-/-  - 3 of /-
```

### [for in vs. for of](https://bitsofco.de/for-in-vs-for-of/) ...
---
- ...
- !!! (comparison table at the end of article)

| A Comparison | for..in | for..of |
| --- | --- | --- |
| Applies to | Enumerable Properties | Iterable Collections |
| Use with Objects?	| Yes |	No |
| Use with Arrays?	| Yes, but not advised |	Yes |
| Use with Strings?	| Yes, but not advised |	Yes |

![](Screenshots/forINvsforOFComparison.png)



### Array("n times specified/size").fill("what");
- console.log(Array(4).fill(3));  //[ 3, 3, 3, 3 ]
- console.log(Array(5).fill("code"));  //[ 'code', 'code', 'code', 'code', 'code' ]




### IIFE - Immediately Inovked Function Expression
---
  ```js
  (function() {
      var a = b = 5;
  })();
  ```


### Global Scope vs. Local Scope
---
 What will be printed on console?
 ```js
  (function() {
    var a = b = 5;
  })();
  console.log(b);
 ```
 Answer: The code above prints 5
 Above function is called an IIFE: Immediately-Invoked Function Expressions.
 In that only a is a local variable declared inside the function with a var.
 b is actually a global scoped variable decleared inside the function withOUT var keyword.
 
 if stict mode (include `'use strict';` inside a function) was enabled,
 the code would raise the error "Uncaught Reference Error: b is not defined."
 strict mode expects a variable to be explicitly referenced to the global scope 
 if this was intended behavior: 
 ```js
  (function() {
    'use strict';
    var a = b = 5;
  })();
  console.log(b);    //Uncaught Reference Error: b is not defined.
  
  (function() {
    'use strict';
    var a = window.b = 5;   //explicitly specified with window.
  })();
  console.log(b);    //=5 due to global scope
 ```

### Hoisting
---
What is the result of executing this code?
```js
function test() {
    console.log(a);
    console.log(foo());
    
    var a = 1;
    function foo() {
        return 2;
    }
}
test();
```
Answer: undefined and 2
Reason: Both variables and functions are "hoisted" (moved at the top of 
the function) but variables doen't retain any assigned value.
At the time the variable a is printed, it exists in the function (declared!)
but its value hasn't been assigned, ie. undefined.
The above code is essentially equivalent to:
```js
function test() {
  var a;
  function foo() {
      return 2;
  }

  console.log(a);       //undefined
  console.log(foo());   //2
  
  a = 1;
}
test();
```

### this.
---
What is the result of this code?
```js
var fullname = 'John Doe';
var obj = {
   fullname: 'Colin Ihrig',
   prop: {
      fullname: 'Aurelio De Rosa',
      getFullname: function() {
         return this.fullname;
      }
   }
};

console.log(obj.prop.getFullname());

var test = obj.prop.getFullname;

console.log(test());
```
Answer: The code prints Aurelio De Rosa and John Doe.
Reason: The context of a function, which is referred with the `this` keyword,
        in JavaScript depends on h ow a function is inovked, not how it's defined.

`console.log(obj.prop.getFullname());` is running the getFullname function right there
with obj.prop and obj.prop is an object with fullname in it. So the `this` is referring to
the fullname property inside the obj.prop object.
`var test = obj.prop.getFullname;` is pulling the getFullname function and assign it to 
the test variable.  It has not been run until it's being logged.  
At the time of logging, test() is executed to return THIS.fullname and `this` is referring to 
global fullname John Doe outside of obj object.

>In the first console.log() call, getFullname() is invoked as a function of the obj.prop object. So, the context refers to the latter and the function returns the fullname property of this object. On the contrary, when getFullname() is assigned to the test variable, the context refers to the global object (window). This happens because test is implicitly set as a property of the global object. For this reason, the function returns the value of a property called fullname of window, which in this case is the one the code set in the first line of the snippet.

### .call() and .apply()
---
Fix the previous question’s issue so that the last console.log() prints Aurelio De Rosa.
Answer:
```js
console.log(test.call(obj.prop));   //Aurelio De Rosa
console.log(test.call(obj));        //Colin Ihrig
```
> .call()/.apply() calls/applies a method of an object, substituting another object for the current object.\
> The issue is fixed by forcing the context of the function using either the call() or the apply() function.\
[See: What’s the difference between function.call and function.apply?](https://www.sitepoint.com/whats-the-difference-between-function-call-and-function-apply/)


### global vs. local scope
---
What is the result of this code?
```js
var v = 1;                      //global var
var f1 = function(){
    console.log(v);
}
var f2 = function(){
    var v = 2;                  //local var
    f1();
}
f2();
```
Answer: f2() prints 1.  f1() v is looking at the global var.

What about this?
```js
var v = 1;                      //global var
var f1 = function(){
    console.log(v);
}
var f2 = function(){
    var v = 2;                  //local var
    var f1 = function(){        //local f1 overrides global
        console.log(v);         //local f1 has scope to local v
    }
    f1();                       
}
f2();
```
Answer: f2() prints 2.  local f1() overrides global f1()

### typeof === object?
---
What is a potential pitfall with using typeof bar === "object" to determine if bar is an object? How can this pitfall be avoided?
Answer: In JS, `null` is ALSO an object (see below).
```js
var bar = "text";
console.log(typeof bar === "object");     //false
console.log(typeof bar);                  //string

var bar = true;
console.log(typeof bar === "object");     //false
console.log(typeof bar);                  //boolean

var bar = {name: "bar", type: "soap"};
console.log(typeof bar === "object");     //true
console.log(typeof bar);                  //object

var bar = null;
console.log(typeof bar === "object");     //true    <-----------------!!!
console.log(typeof bar);                  //object
```
To avoid, also include checking bar is null:
```js
var bar = null;
console.log(bar !== null && typeof bar === "object");   //false <--------
console.log(typeof bar);                                //object

var bar = [];
console.log(bar !== null && typeof bar === "object" );  //true - array is object
console.log(typeof bar);                                //object 
```
Testing multiple scenarios
```js
var bar = function(){ return 1+1;};
console.log(bar !== null && typeof bar === "object" 
    || typeof bar ==="function");         //true
console.log(typeof bar);                  //function

var bar = [];
console.log(toString.call(bar));          //[object Array]
console.log(typeof bar);                  //object

console.log((bar !== null) && (typeof bar === "object") && (toString.call(bar) !== "[object Array]"));                                //more specific filter
```
Note: ES5 has its own null check:
```js
var bar = [];
console.log(Array.isArray(bar));          //true
```

### More Scopes
---
What will the code below output to the console and why?
```js
(function(){
  var a = b = 3;
})();

console.log("a defined? " + (typeof a !== 'undefined'));      //false; a is undefined to global (my answer)
console.log("b defined? " + (typeof b !== 'undefined'));      //true: b is defined in global (my answer)
```
Explanation:
`var a = b = 3;` is NOT shorthand for:  var b = 3; var a = b;

In JS, `var a = b = 3;` is shorthand for:
```js
b = 3;        //global var outside function
var a = b;    //local var inside function
```
As such, logging a and b outside of function after run makes a NOT visible to global (not defined) and b defined in global scope.
> Since the statement var a = b = 3; is shorthand for the statements b = 3; and var a = b;, b ends up being a global variable (since it is not preceded by the var keyword) and is therefore still in scope even outside of the enclosing function.

NOTE: `'use strict'`  
However if in strict mode:
```js
(function(){
    'use strict';
    var a = b = 3;
  })();
```
b defined in such a way would not be allowed and thus generate a runtime error: `ReferenceError: b is not defined`
In strict mode, b needs to be defined as specific as possible:
```js
(function(){
    'use strict';
    var a = Window.b = 3;     //points to DOM loaded in window
  })();
```

### Scope with this.
---
What will the code below output to the console and why?
```js
var myObject = {
    foo: "bar",
    func: function() {
        var self = this;
        console.log("outer func:  this.foo = " + this.foo);                           //bar (mine)
        console.log("outer func:  self.foo = " + self.foo);                           //bar (mine)
        (function() {
            console.log("inner func:  this.foo = " + this.foo);                       //undefined (mine)
            console.log("inner func:  self.foo = " + self.foo);                       //bar (mine)
        }());
    }
};
myObject.func();
```
Explanation:
The above code will output the following to the console:
```js
outer func:  this.foo = bar 
outer func:  self.foo = bar
inner func:  this.foo = undefined
inner func:  self.foo = bar
```
this. represents the current object in ACCESS!
In the outer function, both this and self refer to myObject and therefore both can properly reference and access foo.

In the inner function, though, this no longer refers to myObject. (inner function() is running on its own) As a result, this.foo is undefined in the inner function, whereas the reference to the local variable self remains in scope and is accessible there because it is local to the inner function.  
&nbsp;  
&nbsp;  

### JS function block
---
What is the significance of, and reason for, wrapping the entire content of a JavaScript source file in a function block?  
mine:  
reusability of code (importable elsewhere), modulize for easily maintainable code, separation of concern  
Answer:
> create closure, create private namespace, avoid potential name clashes between JS modules and libraries, allow easily referenceable shorter alias for global variable.

This is an increasingly common practice, employed by many popular JavaScript libraries (jQuery, Node.js, etc.). This technique creates a closure around the entire contents of the file which, perhaps most importantly, creates a private namespace and thereby helps avoid potential name clashes between different JavaScript modules and libraries.

Another feature of this technique is to allow for an easily referenceable (presumably shorter) alias for a global variable. This is often used, for example, in jQuery plugins. jQuery allows you to disable the $ reference to the jQuery namespace, using jQuery.noConflict(). If this has been done, your code can still use $ employing this closure technique, as follows:

(function($) { /* jQuery plugin code referencing $ */ } )(jQuery);


### `'use strict'`
---
What is the significance, and what are the benefits, of including 'use strict' at the beginning of a JavaScript source file?  
mine:  
avoid unintented errors, things are clearly defined and specified, make debugging more efficient.  
Answer:
> enforce stricter parsing and error handling at runtime.  catch errors bypassed/ignored by JS or failed silently so they can be fixed properly.  

Some of the key benefits of strict mode include:

- Makes debugging easier.  
Code errors that would otherwise have been ignored or would have failed silently will now generate errors or throw exceptions, alerting you sooner to problems in your code and directing you more quickly to their source.

- Prevents accidental globals.  
Without strict mode, assigning a value to an undeclared variable automatically creates a global variable with that name. This is one of the most common errors in JavaScript. In strict mode, attempting to do so throws an error.

- Eliminates `this` coercion.  
Without strict mode, a reference to a `this` value of null or undefined is automatically coerced to the global. This can cause many headfakes and pull-out-your-hair kind of bugs. In strict mode, referencing a `this` value of null or undefined throws an error.

- Disallows duplicate parameter values.  
Strict mode throws an error when it detects a duplicate named argument for a function (e.g., function foo(val1, val2, val1){}), thereby catching what is almost certainly a bug in your code that you might otherwise have wasted lots of time tracking down.
    > Note: It used to be (in ECMAScript 5) that strict mode would disallow duplicate property names (e.g. var object = {foo: "bar", foo: "baz"};) but as of ECMAScript 2015 this is no longer the case.

- Makes eval() safer.  
There are some differences in the way eval() behaves in strict mode and in non-strict mode. Most significantly, in strict mode, variables and functions declared inside of an eval() statement are not created in the containing scope (they are created in the containing scope in non-strict mode, which can also be a common source of problems).

- Throws error on invalid usage of delete.  
The delete operator (used to remove properties from objects) cannot be used on non-configurable properties of the object. Non-strict code will fail silently when an attempt is made to delete a non-configurable property, whereas strict mode will throw an error in such a case.  
  
&nbsp;  
&nbsp; 

### return & {}
---
Consider the two functions below. Will they both return the same thing? Why or why not?
```js
function foo1()
{
  return {
      bar: "hello"
  };
}

function foo2()
{
  return
  {
      bar: "hello"
  };
}
console.log("foo1 returns:",foo1());
console.log("foo2 returns:",foo2());
```
mine:  
No, foo1() returns the obj.  foo2() returns undefined because the obj defined is on the next line after return. JS implicitly ends the return stmt with a silent `;` and the next lines (the obj) was never processed.  
Answer:  
  foo1 returns: Object {bar: "hello"}
  foo2 returns: undefined 

foo2() will actually return undefined WITHOUT any error being thrown.

Reason: semicolons are technically optional in JavaScript (although omitting them is generally really bad form). As a result, when the line containing the return statement (with nothing else on the line) is encountered in foo2(), a semicolon is automatically inserted immediately after the return statement.

No error is thrown since the remainder of the code is perfectly valid, even though it doesn’t ever get invoked or do anything (it is simply an unused code block that defines a property bar which is equal to the string "hello").

This behavior also argues for following the convention of placing an opening curly brace at the end of a line in JavaScript, rather than on the beginning of a new line. As shown here, this becomes more than just a stylistic preference in JavaScript.

REMEMBER: The opening { should always follow `return` immediately instead of on the next line.  This is not like a function in other Java/C# language.
  
&nbsp;  
&nbsp; 

### NaN
---
What is NaN? What is its type? How can you reliably test if a value is equal to NaN?  
mine:  
"Not a Number", NaN is a type number, can use parseInt() to test if the value return is a numeric value or NaN  
Answer:  
The `NaN` property represents a value that is “not a number”. This special value results from an operation that could not be performed either because one of the operands was non-numeric (e.g., "abc" / 4), or because the result of the operation is non-numeric.

Things to NOTE:
- NaN means “not a number”, its type however, is Number:  
  ```js
  console.log(typeof NaN);  // number
  ```
- NaN compared to anything – even itself! – is false:
  ```js
  console.log(NaN === NaN);             // false
  var text = 'text';
  console.log(parseInt(text));          // NaN
  console.log(parseInt(text) === NaN);  // false !!!
  console.log(Number(text));            // NaN
  console.log(Number(text) === NaN);    // false !!!
  ```

Testing NaN:
```js
var num = 4;
var text = 'text';
console.log(parseInt(num));   //4
console.log(parseInt(text));  //NaN
console.log(isNaN(num));      //false
console.log(isNaN(text));     //true
console.log(Number(num));     //4
console.log(Number(text));    //NaN
```

A better solution would either be to use value !== value, which would only produce true if the value is equal to NaN. 
```js
var num = 4;
var text = 'text';
console.log(parseInt(num)); //4
console.log(num !== 4);     //false
console.log(text !== 4);    //true    
```
ES6 offers a new Number.isNaN() function, which is a different and more reliable than the old global isNaN() function.
```js
var num = 4;
var text = 'text';
console.log(Number.isNaN(NaN));                 //true
console.log(Number.isNaN(num));                 //false - correct - 4 is number
console.log(Number.isNaN(text));                //false - text is a string, not NaN
console.log(Number.isNaN(parseInt(text)));      //true
```




  
&nbsp;  
&nbsp;  
### topic
---
code example ...