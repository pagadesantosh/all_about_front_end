### ReactDOMServer

`ReactDOMServer` object <u>**enables you to render components to static markup**</u>.

#### - Typically it's used on a Node server:

```js
import ReactDOMServer from 'react-dom/server';
```

The **Server-Side-Rendering** is a popular technique <u>**_for rendering a client-side single page application on the server_**</u> and then sending a fully rendered page to the client.

- This allows for dynamic components to be served as static HTML markup
- Allows your site to have a faster first page load time, which is the key to a good user experience.
- Can be useful for SEO (Search Engine optimization) when indexing does not handle javascript properly.

```js
npm i express
```

```js
// All the content inside the build folder is going to be served as-is, statically by Express.

// server/server.js
import path from 'path';
import fs from 'fs';

import express from 'express';

import React from 'react'; //react
import ReactDOMServer from 'react-dom/server'; //react
import App from '../src/App'; //react App component

const PORT = 8080;
const app = express();

const router = express.Router();

const serverRenderer = (req, res, next) => {
  fs.readFile(path.resolve('./build/index.html'), 'utf8', (err, data) => {
    if (err) {
      console.error(err);
      return res.status(500).send('An error occurred');
    }
    return res.send(
      //core logic is to replace
      data.replace(
        '<div id="root"></div>',
        `<div id="root">${ReactDOMServer.renderToString(<App />)}</div>`
      )
    );
  });
};
router.use('^/$', serverRenderer);

router.use(
  express.static(path.resolve(__dirname, '..', 'build'), { maxAge: '30d' })
);

// tell the app to use the above rules
app.use(router);

// app.use(express.static('./build'))
app.listen(PORT, () => {
  console.log(`SSR running on port ${PORT}`);
});
```

Now in your client application, in your src/index.js, instead of calling **ReactDOM.render**, call **_ReactDOM.hydrate_**

```js
//has the additional ability to attach event listeners to existing markup once React loads.
ReactDOM.hydrate(<App />, document.getElementById('root'));
```

<u>**Points to remember:**</u>

- All the node.js code needs to be transpiled by Babel, as server-side node.js code does not know anything about JSX nor ES modules

```js
npm i @babel/register @babel/preset-env @babel/preset-react ignore-styles
```

<u>**Create an entry point in server/index.js**</u>

```js
require('ignore-styles');
require('@babel/register')({
  ignore: [/(node_modules)/],
  presets: ['@babel/preset-env', '@babel/preset-react'],
});

require('./server');
```

**Build the React application, so that the build/ folder is populated and run this:**

```js
# Build App
npm run build

# Run App on Express
node server/index.js
```
