## Purpose: Understand the Difference between a Library and a Framework

> [Libraries and Frameworks are code someone else wrote/templated to solve common problems that I could implement in writing my application](https://fmontes.com/blog/difference-between-reactjs-and-nextjs)



| Library | Framework |
| :--- | :--- |
| solve a specific problem in app | everything we use to develop a web app. <br> A collection of libraries that work together in some opinionated way to help build a fully function app|
| Popular JS libraries: | Popular JS frameworks: |
| Routing: Reach/Router | Angular: provide routing, fetching data, coponents, testing, etc. |
| Dates Management: date-fns (Modern JS date util library) | Nuxt.js same as Next.js but instead of React.js, uses Vue |
| Transform data: Parsley (form validation library), Ramda | Express.js: is NodeJS framework for the server |
| | |


| ReactJS | [NextJS](https://nextjs.org/learn/basics/create-nextjs-app) |
| :--- | :--- |
| JS library that builds UI using components as building blocks | JS framework with a set of libraries that work together to build a web app, with one of the libraries being ReactJS |
| does **one part** of all the web app - build UI components to show content | builds all parts of the web app |
| | Other libraries used by NextJS: |
| | next/router: for routing and navigation |
| | next/link: a component that allows web app to link pages and allows lazy loading data |
| | next/image: a component to load images into the pages in the most performant way |
| ReactJS as a library is part of a framework, the UI components part | NextJS as a framework allows you to use ReactJS library to build UI components and pages for a web app. |
| Special Feature: | |
| | Next.JS lets you choose which pre-rendering (SSG/SSR) to use for each page, creating a hybrid app using SSG for most pages and SSR for others! |
| | |


![](./Screenshots/React-vs-Next.jpg)
<!-- ![](Screenshots/React-vs-Next.jpg) samd as above -->