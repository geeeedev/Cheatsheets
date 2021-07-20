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
- Pages are associated with a route based on the filename. `pages/about.js` maps to `/about`
- Static file serving `./public/` is mapped to '/'

