```js
//App.js

import { useEffect, useRef, useState } from 'react';
import ProgressBar from './ProgressBar';
import './styles.css';

const totalMs = 15 * 1000;
const interval = 1 * 1000;
const totalCycles = totalMs / interval; //(ex: 15)
const progressMade = (interval / totalMs) * 100;

export default function App() {
  const [progress, setProgress] = useState(0);
  const timer = useRef();
  const cyclesCompleted = useRef(0);

  useEffect(() => {
    timer.current = setInterval(() => {
      setProgress((prevProgress) => prevProgress + progressMade);
      cyclesCompleted.current += 1;
      if (cyclesCompleted.current === totalCycles) clearInterval(timer.current);
    }, interval);

    return () => {
      clearInterval(timer.current);
    };
  }, []);

  return <ProgressBar progress={progress} />;
}
```

```js
//ProgressBar.js
import './progress-bar.css';

const ProgressBar = ({ progress = 0 }) => {
  return (
    <div className='progress-bar'>
      <div
        className='progress-bar-fill'
        style={{ transform: `translateX(${progress - 100}%)` }}
      />
    </div>
  );
};

export default ProgressBar;
```

```js
//progressBar.css
.progress-bar {
  position: relative;
  width: 300px;
  height: 30px;
  background-color: #f1dddd;
  border-radius: 15px;
  overflow: hidden;
}

.progress-bar-fill {
  position: absolute;
  height: 100%;
  width: 100%;
  background-color: rgb(146, 189, 82);
  transform: translateX(calc(100%));
  transition: transform ease-in 500ms;
}

```
