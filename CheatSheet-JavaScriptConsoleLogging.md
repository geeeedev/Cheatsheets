## Purpose: Remind myself the basics and other functions of JavaScript Console Logging
&nbsp; <non-breaking-space>
    

### [JavaScript Console Logging](https://www.freecodecamp.org/news/javascript-console-log-example-how-to-print-to-the-console-in-js/)
- console.log with Multiple Values
  ```js
  let x = 1;
  let y = 2;
  let z = 3;
  console.log(`x:`, x, `y:`, y, `z:`, z);
  console.log({x,y,z});
  ```

- console.log with Objects
  ```js
  let user = {
      name: `Gwen`,
      contact: {
          email: `geeeedev@gmail.com`
      },
      location: `LA, CA`
  }
  console.log(user);
  console.log({user});    //auto include "user:" labelling!
  ```

- console.log with Variables
  ```js
  console.log("%s is %d years old living in %s, %s for %d years!", "Gwen","100","LA",'CA', 24);
  %s - string
  %d - digit
  ```

- Other Console Variations
  ```js
  console.log('Console Log');
  console.info('Console Info');
  console.debug('Console Debug');
  console.warn('Console Warn');     // yellow in browser console; style depends on browser
  console.error('Console Error');   // red in browser console; style depends on browser
  ```

- console.assert - Logs Conditionally (Optional)
  ```js
  let isItWorking = false;
  console.assert(isItWorking, "this is the reason why the test fails")
  ```
  > changing isItWorking to true, then the message will NOT be logged/appeared.

- console.count - Counting
  ```js
  for (let i = 0; i < 10; i++) {
    console.count();
  }
  ```

  > Each iteration of this loop will print a count to the console.  
You will see "default: 1, default: 2", and so on until it reaches 10.

  > If you run this same loop again you will see that the count picks up where it left off; 11 - 20.
  ```js
  for (let i = 0; i < 10; i++) {
    console.count();
  }
  ```

- console.countReset - Reset the count
  ```js
  console.countReset();
  for (let i = 0; i < 10; i++) {
    console.count();
  }
  ```
  > You will see "default: 1, default: 2", until it reaches 10 now due to the reset


- To name the counter to something other than "default"
  ```js
  for (let i = 0; i < 10; i++) {
    console.count("New Counter");
  }
  ```

- Reset with the same specific name
  ```js
  console.countReset("New Counter");
  console.count("New Counter")
  ```

- console.time/timeEnd - Track Time
  ```js
  console.time();
  setTimeout(() => {
    console.timeEnd();
  }, 5000);
  ```


- console.timeLog - Log current time of our timer while it's running without stopping it
  ```js
  setTimeout(() => {
    console.timeLog();
  }, 2000);
  ```
  > we will get our 2 second timeLog first, then our 5 second timeEnd time log.


- console.group/groupEnd - Group the Log
  ```js
  console.log('I am not in a group')

  console.group()
  console.log('I am in a group')
  console.log('I am also in a group')
  console.groupEnd()

  console.log('I am not in a group')
  ```

- make collapsable with Name
  ```js
  console.log("I am not in a group");

  console.groupCollapsed("Group1"); // see in browser console only
  console.log("I am in a group");
  console.log("I am also in a group");
  console.groupEnd();

  console.log("I am not in a group");
  ```

- console.track - stack tracing functions // works in browser console only
  ```js
  function one() {
    two();  //2
  }
  function two() {
    three(); //5
  }
  function three() {
    console.trace(); //8
  }
  one(); //10
  ```

- console.table - log in table format
  ```js
  let devices = [
      {
        name: 'iPhone',
        brand: 'Apple'
      },
      {
        name: 'Galaxy',
        brand: 'Samsung'
      }
    ]

    console.table(devices);
  ```
<!-- 
┌─────────┬──────────┬───────────┐
│ (index) │   name   │   brand   │
├─────────┼──────────┼───────────┤
│    0    │ 'iPhone' │  'Apple'  │
│    1    │ 'Galaxy' │ 'Samsung' │
└─────────┴──────────┴───────────┘
 -->

`console.table(devices,['name']);`
<!-- 
┌─────────┬──────────┐
│ (index) │   name   │
├─────────┼──────────┤
│    0    │ 'iPhone' │
│    1    │ 'Galaxy' │
└─────────┴──────────┘
 -->

`console.table(devices,['brand']);`
<!-- 
┌─────────┬───────────┐
│ (index) │   brand   │
├─────────┼───────────┤
│    0    │  'Apple'  │
│    1    │ 'Samsung' │
└─────────┴───────────┘
 -->

- applying console.table() in more complicated fetch scenario
  ```js
  async function getUsers() {         //works in browser console only
    let response = await fetch("https://jsonplaceholder.typicode.com/users");
    let data = await response.json();

    console.log(data);  //data shows but raw and hard to read
    console.table(data);
    console.table(data, ["name", "email", "username", "websites"]);
  }
  getUsers();
  ```

  > IMPT:  
fetch was designed for the browser and is not a standard node.js method  
fetch API is not implemented in Node  
need exernal module like node-fetch  
npm i node-fetch  
start .js file with const fetch = require("node-fetch");  

- styling console.log with CSS properties - %c to specify the style to be added
  ```js
  // works in browser console only
  console.log("%c this is yellow text on a blue background.", "color: yellow; background-color: blue");
  console.log("%c this is orange text on a green background.", "color: orange; background-color: green");
  ```

- console.clear - Clear the console
  ```js
  console.clear();
  ```
