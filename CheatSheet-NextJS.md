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
    - > ***QUESTION***: the part I don't totally get is the outcome of paths variable -  paths should be an array with a **list** of params obj of ids one for each post.  
    How does getStaticProps handle this **list** of params?  If it were meant to be just one specific id params, then how come I do not see a filter in getStaticPaths() to return just one param obj with id?

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

## Data Fetch - Dive Deep - [getStaticProps()](https://nextjs.org/docs/basic-features/data-fetching#getstaticprops-static-generation)
- `getStaticProps()`
    - Exporting an async function `getStaticProps()` and Next.js will pre-render this page at build time using the props returned by `getStaticProps()`
    ```js
    export async function getStaticProps(context) {
        return {
            props: {}, // will be passed to the page component as props object
        }
    }
    ```
    - Context Input: `getStaticProps()` can expect `context` as parameter
        - The context param is an **object** containing the following **keys**:
            - `params` key contains the route parameters for pages using dynamic routes
                - if the page name is `[id].js` then `params` key would have { id: ... }
                - use this together with `getStaticPaths()`
                - see [Dynamic Routing](https://nextjs.org/docs/routing/dynamic-routes) 
                    ```js
                    //context object would look like: 
                    { 
                        params: { id: ... },
                        preview: undefined,
                        locale: '',
                        locales: [],
                        defaultLocale: ''
                    }
                    ```
            - `preview` key == `true` if page is in the preview mode, otherwise == `undefined`
                - See [Preview Mode](https://nextjs.org/docs/advanced-features/preview-mode)
            - `locale` key contains the active locale if enabled
            - `locales` key contains all supported locales if enabled
            - `defaultLocale` key contains the configured default locale if enabled  
            &nbsp;

    - Object Output: `getStaticProps()` should return an object with:
        - `props` (obj): an optional object with the props that will be received by the page component; it should be a serializable object
        - `revalidate`: an optional amount in seconds after which a page re-generation can occur; defaults to `false` or no revalidating
        - `notFound`: an optional boolean value to allow the page to return a 404 status and page.
            > With `notFound: true` the page will return a 404 even if there was a successfully generated page before. This is meant to support use-cases like user generated content getting removed by its author.  

            > `notFound` is not needed for `fallback: false` mode in `getStaticPaths()` as only paths returned from `getStaticPaths()` will be pre-rendered.  
            ```js
            export async function getStaticProps(context) {
                const res = await fetch(`https://.../data`)
                const data = await res.json()

                if (!data) {
                    return {
                        notFound: true,
                    }
                }

                return {
                    props: { data }, // will be passed to the page component as props
                }
            }
            ```
        - `redirect` (obj): an optional redirect value to allow redirecting to internal and external resources; should match the format of `{ destination: string, permanent: boolean }` 
            > If for rare cases need to assign a custom status code (e.g. for older HTTP Clients to properly redirect), can use the `statusCode` property instead of the `permanent` property, but not both.

            > Redirecting at build-time is currently not allowed and if the redirects are known at build-time they should be added in `next.config.js`  
            ***Question***: Not sure I get this part because getStaticProps() IS run at build time.  Or is it just saying the redirect needs to be an object to be passed elsewhere like the example format and not a redirect action???
            ```js
            export async function getStaticProps(context) {
                const res = await fetch(`https://...`)
                const data = await res.json()

                if (!data) {
                    return {
                        redirect: {
                            destination: '/',
                            permanent: false,   // statusCode: 123,
                        },
                    }
                }

                return {
                    props: { data },            // will be passed to the page component as props
                }
            }
            ```

    - NOTE: can import modules in top-level scope for use in `getStaticProps()`.  Imports used in `getStaticProps()` will not be bundled for the client-side.  This means you can write server-side code directly in `getStaticProps()` including reading from the filesystem or a database.

    - NOTE: should not use `fetch()` to call an [internal-???] API route in `getStaticProps()`. Instead, should directly import the logic needed/used inside the API route [like import into the component-???].  Might need to refactor code for this approach.  Fetching from an external API is perfectly fine!

    - NOTE: should use `getStaticProps()` if:
        - data to render the page is available at build time ahead of a user's request
        - data comes from a headless CMS
        - data can be publicly cached (not user-specific)
        - page must be pre-rendered (for SEO) and be very fast - `getStaticProps()`generates HTML and JSON files, oth can be cached by a CDN for performance.  

    ### [Pay Attention to the ***Technical Details*** of `getStaticProps()` ](https://nextjs.org/docs/basic-features/data-fetching#technical-details)  
    - Only runs at build time
        - `getStaticProps()` runs only at build time, it does NOT receive data that's only avail during request time (query param or HTTP headers)
    - Write server-side code directly
        - `getStaticProps()` runs only on the server-side 
        - It will never be run on the client-side.
        - It wont be included in the JS bundle for the browser (no exposure security risk)
            - ie, you can write server-side code directly in `getStaticProps()` such as direct database queries without them being sent to browsers
    - Statically generates both HTML *and JSON*
        - JSON file holding the result of running `getStaticProps()`
        - JSON file will be used in client-side routing through `next/link` or `next/router`
        - ... [read important details here](https://nextjs.org/docs/basic-features/data-fetching#statically-generates-both-html-and-json)
    - Only allowed in a page
        - `getStaticProps()` can only be exported from a **page**. 
        - cannot export it from a non-page files 
            - restriction reason: React needs to have all the required data before the page is rendered
    

    &nbsp;  &nbsp;  
    > Important Points:  
    > Does `getStaticProps()` replace `useEffect()`?  
    > - No - two different things/functions!
    > - `useEffect()` is used to execute code ***when component is mounted on client side***, and ***when specific variables > change.***  
    >  - `getStaticProps()` is run ***only ONCE on server side and at build time.***  
    >  - And if trying to run `useEffect()` inside `getStaticProps()` will cause below error. `useEffect()`, as with all react hooks, is supposed to be inside/at-top-level-of the component function, not within any other functions.
    >     > Error: Invalid hook call. Hooks can only be called inside of the body of a function component.
    ```
    in next.js data is fetched on the server. This is the key aspect of server side rendering. The main purpose of server-side rendering, is sending populated page, so browser crawlers can analyze the response page and this help better seo for your page. When client makes a request, before sending the response, next.js runs getStaticProps or getServerSideProps.

    However useEffect runs on the client-side. The purpose of useEffect, to get data before components mount, so you can use that data inside the component.
    ```

    &nbsp;  
    > [Read more on Incremental Static Regeneration](https://nextjs.org/docs/basic-features/data-fetching#incremental-static-regeneration)

    &nbsp;  
    > [Read more on `getStaticProps()` usage ***with TypeScript***](https://nextjs.org/docs/basic-features/data-fetching#typescript-use-getstaticprops)


## Data Fetch - Dive Deep - [getStaticPaths()](https://nextjs.org/docs/basic-features/data-fetching#getstaticpaths-static-generation)
- `getStaticPaths()`
-
-
-


## Data Fetch - Dive Deep - [getServerSideProps()](https://nextjs.org/docs/basic-features/data-fetching#getserversideprops-server-side-rendering)
- `getServerSideProps()`
-
-
-
-
-





&nbsp;  &nbsp;  
## Built-In CSS Support
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