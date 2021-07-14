## Purpose: React Knowledge Review - Pros and Cons

> To review an older version of React (if I run into older React code), follow [this](https://www.w3schools.com/react/react_render.asp)
> 

## [React Pros & Cons](https://www.knowledgehut.com/blog/web-development/pros-and-cons-of-react)
- Virtual DOM
   - high performance JavaScript library 
   - React observes (follows the observable pattern) and listens for state changes, then update the Virtual DOM, diffing the changes with previous VDOM, then batch update only those changed objects in the real DOM.  
   - makes rendering efficient - fast display of a great number of components

- Component driven/Component based architecture 
   - makes it easy to divide-and-conquer, and greatly improves reusability
   - multiple components can be composed together to make complex 
   applications without losing their state in DOM
   - makes highly scaled Single Page App (SPA), in which content is dynamicaly loaded during user interaction without loading the entire page

- Redux in React
   - serves as a "manager" who manages data, provides a single source of truth for data ensuring all components are in synce with latest correct data
   - foces components to avoid talking to each other directly or dependent on each other
   - components send their data to redux; it is the responsibility of redux to update the components with new data
   - With Redux, components are always updated with the latest data available without having to depend on each other

- Flexible, Light-weight, and UN-opinionated (Pros)
   - does not force developers to follow any specific architecture pattern like MVC.  Development teams are free to choose their own style or patterns
   - not a lot of structure or scaffolding developers have to straightly follow 
   - no new pattern means less new terminologies, make it fast to learn (just JS), easy to use, and can be creative with it
   - React uses most of what JS is already available, making it very easy to start
   - allows vanilla JS developers to work with component-based architecture without having to lose the freeedom of vanilla JS

- being UN-opinionated could also be a **Cons** - Lack of Conventions/Standard (Cons)
   - Libraries and frameworks have global standards of what styles or patterns devs should follow. Without that standards, it is not easy for newcomers to predict what styles or standards React development teams follow
   - since it doesn't come with a structure or certain features like a framework would, will require more coding to get things done -eg. having to include additional libraries nad tools, such as Reach/Route for routing in React vs. routing is already part of the structure in C#.Net Core 
   - but I also think this is where the creativity and control come in - we can built on however we want it or apply third party npm

- SEO-friendly
   - due to Virtual DOM and component-based

- Mobile App Development
   - the flexibility of using the same library over web and mobile 
   applications
   - React Native allows us to create mobile applications on any mobile platform with the same React concepts and syntaxes, without having to learn a new tool or language

- High Pace of Development (Cons)
   - With React being rapidly growing and changing, forcing developers to update the way they code
   - cannot be easily adopted by applications where changes are critical to customers

- View-only/Not full-featured framework  (Cons)
   - echoes the Un-opinionated Cons. Compare to MVC, React only handles the view part.  For Controller and Model, additional libraries and tools would be needed, which could result in poor structore of code
   (whereas frameworks like Angular provide the complete MVC featured ground which is more structured and well managed.)
   - might require deeper understanding of JS and its core behavior to make React work the way we want it.  Whereas with frameworks like Angular (although it is more difficult to learn than React) force developers to follow a strict structure where you enjoy similar patterns as backend development

- Difficult to Maintain Documentation
   - React's rapid growth and changes make it difficult for the community to maintain documentation, making it challenging for new developers
- Data change are processed manually - no ORM (Cons)
- Not strongly typed - could cause mystery errors - but there's always TypeScript

- Developers' Perspective (Pros)
- Business Owners' Perspective (Pros)


## [React & Virtual DOM](https://programmingwithmosh.com/react/react-virtual-dom-explained/)
- Virtual DOM vs. Real DOM
   - Real DOM: Document Object Model: UI elements tree of app
      - Everytime there is a change in the state of app UI, the DOM gets updated to represent that change.
      - Frequently manipulating the DOM affects performance, ie, slow.
      - DOM is represented as a tree data structure. After a change, the updated element and it's children have to be **re-rendered** to update the application UI.  
      - The re-rendering/re-painting of UI is the most costly part of the process and is what makes performance slow.  Thus, the more UI components there are, the more expensive the DOM updates could be, since they would need to be re-rendered for EVERY DOM update.
   
   - Virtual DOM: a virtual representation of the real DOM
      - Everytime the state of our app changes, the virtual DOM gets updated instead of the real DOM.
      - VDOM is faster and more efficient: When new elements are added to UI, a virtual DOM, represented as a tree, is created.  Each element is a node on this tree.  
      - If the state of any of these elements changes, a new virtual DOM tree is created. The new tree is then compared, "diffed", with the previous virtual DOM tree to calculate the net changes/difference.  
      - The subtree with changes then gets re-rendered to give the updated UI.  This updated tree is then batch updated to the real DOM, ensuring minimal operations on the real DOM, reducing performance cost of updating the real DOM.

- React uses/leverages Virtual DOM
   - In React, every UI piece is a component, and each component has a state.  
   - React follows the observable pattern and listens for state changes.  When the state of a component changes, React updates the virtual DOM tree. Once the virtual DOM has been updated, React then compares the current version of the VDOM with the previous version of the VDOM - "diffing".
   - React then knows which virtual DOM objects have changed, batches these changes together, and updates only those objects in the real DOM. This makes the performance far better when compared to manipulating the real DOM directly.
   - All the details are abstracted away from React developers.  All you need to do is update the **states** of your components as needed and React takes care of the rest, ensuring a superior developer experience when using React.
   - React efficiently manages the most costly processing of re-rendering UIs by running batch updates to re-render UI 

- React render() function
   - render() is where the UI gets updated and rendered. 
   - render() is the required lifecycle method in React.
   - render() is the point of entry where the tree of React elements are created.
   - When a state or prop within the component is updated, the render() will return a different tree of React elements.  If you use setState() within the component, React immediately detects the state change and re-renders the component.
   - This is when React updates its virtual DOM first, then performs diffing to batch changes.

- Batch Update mechanism
   - React follows a batch update mechanism to update the real DOM.  This means that updates to the real DOM are sent in batches, instead of sending updates for every single change in state.  Hence, leading to increased performance.
   - The repainting of the UI is the most expensive part, and React efficiently ensures that the real DOM receives only batched updtaes to repain the UI.

- Recap - Virtual to Real
   - Frequent DOM manipulations are expensive and performance heavy.
   - Virtual DOM is a virtual representation of the real DOM.
   - When state changes occur, the virtual DOM is updated and the previous and current version of virtual DOM is compared. This is called “diffing”.
   - The virtual DOM then sends a batch update to the real DOM to update the UI.
   - React uses virtual DOM to enhance its performance.
   - It uses the observable to listen and detect state and prop changes.
   - React uses an efficient diff algorithm to compare the versions of virtual DOM.
   - It then makes sure that batched updates are sent to the real DOM for repainting or re-rendering of the UI.

## [React Lifecycle](https://programmingwithmosh.com/javascript/react-lifecycle-methods/) 
- React Lifecycle Events
   - the series of events that happen from the birth of a React component to its death.
   - Every component in React goes through a lifecycle of events.
      - Mounting Event - Birth of React component
      - Update Event - Growth of React component
      - Unmount Event - Death of React component

- React Lifecycle Methods (Common)
   - render() 
      ```js
      class Hello extends Component{
         render(){
            return <div>Hello {this.props.name}</div>
         }
      }

      const Hello = () => {
         //state
         //logic to modify state
         return (
            <div>Hello {props.name}</div>
         )
      }
      ```
      - most used lifecycle method, used in all React classes.
      - the only **required** method within a class component in React.
      - handles the rendering of components to the UI
      - happens during the **mounting** and **updating** events of components
      - returns JSX that is displayed in the UI.
      - could also return a null if there is nothing to render for that component.
      - method must be pure and simple - no side-effects
      - must always return the same output when the same inputs are passed, ie, no setState()/no modifying the component state within a render()
      - state modification should happen in other lifecycle methods, keeping render() pure

   - componentDidMount()
      - called as soon as the component has been moutned and ready
      - good place to initiate API calls, load data from a remote endpoint
      - allows modifying state using setState()
      - will update state and cause another rendering but will happen before the browser updates the UI, ensure that user will not see any UI updates with double rendering
      - best practice to ensure states are assigned in the constructor()
      - best to setState() for special cases like tooltips, modals, etc. when you would need to measure a DOM node before rendering something that depends on its position
      - use this pattern with caution to avoid unwanted performance issues

   - componentDidUpdate()
      - invoked as soon as UI updating happens
      - most common use case is updating the DOM in response to prop or state changes
      - can call setState() in this lifecycle event, must wrap it in a condition to check for state or prop changes from previous state
      - incorrect usage of setState() will lead to an infinite loop
      ```js
      componentDidUpdate(prevProps) {
         //Typical usage, don't forget to compare the props
         if (this.props.userName !== prevProps.userName) {  //userName has been updated
            this.fetchData(this.props.userName);            //fetchData with updated userName; no need to make the API call if props.userName did not change
         }
      }
      ```

   - componentWillUnmount()
      - called just before the component is unmounted and destroyed.
      - good place for any cleanup actions
      - common cleanup activities include clearing timers, cancelling API calls, clearing any caches in storage
      - canNOT modify the component state here, no setState() allowed, changes will never be re-rendered 
      ```js
      componentWillUnmount() {
         window.removeEventListener('resize', this.resizeListener)
      }
      ```

![](Screenshots/ReactComponentLifecycle.png)

- React Lifecycle Methods (UnCommon)
   - shouldComponentUpdate()
      - always return a boolean value responding to question "Should the componenet be re-rendered?"
      - handy when don't want React to render if state or prop has no changes because component re-renders by default anytime setState() **is called**
      - exists only for performance optimizations
      - must not update component state here
      - be cautious to not rely on it to prevent rendering of your component
      ```js
         shouldComponentUpdate(nextProps, nextState) {
            return this.props.title !== nextProps.title || 
            this.state.input !== nextState.input 
         }
      ```

   - static getDerivedStateFromProps()
      - called just before calling the render()
      - this is a static function that does NOT have access to "this." 
      - returns **an object to update state** in response to prop changes.
      - can return a null if there is no change to state
      - exits only for rare use cases where the state depends on changes in props in a component
      - is fired/executed on every render
      - example use case: a <Transition> component that compares its previous and next children to decide which ones to animate in and out
      - safer alternative to componentWillReceiveProps()
      ```js
         static getDerivedStateFromProps(props, state) {
            if (props.currentRow !== state.lastRow) {
               return {
                  isScrollingDown: props.currentRow > state.lastRow,
                  lastRow: props.currentRow,
               };
            }
            // Return null to indicate no change to state.
            return null;
         }
      ```

   - getSnapshotBeforeUpdate()
      - called right before the DOM is updated
      - value returned is passed on to componentDidUpdate()
      - should be used rarely or not used at all
      - example use case: resizing the window durnig an async rendering
      - safer alternative to componentWillUpdate()

![](Screenshots/ReactComponentLifecycle.png)

- Recap - Lifecycle Events and Method

   - React component lifecycle has three events – Mounting, Updating and Unmounting.

   - The render() is the most used lifecycle method.
      - It is a pure function.
      - You cannot set state in render()

   - The componentDidMount() happens as soon as your component is mounted.
      - You can set state here but with caution.

   - The componentDidUpdate() happens as soon as the updating happens.
      - You can set state here but with caution.

   - The componentWillUnmount() happens just before the component unmounts and is destroyed.
      - This is a good place to cleanup all the data.
      - You cannot set state here.

   - The shouldComponentUpdate() can be used rarely.
      - It can be called if you need to tell React not to re-render for a certain state or prop change.
      - This needs to be used with caution only for certain performance optimizations.

   - The two new lifecycle methods are getDerivedStateFromProps() and getSnapshotBeforeUpdate().
      - They need to be used only occasionally.
      - Should research for more examples to see how to properly implement them




- [Code Splitter in React](https://www.geeksforgeeks.org/code-splitting-in-react/)
   - supported by bundlers like Webpack, Rollup, Browserify
   - Webpack, Rollup, Browserify, etc. create multiple bundles that can be dynamically loaded at runtime
   - Code Splitter is a method that helps to generate bundles that are able to run dynamically, making code efficient because the bundle contains all required imports and files.
   - Bundling is the method of combining imported files with a single file.
   - With code splitting, "lazy loading" can be implemented, which means just using/loading the code which is needed at that time.
   ```js
   //Default Importing (no code splitting)
   import { add } from './math';

   console.log(add(x, y));
   ```
   ```js
   //Importing with code splitting
   import("./math").then(math => {
      console.log(math.add(x, y));
      });
   ```
   - As soon as [Webpack](https://webpack.js.org/guides/code-splitting/) gets this type of syntax, code-splitting is started automatically.
   - In Create-React-App, it is already set up and can be used immediately.