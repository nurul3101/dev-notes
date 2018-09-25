## Server Side Rendering

Main aim of server side rendering is to decrease the time of first time appearance of content on the screen.

In the application traditionally there will be 2 servers
1) API Server
2) **Renderer Server**

API Server - Handles Authentication / Buisness Logic / DB Access.
It produces some JSON.

View Layer/ Renderer server -> Takes data and produces HTML.

By decoupling we make sure that in future in view layer we can replace it with any other framework.
It helps in scaling.

React Rendering Server is slow compared to hbs or other frameworks.

Node uses -> Common JS Modules
React uses -> ES6 Module Syntax.

Server side needs to handle JSX first before it can render.

Webpack and Babel are responsible for handling JSX on server side as well.

```renderToString()```

Render a React element to its initial HTML. React will return an HTML string. You can use this method to generate HTML on the server and send the markup down on the initial request for faster page loads and to allow search engines to crawl your pages for SEO purposes.

If you call ```ReactDOM.hydrate()``` on a node that already has this server-rendered markup, React will preserve it and only attach event handlers, allowing you to have a very performant first-load experience

renderToString converts your componenet into raw html and sends it to browser.

---

##### webpack

By default webpack assumes we are creating bundle for browser we need to specify if we want to create bundle for node.
specify target = 'node'
specify the entry file
specify output filename and its path
specify module -> rules -> conatins test,loader,exclude,options->preset.
E.g
```javascript
const path = require('path');

module.exports = {
  target: 'node',
  entry: './src/index.js',

  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'build')
  },

  module: {
    rules: [
      {
        test: /\.js?$/,
        loader: 'babel-loader',
        exclude: /node_modules/,
        options: {
          presets: [
            'react',
            'stage-0',
            ['env', { targets: { browsers: ['last 2 versions'] } }]
          ]
        }
      }
    ]
  }
};
```
---
### Universal / Isomorphic Javascript
Same code runs on the server and browser.


Initially for node side we used Common JS Modules but as we have implemented webpack now we can use ES2015 module

Only HTML is sent first in SSR we need to send the JS files afterwards to register the event handlers , action creators and other JS bundles.

we use two bundles
1) Server side bundle which runs on server
2) Client side bundle which runs on browser

Initial render is going to be on server and on the client side it will manually again re-render and compare it with HTML that already exists.

we give the same id on browser side in which we want to re render.
Traditionally we use id=root

### The process of giving life back to html i.e attaching event handlers and all the js stuff back is known as Hydration. 
```
# Process of re-rendering over already rendered content is known as 
Hydrating.
```

webpack merge is used for using same configuration in client and server webpack files.

Server side bundle is used because on server side we are using ES2015 modules and babel.

Client side bundle will be public and is the one which is sent after initial markup is rendered.

**npm run all command is used to run multiple scripts**

webpackNodeExternals library is used in our server side configuration because it will avoid copying react , express code into our bundle files as it will be already availbale through node_modules.

Server side bundle will not be shipped to the browser but using the externals will help is reducing the size of bundle and will boot faster.

For refactoring purpose we can separate the express and react logic in separate helper files.

---

*In SSR application express is going to delegate the requests to React Router and RR will be going to handle what content/HTML appears on the screen*

BrowserRouter is hard-coded to look a the URL Address bar and render but on server side there is no url address bar so instead we use StaticRouter in ServerSide Rendering

**We create a Routes.js file which contains mapping of routes and no specification of router.**

In Client.js file which will be sent to the browser we will be using browserrouter while in our renderer file which will be used on the server side we will be using StaticRouter.

Mismatch in html while hydarting will give us an HTML Mismatch error.
If we will not have implemented routing in server side

we have to specifically say to StaticRouter that this is the location as it does not have access to the Url bar so we forward the req object from the express side.

Redux needs different configuration on server and browser.

Aspects of auth needs to be handled on server. normally in browser

Need some way to detect when all initial data load action creators are completed on server.

Need state rehydration on browser

Redux will have two stores
1) For server bundle
2) For Client Bundle

server side store is going to behave different compared to client side store.
In client side we call action creator which passes through reducers and thats it.
In SSR we need to take care of when data is fetched.
First data will be loaded in the index.js file not in renderer.
After data has loaded then it will be provided to the Provider.

For using async await syntax we have to import babel-polyfill.

In server side componentDidMount() is not even called.
There is no time for fetching data and then rendering.
HTML is sent back instantly.

Rendering on server 2 times in not a viable solution.
we can only know which componenets to show after first render.

what traditionally we do is call the action creators to fetch data in componentDidMount which can only be achieved if we render the application.

Data Loading function is the way we implement redux in SSR.

---

#### *React Router Config library is used to let us know which componenets are to be rendered by looking at the url and for using this library we need to change the way we define routes*

Solution

Find which components to render based on url without rendering.
Call load data function.


renderRoutes , matchRoutes function are used.

while using redux on server we cannot use connect function as connect works with the Provider which is at the root of the application and we cannot access it before rendering.

we pass action creators in connect function which manages dispatching
Here we have to dispatch our action creators manually which will return promises.

We make store [reduxState] on server and with that create HTML and then throw away store which is not the case. we need to pass the state to the client side.  

In createStore second argument is initial state of store.

We send the state in form of json in HTML Template and used that in second argument of our client side redux store.

we use window.INITIAL_STATE to preserve the state.

[React Router Config Github Page](https://github.com/ReactTraining/react-router/tree/master/packages/react-router-config)

As an alternative we can use Pre-Rendering in React







<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg0Mjc0NzYxNF19
-->