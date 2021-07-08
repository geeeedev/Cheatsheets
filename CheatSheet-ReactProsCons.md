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















