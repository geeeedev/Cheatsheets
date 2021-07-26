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


### [`/Pages`](https://nextjs.org/docs/basic-features/pages)
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
- Static Generation (SSG): The HTML page is generated at **build time** when you run `next build` or `npm build` and will be reused on each request. Can be cached by CDN
- Server-Side Rendering (SSR): The HTML is generated on each request
- Next.js lets us **choose** which pre-rendering we'd like to use for **each** page.  Can create a "hybrid" Next.js app by using SSG for most pages and SSR for a couple
- SSG is better than SSR performance wise: Statically generated pages can be cached by CDN with no extra configuration to boost performance
- Can also use Client-side Rendering along with SSG or SSR.  That means some parts of a page can be rendered entirely by client side JS
- SSG (with and without data) is recommended whenever possible since page can be built once and served by CDN, which makes it much faster than having a server render the page on every request
- SSG for many types of pages: Marketing pages, blog posts, e-commerce product listings, Help and documentation, etc.
- If you can pre-render a page ahead of users' request, SSG should be used.
- If a page shows frequently updated data, or its content changes on every request, SSR should be used, or do SSG with Client-side Rendering (skip pre-rendering some parts of a page and then use client-side JS to populate them)


#### Static Generation WITHOUT data
- By default, Next.js pre-renders pages using SSG without fetching data - just HTML elements.

#### Static Generation WITH data
- Page **content** depends on external data: Use `getStaticProps()`
    - Eg. page needs to fetch the list of blog posts from a CMS.
    - To fetch data on pre-render, `export` an `async` function called `getStaticProps()` from the same file.  
    - This function gets called at build time and passes fetched data to the page's `props` on pre-render.
    ```js
    //pages/posts.js
    //Need posts (by calling some API endpoints) before this component is pre-rendered
    function Blog({posts}){
        return (
            <ul>
                {posts.map((post) => (
                    <li>{post.title}</li>
                ))}
            </ul>
        )
    }
    //This gets called at build time
    //Fetch posts by calling external API endpoint
    //Returning { props: {posts} }, Blog component will receive posts as a prop at build time
    export async function getStaticProps(){
        const res = await fetch(`http://.../posts`);
        const posts = await res.json();

        return {
            props: {
                posts,
            }
        }
    }
    export default Blog;
    ```

- Page **paths** depend on external data: Use `getStaticPaths()` which then feeds into `getStaticProps()`
    - For pages with dynamic routes, what data to pre-render at build time depends on external feed
    - Eg. page with `pages/posts/[id].js` to show a single blog post based on id.
    - To fetch data for page **paths** on pre-render, `export` an `async` function called `getStaticPaths()` from a dynamically routed page `pages/posts/[id].js`.  
    - This function gets called at build time and (lets you specify which paths you want to pre-render???) (compile all the paths available???)
    ```js
    //pages/posts/[id].js
    function Post({ post }) {
        // Render 1 post...
    }

    // This function gets called at build time
    export async function getStaticPaths() {
        // Call an external API endpoint to get posts
        const res = await fetch('https://.../posts')
        const posts = await res.json()

        // Get the paths we want to pre-render based on posts
        const paths = posts.map((post) => ({
            params: { id: post.id },
        }))
        /**paths = 
        [ 
            { params: { id: '1' } },
            { params: { id: '2' } },
            { params: { id: '3' } }
        ]*/

        // We'll pre-render only these paths at build time.
        // { fallback: false } means other routes should 404.
        return { paths, fallback: false }
    }

    // This also gets called at build time
    export async function getStaticProps({ params }) {
        // params contains the post `id`.
        // If the route is like /posts/1, then params.id is 1
        const res = await fetch(`https://.../posts/${params.id}`)
        const post = await res.json()

        // Pass post data to the page via props
        return { props: { post } }
    }

    export default Post
    ```

#### Server-Side Rendering (aka Dynamic Rendering)
- Remember in SSR, the HTML page is generated on **each request**
- Need to `export` an `async` function `getServerSideProps()` which will be called by the server on every request
- Eg. A page needs to pre-render frequently updated data (fetched from an external API).  We can write `getServerSideProps()` which fetches this data and passes it to `Page`
- `getServerSideProps()` is similar to `getStaticProps()`; the difference is that `getServerSideProps()` is run on every request instead of on build time.
    ```js
    function Page({ data }) {
    // Render data...
    }

    // This gets called on every request
    export async function getServerSideProps() {
    // Fetch data from external API
    const res = await fetch(`https://.../data`)
    const data = await res.json()

    // Pass data to the page via props
    return { props: { data } }
    }

    export default Page
    ```

### Data Fetch




### Built-In CSS Support
- Next.js allows the import of CSS files

#### Global Stylesheet
- To add a stylesheet to your application, import the CSS file within `pages/_app.js`.
    ```js
    //pages/_app.js
    import '../styles.css'

    // This default export is required in a new `pages/_app.js` file.
    export default function MyApp({ Component, pageProps }) {
    return <Component {...pageProps} />
    }
    ```
- These imported styles will apply to **all pages and componenets** in the application.
- Due to the global nature of stylesheets, and to avoid conflicts, stylesheets must only be imported inside `pages/_app.js`
- In development, stylesheet imported inside _app.js allows styles to be hot reloaded as the page is being editted, keeping application state
- In production, all CSS files will be automatically concatenated into a single minified `.css` file

#### Import styles from `node_modules`
- Importing css files from `node_modules` is permitted anywhere in application (from Next.js 9.5.4 on)
- For global stylesheets `bootstrap` or `nprogress`, import its css file inside `pages/_app.js`
    ```js
    // pages/_app.js
    import 'bootstrap/dist/css/bootstrap.css'

    export default function MyApp({ Component, pageProps }) {
    return <Component {...pageProps} />
    }
    ```
- For CSS required by third party modules, import its css file inside individual application component
    ```js
    // components/ExampleDialog.js
    import { useState } from 'react'
    import { Dialog } from '@reach/dialog'
    import VisuallyHidden from '@reach/visually-hidden'
    import '@reach/dialog/styles.css'

    function ExampleDialog(props) {
        const [showDialog, setShowDialog] = useState(false)
        const open = () => setShowDialog(true)
        const close = () => setShowDialog(false)

        return (
            <div>
                <button onClick={open}>Open Dialog</button>
                <Dialog isOpen={showDialog} onDismiss={close}>
                    <button className="close-button" onClick={close}>
                    <VisuallyHidden>Close</VisuallyHidden>
                    <span aria-hidden>×</span>
                    </button>
                    <p>Hello there. I am a dialog</p>
                </Dialog>
            </div>
        )
    }
    ```