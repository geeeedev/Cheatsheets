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

### React Features
- Virtual DOM vs. Real DOM
   - Real DOM: Document Object Model: UI elements tree of app
      - Everytime there is a change in the state of app UI, the DOM gets updated to represent that change.
      - Frequently manipulating the DOM affects performance, ie, slow.
      - DOM is represented as a tree data structure. After a change, the updated element and it's children have to be **re-rendered** to update the application UI.  
      - The re-rendering/re-painting of UI is what makes it slow.  Thus, the more UI components there are, the more expensive the DOM updates could be, since they would need to be re-rendered for every DOM update.
   
   - Virtual DOM: a virtual representation of the real DOM
      - Everytime the state of our app changes, the virtual DOM gets updated instead of the real DOM.
      - VDOM is faster and more efficient: When new elements are added to UI, a virtual DOM, represented as a tree, is created.  Each element is a node on this tree.  If the state of any of these elements changes, a new virtual DOM tree is created. The new tree is then compared, "diffed", with the previous virtual DOM tree to calculate the net changes/difference.  The subtree with changes then gets re-rendered to give the updated UI.  This updated tree is then batch updated to the real DOM, ensuring minimal operations on the real DOM, reducing performance cost of updating the real DOM.

   












