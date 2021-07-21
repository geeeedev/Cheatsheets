## Purpose: Remind myself how to get started with Next.js

[NextJS Start](https://nextjs.org/docs/getting-started)  
[NextJS API](https://nextjs.org/docs/api-reference/create-next-app)

- Start a next.js app  
    `npx create-next-app app-name-no-capital-letters`  
    `npx create-next-app --typescript` - TS flag to start a TypeScript project

- Run a next.js app and starts a production server  
   `npm start` or `npm run start`

- Run a next.js app in development mode  
   `npm dev` or `npm run dev`

- Run a production build which builds the app for production usage  
   `npm build` or `npm run build`

- Sets up Next.js' built-in ESLint configuration  
   `npm lint` or `npm run lint`

- Visit `http://localhost:3000` to view application in development server


### `/Pages`
- Next.js is built around the concept of pages.  
- A page is a React Component exported from a .js, .jsx, .ts, or .tsx file in the `pages` directory
- Each page is associated with a route based on the filename. `pages/about.js` maps to `/about`
- Static file serving `./public/` is mapped to '/'
- Next.js supports pages with dynamic routes.  `pages/posts/[id].js` maps to `/posts/1`, `/posts/2`, etc.


### Pre-rendering
- Next.js **pre-renders** every page by default: Next.js generates HTML for each page *in advance*, instead of having it all done by client-side JS.  
- Pre-rendering can result in better performance and SEO (Search Engine Optimization).
- Each generated HTML is associated with minimal JS code necessary for that page. When a page is loaded by the browser, its JS code runs and makes the page fully interactive - This process called Hydration.

#### Two Forms of Pre-rendering
- Difference is in **WHEN** it generates the HTML for a page
- Static Generation (SSG): The HTML page is generated at **build time** when you run `next build` or `npm build` and will be reused on each request. Can be cached by CDN.
- Server-Side Rendering (SSR): The HTML is generated on each request.
- Next.js lets us **choose** which pre-rendering we'd like to use for **each** page.  Can create a "hybrid" Next.js app by using SSG for most pages and SSR for a couple.
- SSG is better than SSR performance wise: Statically generated pages can be cached by CDN with no extra configuration to boost performance.  
- Can also use Client-side Rendering along with SSG or SSR.  That means some parts of a page can be rendered entirely by client side JS

