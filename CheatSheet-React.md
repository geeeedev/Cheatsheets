## Purpose: Remind myself how to get started with React.js

- Start a react app  
  `npx create-react-app app-name-no-capital-letters`
  > [WebPack](https://webpack.js.org/guides/getting-started/)

- Run a react app  
   `npm start`

- Run a production build  
   `npm run build`

- super basic code structure example
   ```jsx
   //import statements
   import React, {useState, useEffect} from "react";
   import otherComponent from './componentDirectory/otherJSfile';
   import { styledCSSComponents, forExample, fromUsingStyledComponenet, ifAny } from './styleDirectory/cssFileInJSExtension';

   const funcName = (props) => {
      //states in JS
      const [stateOne, setStateOne] = useState('');
      const [stateTwo, setStateTwo] = useState('');
      const [stateList, setStateList] = useState('');
      
      //logic in JS
      const otherLogicFunction = () => {
         //...code
         //maybe a func with useEffect if applicable
         return stmt;
      }

      //view output in HTML <=> JS
      return ( 
         <> 
            <div className="veryBasicCSS">
               <h1>Some Title</h1>
               <OtherComponentHere />
            </div>
            <OrUsingFancyTagWithStyledComponent>
               {someJSObjectHere}
            </OrUsingFancyTagWithStyledComponent>
         </>
      );
   }
   ```   


# JSX
- Needed for all components written in JSX code
   
   `import React from "react";`

- JSX Syntax
   1. JavaScript + HTML in one file (no switching .js in .html with `<script></script>`)
   1. JSX is not required for React syntax, just makes life easier
   1. Allow HTML tag coding back in the mix
   1. Avoid constantly using `React.CreateElement("tag",{props},"childText...or more React.CreateElement for more children")`
   1. JSX also allows embedding JS expression inline with HTML/render()/return() WHEN USED WITH Curly Braces!! (don't forget the curlys)
      ```js
      function NumberList(props) {
         //logic in JS
         const numbers = props.numbers;
         const listItems = numbers.map((number) =>
            <ListItem key={ number.toString() } value={number} />
         );
         //view output in HTML wrapped in JS
         return (
            <ul>
               {listItems}
            </ul>
         );
      }
      ```
      ```js
      function NumberList(props) {
         //logic in JS
         const numbers = props.numbers;
         //view output in HTML <=> JS
         return (
            <ul>
               {numbers.map((number) =>
                  <ListItem key={number.toString()} value={number} />
               )}
            </ul>
         );
      }
      ```
   > [React & JSX](https://reactjs.org/docs/introducing-jsx.html)

   > [React Map()](https://reactjs.org/docs/lists-and-keys.html)

# Class Component 
- React Components are like functions that return HTML elements
- The Must
  1.  Component name must start with Capital letter
  1.  extends React.Component with import
  1.  render() to return React element (by JSX below or `React.createElement()`)
  1.  need `this` to access props and states
  1.  need a constructor if having state
      ```js
      import React, { Component } from "react";

      class MyClassComponent extends Component {
        constructor(props) {
          super(props);
          this.state = {
            position: "On", //initializing state, NOT setting
          };
        }
        render() {
          return (
            <>
              <h1> Hello!</h1>
              <p> This is a react element </p>
              <p> This is a prop element: {this.props.element} </p>
              <p> This is a state element: {this.state.position} </p>
            </>
          );
        }
      }
      export default MyClassComponent;
      ```

# Functional Component 
- React Components are like functions that return HTML elements
- The Must
   1. No extends Component - function IS a component already
   1. No render(), just go straight to return() 
   1. Accepts props in the function argument; no using `this`
   1. `import React, { useState } from "react";` to access states
   1. No constructor needed
      ```js
      import React from 'react';
      const PersonCard = props => {
         return(
            <div>
               <h1>{ props.lastName }, { props.firstName }</h1>
               <p>Age: { props.age }</p>
               <p>Hair Color: { props.hairColor }</p>
            </div>
         );
      }
      export default PersonCard;
      ```

# Functions
   - functions are first-class citizens in JavaScript - they can be passed around in parameter in the same way as other values.
   - map() in React
      - a JavaScript function specifically for array data only 
      - broadly used to transform each element of an array to function logic specified
      - the result of calling map() is always a NEW array; it never changes the original array data set.
      - always expects two arguments: each array item and each item's index
      ```js
      const Groceries = (props) => {
      // this could just as easily come from props
      const groceryList = ["pearl onions", "thyme", "cremini mushrooms", "butter"];
      return (
         <ul>{
            groceryList.map( (item, i) => 
                  <li key={ i }>{ item }</li>   //using index i as key to silent React warning
            )
         }</ul>
         ); 
      }
      ```
      > [map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

      > [React Lists and Keys](https://reactjs.org/docs/lists-and-keys.html)

# Props
- Passing Props
  1.  Immutable! === Read Only!
  1.  passing string needs ""
  1.  passing number needs {}, otherwise error and red
  1.  when in doubt, always use {}
  1.  can be string, number, boolean, and FUNCTION as well
   ```js
   <ComponentName
      PropOne="no curly ok for string"
      PropTwo={67}
      PropThree={"test"}
   /> //all valid
   ```

- Destructing Props
  ```js
  function PersonCard({ Fn, Ln, age, hairColor }) { ... //valid - smarter }

   function PersonCard(props) {
   const { Fn, Ln, age, hairColor } = props; //valid - less elegant
   return (
         <>
            <h1>{Ln}, {Fn}</h1>
            <p>Age: {age}</p>
            <p>Hair Color: {hairColor}</p>
         </>
      );
   }

   export default PersonCard;
   ```

# State
- Initial State
- setState
- Events
   1. prevent event default behavior (e.g. trigger full page refresh)
      `event.stopPropagation()  OR  event.preventDefault()`
   1. onClick - triggered when element is clicked
   1. onChange - triggered when element/form input is changed
   1. onSubmit - triggered when form is submitted
   1. onFocus - triggered when element is focused on by click or tap
   1. onBlur - triggered when element loses focus (clicked away)
   >[Handling Events](https://reactjs.org/docs/handling-events.html)

# Import/Export in React
- Single Export `export default` exports ONLY ONE component
   - then imports that ONLY ONE component in child component
   - no { } signifies this is a **default** import/export
      ```js
      ...
      export default NavBarContext;

      ...
      import NavBarContext from "../context/NavBarContext";  
      ```
   
- Multiple Export `export` exports MORE THAN ONE components at the same time
   - then must import with { } in ALL child component, even if just one component you are importing
      ```js
      ...
      export { Wrapper, NavBarContext }; 

      ...
      import { Wrapper, NavBarContext } from "./Wrapper";
      or 
      import { NavBarContext } from "./Wrapper";  
      ```

   - if you try to import like the default version thinking you are just grabbing one 
      ```js
      import NavBarContext from "./Wrapper";
      ```
   - you will get the error
      ```
      Attempted import error: './Wrapper' does not contain a default export (imported as 'NavBarContext').
      ```

- You could also export something you import from elsewhere and it would still work
   ```js
   //NavBarContext.js
   import React, {createContext} from 'react';

      const NavBarContext = createContext();

   export default NavBarContext;

   //This func component is the context object reference only
   //its Provider is where the current value is housed
   ```
   ```js
   //Wrapper.js
   import React, {useState} from 'react';
   import NavBarContext from "../context/NavBarContext";

   const Wrapper = ({children}) => { 
      //same as =({props}) ...{props.children}

      const [input, setInput] = useState("");
      return (
         <NavBarContext.Provider value={{input,setInput}}>
               {children}
         </NavBarContext.Provider>
      )
   }
   //export default Wrapper;

   //Doing a multiple export here exporting something I imported
   export { Wrapper, NavBarContext };     
   //then must import with { } in child component like below
   //import { NavBarContext } from "./Wrapper";  - works the same 
   ```
   
   > SideNote: in JavaScript, import file with `require` like `const navBarContext = require("./Wrapper")`


# CSS Styling

   >[React Virtual DOM & Attributes](https://reactjs.org/docs/dom-elements.html)

   1. style=JavaScript{} obj{}      ___Quick Test Only - Not recommeded for React coding___

      `<div style={{propKey: "value", propKey: "value", propKey: "value"}}> ... </div>`

      outer {} is JSX entering js expression; inner {} is the css objects
      > Note: 
      Some examples in the documentation use style for convenience, **but using the style attribute as the primary means of styling elements is generally not recommended.** In most cases, className should be used to reference classes defined in an external CSS stylesheet. style is most often used in React applications to add dynamically-computed styles at render time. See also FAQ: Styling and CSS.

   
   1. CSS Modules  **-React Supported by Default-**

      Create-react-app supports this CSS Modules by default, preserving original CSS syntax
      ```css
      /* MyButtonComponent.module.css */
      .btn {
         padding: 12px 15px; 
         font-family: Arial, sans-serif; 
         font-weight: bold;
         background: linear-gradient(30deg, rebeccapurple, magenta); 
         color: #fff; 
         border: none;
      }
      ```
      ```js
      // MyButtonComponent.js
      import React, { Component } from 'react';
      import styles from './MyButtonComponent.module.css';     //importing the module.css file as one module named "styles"
         
      class MyButton extends Component {
         render() {
            return <button className={ styles.btn }>{ props.children }</button>;  //call the modules.properties to call on the css styling
         }
      }
         
      export default MyButton;
      ```
      > What about non-class items?  Like tag element or #id?? how are they defined?
      > CSS filename must end in "module.css"
      > CSS class name cannot be hyphenated, and should be camelCase only. So no ".btn-Submit"; do ".btnSubmit"
      > Benefits of using module.css: 
      >   1. ok to use media queries
      >   2. css elements are completely encapsulated at the component level.  `.btn` styling only applies to the component importing the css module. class names are given unique hashes at build time to keep them isolated!
   
   1. Direct Import 
   
      Simply importing a regular .css file, similar to HTML way with <script></script>, preserving original CSS syntax
      ```css
      /* styles.css */
      .btn {
          padding: 12px 15px; 
          font-family: Arial, sans-serif;
          font-weight: bold;
          background: linear-gradient(30deg, rebeccapurple, magenta); 
          color: #fff; 
          border: none;
      }
      ```
      ```js
      // MyButtonComponent.js
      import React, { Component } from 'react';
      import './styles.css';        // <<<<<<< Importing .css file directly

      class MyButton extends Component {
          render() {
              return <button className="btn">{ props.children }</button>;  //<<<<<<<<< apply as normal HTML/CSS
          }
      }

      export default MyButton;
      ```
      > Drawback: styles are NOT encapsulated to the component.  .btn class styling will be applied elsewhere in app

      > ** used `className` in JSX, as `class` is a reserved word in JavaScript for the class component setup
   
   1. Inline Style

      defined styling in the same JSX file as the component (i.e. inline) just like any other object
      ```js
      // MyButtonComponent.js
      import React, { Component } from 'react';
      
      const btnStyle = {
         padding: '12px 15px',
         fontFamily: 'Arial, sans-serif',
         fontWeight: 'bold',
         background: 'linear-gradient(30deg, rebeccapurple, magenta)', 
         color: '#fff',
         border: 'none'
      };
      
      class MyButton extends Component {
         render() {
            return <button style={ btnStyle }>{ props.children }</button>;
         }
      }
         
      export default MyButton;
      ```
      > Drawback: 
      >   - media queries can't be used for responsiveness; 
      >   - doesn't support [CSS pseudo-classes](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements)
      >   - all integers must be quoted as strings; css name needs to be camelCase because it is existing in JSX file

   ---
   1. `{props.children}` - Whaaaatt?
      
      Some components don’t know their children at the time of building the component. This is especially common for components like Sidebar or Main that represent generic “boxes”.

      React recommends that such components use the special `{props.children}` to pass children elements directly into their output:
      ```js
      // Main.js                              //building the Main (parent) component
      import React from 'react';
      import styles from '../css/Main.module.css'; //just a div with color and padding to represent Main section block

      function Main(props) {                  //children is one kind of props
      return (
            <div className={styles.block}>    //Main wraps around child components
               {props.children}               //pre-warning to expect children
            </div>
      )
      }

      export default Main;
      ```
      ```js
      // App.js
      import Header from "./components/Header";
      import SideNav from "./components/SideNav";
      import Main from "./components/Main";
      import Content from "./components/Content";
      import FooterAds from "./components/FooterAds";

      function App() {
      return (
         <div className="App">
            <Header />
            <SideNav />
            <Main>                  // <<<<<<<< Main component with children Content and FooterAds
               <Content />          // these are the expected children from pre-warning
               <Content />          // similar to React.CreateElement("Main",{},
                                    //    React.CreateElement("Content",{},....),
               <Content />          //    React.CreateElement("Content",{},....),
               <FooterAds />        //    React.CreateElement("FooterAds",{},....))
            </Main> 
         </div>
      );
      }

      export default App;
      ```
      
      >[Props Containment](https://reactjs.org/docs/composition-vs-inheritance.html)

      >[Another Explanation](https://codeburst.io/a-quick-intro-to-reacts-props-children-cb3d2fce4891)

   1. CSS in JS Libraries - Dynamic Styling
      
      - Define styling using JavaScript dynamically
      - `npm install styled-components`
      - [Styled Components](https://styled-components.com/docs/basics#installation)
      - [Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)
      - [Styletron](https://github.com/styletron/styletron)
      - [emotion](https://emotion.sh/docs/introduction)

# Hooks

- useRef()

   1. Access DOM node - work with element's ref attribute to hold on to a reference to that specific DOM node element.  useRef creates that reference inside component
   - [useRef Hook](https://medium.com/trabe/react-useref-hook-b6c9d39e2022) - show both class and functional component coding
   - [React Refs n DOM](https://reactjs.org/docs/refs-and-the-dom.html)

- useState()

   - Class Component has `this.state` in props by default
      ```js
      import React, { Component } from 'react';

      class Counter extends Component {
         constructor(props) {
            super(props);
            this.state = {
               clickCount: 0
            }
         }
         
         handleClick = () => this.setState({
                 clickCount: this.state.clickCount + 1
             })

         render() {
            return (
               <div>
                     { this.state.clickCount }
                     <button onClick={ this.handleClick }>Click Me</button>
               </div>
            );
         }
      }
      export default Counter;
      ```

   - Functional Component has useState hook
      ```js
      import React, { useState } from 'react';     //importing hook from 'react'

      const Counter = props => {
         const [state, setState] = useState({      //destructing out of useState
            clickCount: 0                          //state: curr value
         });                                       //setState: change method

         const handleClick = () => {
            setState({
               clickCount: state.clickCount + 1
            });
         }

         return (
            <div>
               { state.clickCount }
               <button onClick={ handleClick }>Click Me</button>
            </div>
         );
      }
      export default Counter;
      ```
      > NOTE: When invoking useState, we do not need to pass in **an object** (above). We can just pass in a primitive value and then update it accordingly. You will more commonly see useState implemented as in the following example:

      ```js
      import React, { useState } from 'react';

      const Counter = props => {
         const [count, setCount] = useState(0);

         const handleClick = () => {
            setCount(count + 1);
         }

         return (
         <div>
            { count }
            <button onClick={ handleClick }>Click Me</button>
         </div>
         );
      }
      export default Counter;
      ```
   
   - clean up with useState()
      > clearing the input fields after submitting form
      ```js
      //UserForm.js
      import React, { useState } from  'react';

      const UserForm = (props) => {
          const [username, setUsername] = useState("");
          const [email, setEmail] = useState("");
          const [password, setPassword] = useState("");  

          const createUser = (e) => {
              e.preventDefault();
              const newUser = { username, email, password };
              console.log("Welcome", newUser);
              setUsername("") ;     // clear up Username input field after submitting form
          };

          return(
              <form onSubmit={ createUser }>
                  <div>
                      <label>Username: </label> 
      <!--            //<input type="text" onChange={ (e) => setUsername(e.target.value) } /> -->
                      <input type="text" onchange={ (e) => setUsername(e.target.value) } value={ username } />    // retrieve username value to whatever is currently set
                  </div>
                  <div>
               <label>Email Address: </label> 
               <input type="text" onChange={ (e) => setEmail(e.target.value) } />
         </div>
                  <div>
               <label>Password: </label>
               <input type="text" onChange={ (e) => setPassword(e.target.value) } />
         </div>
                  <input type="submit" value="Create User" />
              </form>
          );
      };
      export default UserForm;
      ```
   
   - Lifting State
      > Passing a function as props to the child component.  Once the child component runs this passed function, it will set the data back to parent component automatically which data can then be applied to another child component.

      > [Lifting State](https://reactjs.org/docs/lifting-state-up.html)
      ```jsx
      import React, {useState} from "react"; 

      function App() {
         const [currMsg, setCurrMsg] = useState("");  //lifting states to be shared in 2 child components
         // console.log(`app currMsg: ${currMsg}`);
         return (
         <div className="App">
            <MessageForm sendMsg={setCurrMsg}/>
            <MessageDisplay message={currMsg}/>
         </div>
         );
      }
      export default App;

      import React, {useState} from "react";

      const MessageForm = (props) => {
         const [msg, setMsg] = useState("");

         const handleSubmit = (e) => {
            e.preventDefault();
            props.sendMsg(msg);
            //console.log(`form submit: ${msg}`);
            setMsg("");
         }
         return (
            <form onSubmit={handleSubmit}>
               <h3>Enter a Message:</h3>
               <input
                  type="text"
                  onChange={(e) => setMsg(e.target.value)}
                  value={msg}
               ></input>
               <button type="submit" >
                  Send
               </button>
            </form>
         );
      };
      export default MessageForm;

      import React, {useState} from "react";

      const MessageDisplay = (props) => {
      //   const [msges, setMsges] = useState("");  
      //   setMsges(props.message);                //incorrect
      //   Error: Too many re-renders. React limits the number of 
      //   renders to prevent an infinite loop.

         return (
            <>
               {props.message ? <h4>New Message Sent:</h4> : ""}
               <p>{props.message}</p>
            </>
         );
      };
      export default MessageDisplay;
      ```

      >Another good example of using lift state is Freeze-or-Spoil before DB Data Store
      >... add here

# React Components Lifecycle
> https://www.w3schools.com/react/react_lifecycle.asp
- Each component has a lifecycle which can be monitored and mainpulated 
- Three lifecycle phases:
   - Mounting
   - Updating
   - Unmounting
   ---
   - Mounting
      > Remember: render() is required and will always be called.  The others are optional and will be called if defined.  
      - means putting elements into the DOM
      - React has four built-in methods that get called (in below order) when mounting a component:
         1. constructor()
            - called before anything else when the component is initialized
            - is the place to set up the initial state and other initial values
            - called with `props` as arguments
            - should always start by calling the `super(props)` to initiate the parent's constructor method and allow component to inherit methods from its parent (React.Component)
               ```jsx
               class Header extends React.Component {
                  constructor(props){
                     super(props);
                     this.state = {favoriteColor: "red"};
                  }
                  render() {
                     return ( <> ... </>);
                  }
               }
               ```
         1. getDerivedStateFromProps()
            - called right before rendering the elements in the DOM
            - natural place to set the state object based on the initial props
            - takes `state` as an argument, and returns an object with **changes** to the `state`
            - example: starts with the fav color being "red, but the getDerivedStateFromProps() updates teh fav color based on the favCol attribute:
               ```jsx
               class Header extends React.Component {
                  constructor(props) {
                     super(props);
                     this.state = {favoriteColor: "red"};
                  }
                  static getDerivedStateFromProps(props, state) {
                     return {favoriteColor: props.favCol };
                  }
                  render() {
                     return (
                        <h1>My Favorite Color is {this.state.favoriteColor}</h1>
                     );
                  }
               }
               ReactDOM.render(<Header favCol="yellow"/>, document.getElementById('root'));
               ```
         1. render()
            - required method
            - is the method that actually outputs the HTML to the DOM
               ```jsx
               ...
               ReactDOM.render(<Header/>, document.getElementById('root'));
               ```
         1. componentDidMount()
            - called AFTER the component is rendered
            - this is where you run statements that requires that the component is already placed in the DOM.
               ```js
               //at first fav Color is red, but after a second, fav Color is yellow instead
               class Header extends React.Component {
               constructor(props) {
                  super(props);
                  this.state = {favoriteColor: "red"};
               }
               componentDidMount() {
                  setTimeout(() => {
                     this.setState({favoriteColor: "yellow"})
                  }, 1000)
               }
               render() {
                  return (
                     <h1>My Favorite Color is {this.state.favoriteColor}</h1>
                  );
               }
               }

               ReactDOM.render(<Header />, document.getElementById('root'));
               ```
      

   - updating
      - next lifecycle phase is when a component is updated
      - a component is updated whenever there is a change in the component's state or props
      - React has five built-in methods that get called (in below order) when a component is updated:
         1. getDerivedStateFromProps()
         1. shouldComponentUpdate()
         1. render()
         1. getSnapshotBeforeUpdate()
         1. componentDidUpdate()
      - render() is required and will always be called.  The others are optional and will be called if defined.

   - Unmounting
      - next lifecycle phase is when a component is removed from DOM
      - React has one built-in method that gets called when a component is unmounted
         1. compononetWillUnmount()
      - componentWillUnmount() is called when the component is about to be removed fom the DOM


# Syntax Compare

- Class vs. Functional Component
   ```js
   //Class Comp
   import React , {Component} from 'react';

   class PersonCard extends Component{
      render() {
         return(
            <div>
               <h1>{ this.props.lastName }, { this.props.firstName }</h1>
               <p>Age: { this.props.age }</p>
               <p>Hair Color: { this.props.hairColor }</p>
            </div>
         );
      }
   }  
   export default PersonCard;
   <PersonCard firstName="John" lastName={"Smith"} age={ 8 } hairColor="Brown" /> 
   //same as Func Comp 
   //Note: we can pass down a string with or without curly braces.
   ```


   ```js
   //Functional Comp
   import React from 'react';

   const PersonCard = (props) => {
      return(
         <div>
            <h1>{ props.lastName }, { props.firstName }</h1>
            <p>Age: { props.age }</p>
            <p>Hair Color: { props.hairColor }</p>
         </div>
      );
   }
   export default PersonCard;

   <PersonCard firstName="John" lastName={"Smith"} age={ 8 } hairColor="Brown" /> 
   //same as Class Comp
   //Note: we can pass down a string with or without curly braces.
   ```

   ```js
   // could destructure in parameter
   import React from "react";

   function PersonCard({ Fn, Ln, age, hairColor }) {
   // function PersonCard(props) {   //same as above
   //   const { Fn, Ln, age, hairColor } = props;
      return (
         <>
            <h1>
               {Ln}, {Fn}
            </h1>
            <p>Age: {age}</p>
            <p>Hair Color: {hairColor}</p>
         </>
      );
   }
   export default PersonCard;
   ```

- `export default` === `function App()`
   
   `export default () =>` just skips naming the function as App, basically creating the function and exporting it in one step!
   
   `export default App` basically just exports the function named App just created
   ```js
   import React, { useRef } from 'react';

   export default () => {
       const input = useRef();

       function focusInput() {
           input.current.focus();
       }

       return (
           <>
               <input ref={input}/>
               <button onClick={focusInput}>Focus Me!</button>
           </>
       );
   }
   ```
   ```js
   import React, { useRef } from 'react';

   //const App = () => {            same as below too!
   function App() {
      const input = useRef();

       function focusInput() {
           input.current.focus();
       }

       return (
           <>
               <input ref={input}/>
               <button onClick={focusInput}>Focus Me!</button>
           </>
       );
   }

   export default App;
   ```

- ES6 Property Value Shorthand
   > if the key has the same name as the variable, shorthand works well
   ```js
   const newUser = { username: username, email: email, password: password };
   ```
   ```js
   const newUser = { username, email, password };
   ```

- Ternary Operators with/without
   > Advantage: replace function (formMessage in this case) with code that ca go directly into React JSX
   ```jsx
   import react, { useState } from  'react';
      
      
   const UserForm = (props) => {
      const [username, setUsername] = useState("");
      const [email, setEmail] = useState("");
      const [password, setPassword] = useState("");
      const [hasBeenSubmitted, setHasBeenSubmitted] = useState(false);
      
      const createUser = (e) => {
         e.preventDefault();
         const newUser = { username, email, password };
         console.log("Welcome", newUser);
           setHasBeenSubmitted( true );
      };
      
       const formMessage = () => {
          if( hasBeenSubmitted ) {
             return "Thank you for submitting the form!";
         } else {
             return "Welcome, please submit the form";
         }
       };
      
      return (
         <form onsubmit={ createUser }>
            <h3>{ formMessage() }</h3>
            <div>
                  <label>Username: <label> 
                  <input type="text" onchange={ (e) => setUsername(e.target.value) } />
            </div>
            <div>
                  <label>Email Address: </label> 
                  <input type="text" onchange={ (e) => setEmail(e.target.value) } />
            </div>
            <div>
                  <label>Password: </label>
                  <input type="text" onchange={ (e) => setPassword(e.target.value) } />
            </div>
            <input type="submit" value="Create User">
         </form>
      );
   };
   export default UserForm;
   ```
   ```jsx
   const createUser = (e) => {
         e.preventDefault();
         const newUser = { username, email, password };
         console.log("Welcome", newUser);
           setHasBeenSubmitted( true );
      };

   return (
      <form onsubmit={ createUser }>
          {   //accessing js expression
              hasBeenSubmitted ? 
              <h3>Thank you for submitting the form!</h3> :
              <h3>Welcome, please submit the form.</h3> 
          }   //done with js expression
          <div>
              <label>Username: <label> 
              <input type="text" onchange={ (e) => setUsername(e.target.value) } />
         </div>
      </form>
   );
   ```
   > Leveraging JS EMPTY string as being "falsy" to apply ternaries
   ```js
   const MovieForm = (props) => {
       const [title, setTitle] = useState("");
       const [titleError, setTitleError] = useState("");

       const handleTitle = (e) => {
           setTitle(e.target.value);
           if(e.target.value.length < 1) {
               setTitleError("Title is required!");
           } else if(e.target.value.length < 3) {
               setTitleError("Title must be 3 characters or longer!");
           }
       }

       {/* rest of component removed for brevity */}

       return (
           <form onsubmit={ (e) => e.preventDefault() }>
               <div>
                   <label>Title: </label>
                   <input type="text" onChange={ handleTitle } />
                   {
                       titleError ?
                       <p style={{color:'red'}}>{ titleError }</p> :
                       ''
                   }
               </div>
               <input type="submit" value="Create Movie" />
           </form>
       );
   }
   ```
- map() 
   - when applying map() inline with render()/return(), ensure to wrap code around {} to allow JS expression access
   - best to include `return( ...);` inside map() callback function
      ```js
      ...
      return (
         <>
            {tabs.map((tab) => {
               return (
                  <button type="submit" onClick={(e) => handleClick(e, tab)}> {tab} </button>
               );
            })}
            <div>
            <p>{tabText} content is showing here.</p>
            </div>
         </>
      );
      ...
         ...
      };
      export default Tab;
      ```
- Handling of `this` in regular functions vs. in arrow functions  
   - Conclusion: with arrow functions there is no binding of `this` to its DOM object.
   - In regular functions `this` represented the object that called the function, which could be the DOM window, the document, a button, etc.
      ```js
      class Header {
         constructor() {
            //do something to set up the Header obj
         }

         //Regular function:
         printThis = function() {
            document.getElementById("demo").innerHTML += this;  //innerHTML was initially blank
         }
      }

      myheader = new Header();

      //The window object calls/fires off the function when it loads:
      window.addEventListener("load", myheader.printThis);

      //A button object calls/fires off the function when it is clicked:
      document.getElementById("btn").addEventListener("click", myheader.printThis);

      //output:
      //"demo".innerHTML would print: [object Window] [object HTMLButtonElement]
      //                               (first loads)   (when btn is clicked)
      ```
   - In arrow functions `this` keyword **always** represents the object that defined the arrow function (Header instance/object in this case)
      ```js
      class Header {
         constructor() {
            //do something to set up the Header obj
         }

         //Arrow function:
         printThis = () => {
            document.getElementById("demo").innerHTML += this;  //innerHTML was initially blank
         }
      }

      myheader = new Header();

      //The window object calls/fires off the function when it loads:
      window.addEventListener("load", myheader.printThis);

      //A button object calls/fires off the function when it is clicked:
      document.getElementById("btn").addEventListener("click", myheader.printThis);

      //output:
      //"demo".innerHTML would print: [object Object] [object Object]
      //                               (first loads)   (when btn is clicked)
      ```
- 
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
- To review an older version of React (if I run into older React code), follow [this](https://www.w3schools.com/react/react_render.asp)

