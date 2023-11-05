```js
//index.html

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <link href="./style.css" rel="stylesheet" />
    <title>Static Template</title>
  </head>
  <body>
    <div class="parent">
      <header>This is header</header>
      <div class="left-sidebar">
        I am left sidebar
      </div>
      <main>
        I am main content
      </main>
      <div class="right-sidebar">
        I am right sidebar and I am having more text
      </div>
      <footer>
        I am footer
      </footer>
    </div>
  </body>
</html>

```

```js
//css

html,
body {
  padding: 0;
  margin: 0;
}
.parent {
  height: 100vh;
  display: grid;
  grid-template-columns: 100px 1fr 100px;
  grid-template-rows: 40px 1fr 40px;
}

header,
footer,
.left-sidebar,
main,
.right-sidebar {
  padding: 10px;
}

header {
  grid-column: 1 / 4;
  background-color: red;
}

.left-sidebar {
  grid-column: 1 / 2;
  background-color: green;
}

main {
  grid-column: 2 / 3;
  background-color: plum;
}

.right-sidebar {
  grid-column: 3 / 4;
  background-color: greenyellow;
}

footer {
  grid-column: 1 / 4;
  background-color: blue;
  color: white;
}

@media (max-width: 768px) {
  .parent {
    grid: repeat(5, 1fr) / 1fr;
  }
  header,
  footer,
  .left-sidebar,
  main,
  .right-sidebar {
    grid-column: 1 / 2;
  }
}

```
