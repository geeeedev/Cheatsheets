## Purpose: React Knowledge Review - Pros and Cons

> To review an older version of React (if I run into older React code), follow [this](https://www.w3schools.com/react/react_render.asp)

### React Pros & Cons
- Virtual DOM
   - high performance JavaScript library 
   - React observes (follows the observable pattern) and listens for state changes, then update the Virtual DOM, diffing the changes with previous VDOM, then batch update only those changed objects in the real DOM.  
   - makes rendering efficient - fast display of a great number of components
- Component driven/Component based architecture 
   - makes it easy to divide-and-conquer, and greatly improves reusability
- Light-weight, flexible, and UN-opinionated (Pros)
   - not a lot of structure or scaffolding developers have to straightly follow 
   - make it easy to use, fast to learn (just JS), and can be creative with it
- being UN-opinionated could also be a Cons 
   - since it doesn't come with a structure or certain features like a framework would, will require more coding to get things done -eg. having to include Reach/Route for routing in React vs. routing is already part of the structure in C#.Net Core 
   - but I also think this is where the creativity and control come in - we can built on however we want it or apply third party npm
- SEO-friendly
- View-only (Cons)
- Data change are processed manually - no ORM (Cons)
- Not strongly typed - could cause mystery errors - but there's always TypeScript

### React & Virtual DOM
- Virtual DOM vs. Real DOM
   - Real DOM: Document Object Model: UI elements tree of app
      - Everytime there is a change in the state of app UI, the DOM gets updated to represent that change.
      - Frequently manipulating the DOM affects performance, ie, slow.
      - DOM is represented as a tree data structure. After a change, the updated element and it's children have to be **re-rendered** to update the application UI.  
      - The re-rendering/re-painting of UI is what makes it slow.  Thus, the more UI components there are, the more expensive the DOM updates could be, since they would need to be re-rendered for every DOM update.
   
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

- React render() function
   - render() is where the UI gets updated and rendered. 
   - render() is the required lifecycle method in React.
   - render() is the point of entry where the tree of React elements are created.
   - When a state or prop within the component is updated, the render() will return a different tree of React elements.  If you use setState() within the component, React immediately detects the state change and re-renders the component.
   - This is when React updates its virtual DOM first, then performs diffing to batch changes.

- Batch Update mechanism
   - React follows a batch update mechanism to update the real DOM.  This means that updates to the real DOM are sent in batches, instead of sending updates for every single change in state.  Hence, leading to increased performance.
   - The repainting of the UI is the most expensive part, and React efficiently ensures that the real DOM receives only batched updtaes to repain the UI.

- Recap - Full Cycle
   - Frequent DOM manipulations are expensive and performance heavy.
   - Virtual DOM is a virtual representation of the real DOM.
   - When state changes occur, the virtual DOM is updated and the previous and current version of virtual DOM is compared. This is called “diffing”.
   - The virtual DOM then sends a batch update to the real DOM to update the UI.
   - React uses virtual DOM to enhance its performance.
   - It uses the observable to listen and detect state and prop changes.
   - React uses an efficient diff algorithm to compare the versions of virtual DOM.
   - It then makes sure that batched updates are sent to the real DOM for repainting or re-rendering of the UI.

### React Lifecycle
   - React Lifecycle methods
      - the series of events that happen from the birth of a React component to its death.
      - Every component in React goes through a lifecycle of events.
         - Mounting - Birth of React component
         - Update - Growth of React component
         - Unmount - Death of React component










