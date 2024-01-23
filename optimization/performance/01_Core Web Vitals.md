### Core Web Vitals

- Web vitals are set of metrics related to speed, responsiveness and visual stability, to help site owners measures user experience on the web and identify opportunities to improve.

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/05f2806f-e67f-47e9-872c-b8a0299874ca)

- The current set of metrics focusses on three aspects of the user experience - **_loading, interactivity, visual stability_**

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/bcc6d834-870e-4956-8d87-06cd67e2cb03)

**1. Largest Contentful Paint (LCP):** measures loading performance of a page.

- To provide a good user experience, LCP should occur **_within 2.5 seconds_** of when the page first starts loading.
- LCP metric **_reports the render time of the largest image or text block visible within the viewport_**, relative to when the user first navigated to the page.
- Ex: As per google, a LCP of under 2.5 seconds for 75th percentile of users is considered as good.

**Example:** The LCP in the image below is 2.4 seconds which means that it took 2.4 seconds for the image to get visible to the user from the time user opened the page.

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/8cd3acbf-9635-4b4f-a97b-d1d308b7bd32)

#### To optimize LCP, let’s discuss few best practices:

#### 1. <b><u>Server Side Rendering(SSR) with React:</u></b>

- Using frameworks like <u>**_Next.js for SSR can significantly improve LCP_**</u> by sending a <u>**_fully rendered page in response_**</u> to a browser request.
- In SSR, <u>**_the server pre-renders the HTML with data_**</u> before sending it to the browser in response to a request.
- When a user requests the page, <u>**_Next.js fetches the data on the server and renders the page_**</u> with the product data before sending it to the browser. This <u>**_results in a fully rendered HTML page being sent in response_**</u> to the browser request, <u>**_which can significantly improve LCP because there's no need for additional client side rendering_**.</u>

```js
//Server Side Rendering with Next.js

import React from 'react';

function HomePage({ products }) {
  return (
    <div>
      {products.map((product) => (
        <div key={product.id}>
          <h2>{product.name}</h2>
          <p>{product.description}</p>
        </div>
      ))}
    </div>
  );
}

export async function getServerSideProps() {
  //Fetch products from an API endpoint at build time or on each request
  const response = await fetch('https://api.example.com/products');
  const products = await response.json();

  return {
    props: { products },
  };
}
export default HomePage;
```

---

- Whereas **in Client Side Rendering**, the <u>**_browser initially receives an empty HTML shell_**</u>. Then <u>**_it needs to fetch data via Javascript and render the content on the client side_**.</u> This additional step <u>**_can delay the rendering of the largest contentful element_**</u>, leading to slower LCP times.

```js
// ProductList.js (Client-Side Rendering)
import React, { useEffect, useState } from 'react';

function ProductList() {
  const [products, setProducts] = useState([]);

  useEffect(() => {
    // Fetch products from an API endpoint
    fetch('/api/products')
      .then((response) => response.json())
      .then((data) => setProducts(data));
  }, []);

  return (
    <div>
      {products.map((product) => (
        <div key={product.id}>
          <h2>{product.name}</h2>
          <p>{product.description}</p>
        </div>
      ))}
    </div>
  );
}

export default ProductList;
```

#### 2. <b><u>Optimization of Images with 'srcset':</u></b>

- using responsive images ensures that only suitable image sizes are loaded on different devices.

```js
function ResponsiveImages() {
  return (
    <img
      srcSet='small.jpg 320w, medium.jpg 480w, large.jpg 800w'
      sizes='(max-width: 320px) 280px, (max-width: 480px) 440px, 800px'
      src='medium.jpg'
      alt='Description'
    />
  );
}
```
![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/020d784b-dd91-4453-a95a-111d0468049f)


#### 3. <b><u>Use React's memo for Pure components:</u></b>
- Prevents re-renders for the components that receive the same props

```js
const MyComponent = React.memo(AnotherComponent)
```

---

**You can read more about how to improve LCP here** — https://web.dev/articles/optimize-lcp

---

**2. First Input Delay (FID)**: measures interactivity.

- FID measures the time from when a user first interacts with a page (i.e, when they click a link, tap on a button, or use a custom, javascript powered control) to the time when the browser is actually able to begin processing event handlers in response to that interaction.

- To provide a good user experience, pages should have a FID of **_100 milliseconds_** or less

You can read more about FID here — https://web.dev/articles/fid

---

**3. Cumulative Layout Shift (CLS)**: measures visual stability.

<img src="https://miro.medium.com/v2/resize:fit:1400/format:webp/1*yGTfSAZdfrphqPgSQRJSOg.gif">

- CLS measures the unexpected shifting of web elements while the page is being rendered.
- This is very annoying for the users and sometimes can actually can do financial damage to users.

- For ex: If you look into the above GIF, the user actually intended to click on "No, go back" button but due to CLS the button which placed the order.

- To provide a user experience, pages should **_maintain a CLS of 0.1 or less_**

You can read more about CLS here — https://web.dev/articles/cls

---

**Note:** For each of the above metrics, to ensure you're hitting the recommended target for most of your users, a good threshold to measure is the **_75th percentile_** of page loads.

---

Some more web vitals we should be aware of:

**First Contentful Paint (FCP)**:

- FCP measures how long it takes the browser to render the first piece of DOM content after a user navigates to your page.
- Images, non-white canvas elements, and SVGs on your page are considered DOM content; anything inside an iframe isn't included.

Read more about FCP here — https://web.dev/articles/fcp

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/6bdff6e1-5fd8-493b-b095-f036e788b6f9)

---

**Interaction to Next Paint (INP):**

- INP is a metric that **_assesses a page's overall responsiveness to user interactions_** by observing the latency of all click, tap and keyboard interactions **_that occur throughout the lifespan of a user's visit to a page_**.

- The final INP value is the longest interaction observed, ignoring outliers.

- INP will soon replace FID as a core web vital.

---

**Time to First Bite (TTFB)**:

- TTFB is a metric that measures the time **_between the request for a resource_** and **_when the first byte of a response begins to arrive_**.

TTFB is the sum of:

- Redirect time
- Service Worked Startup time (if applicable)
- DNS lookup
- Connection and TLS negotiation
- Request, up until the point at which the first byte of the response has arrived.

---

**Total Blocking Time(TBT)**:

- The Total Blocking Time (TBT) metric measures the total amount of time after First Contentful Paint (FCP) where the main thread was blocked for long enough to prevent input responsiveness.

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/26bab05a-2c89-46ca-a40e-3889bfff7411)

---

**Speed Index**:

- Measure how quickly the page's content becomes visible to the user

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/90b7e2de-3103-4975-94c1-ca9df451a13a)
