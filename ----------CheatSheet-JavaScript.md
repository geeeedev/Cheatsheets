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

### call() and apply()
---
Fix the previous question’s issue so that the last console.log() prints Aurelio De Rosa.

Answer:
```js
console.log(test.call(obj.prop));   //Aurelio De Rosa
console.log(test.call(obj));        //Colin Ihrig
```
> The issue can be fixed by forcing the context of the function using either the call() or the apply() function.\
[See: What’s the difference between function.call and function.apply?](https://www.sitepoint.com/whats-the-difference-between-function-call-and-function-apply/)














### topic
---
code example ...