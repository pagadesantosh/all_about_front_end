### Portals in React

- Portals provide a quick and seamless <u>way to render children into a DOM node</u> <u>**_that exists outside the DOM hierarchy of the parent component_**</u>

```js
ReactDOM.createPortal(child, container);
```

**Features**:

- It transports **_its children component into a new React portal_** <u>which is appended by default to document body.</u>
- It can also target user specified DOM element
- Supports server side rendering
- Supports returning arrays (no wrapper divs needed)
- It uses Portal and PortalWithState so there is no compromise between flexibility and convenience.

**When to use**:

- Modals
- Tooltips
- Floating menus
- Widgets

**Installation**

```js
npm i react-portal
```

```js
//Example
import React from 'react'
import ReactDOM from 'react-dom'

function PortalDemo(){
    return ReactDOM.createPortal(
        <h1>Portal Demo</h1>
        document.getElementById('portal-root')
    )
}
export default PortalDemo
```

Now, open the Index.html file **and add a element to access the child component outside the root node**.

```html
<!-- index.html -->

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="shortcut icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="theme-color" content="#000000" />
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    <title>React App using Portal</title>
  </head>
  <body>
    <noscript>It is required to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
    <div id="portal-root"></div>
  </body>
</html>
```
