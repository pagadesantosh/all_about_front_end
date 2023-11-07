**loading="lazy"** is the attribute you need to provide to lazily load the images.

- What it does when it encounters the loading attribute with the lazy value, so if that particular image is `not in the viewport` of the user, then it is `not downloaded`.
- The moment you are `about to arrive` on that image then only the `network call happens` and the `image gets downloaded`.

- **Real Time scenario**: Infinite scrolling, ex: as the user scrolls the network api gets called to download that image

```js
//syntax:
<head>
<title>Lazy Load Images</title>
<meta name="viewport" content="width=device-width,initial-scale=1">
</head>

<body>
<img src="https://image.png" loading="lazy" width="401" height="401" alt="image1">
</body>
```
