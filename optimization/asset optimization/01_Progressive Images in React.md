```css
/* App.css */
body {
  padding: 10px;
}

.loading {
  filter: blur(10px);
}

.loaded {
  filter: blur(0px);
  transition: filter 0.5s linear;
}
```

```js
//App.js
import './App.css';
import ProgressiveImage from './ProgressiveImage';

import largeImg from './images/large.jpg';
import tinyImg from './images/tiny.jpg';

function App() {
  return (
    <>
      <h1>Progressive Image</h1>
      <ProgressiveImage
        src={largeImg}
        placeholderImg={tinyImg}
        height={'450'}
        width={'450'}
      />
    </>
  );
}

export default App;
```

```js
//ProgressiveImage.js

import { useState, useEffect } from 'react';
const ProgressiveImage = (props) => {
  const { height, width, placeholderImg, src } = props;
  const [imgSrc, setSrc] = useState(placeholderImg || src);

  const customClass =
    placeholderImg && imgSrc === placeholderImg ? 'loading' : 'loaded';

  useEffect(() => {
    const img = new Image();
    img.src = src; //src is the value from props
    img.onload = () => {
      setSrc(src);
    };
  }, [src]);

  return (
    <img src={imgSrc} className={customClass} height={height} width={width} />
  );
};

export default ProgressiveImage;
```
