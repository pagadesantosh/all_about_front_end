```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="index.css" />
  </head>
  <body>
    <img
      src="cat-500.jpg"
      srcset="cat-500.jpg 500w, cat-1000.jpg 1000w, cat-1500.jpg 1500w"
    />
  </body>
</html>
```

```css
img {
  /* width: 500px; */
  width: 100%;
}
```
