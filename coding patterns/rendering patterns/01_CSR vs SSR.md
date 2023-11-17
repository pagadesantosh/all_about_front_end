**CSR**

```js
//api fetch example
import { useEffect, useState } from 'react';
export default function MyPosts() {
  const [posts, setPosts] = useState;
  useEffect(() => {
    fetch('https://api.jsonbin.io/v3/b/6342b4f62b3499323bd881c1')
      .then((res) => res.json())
      .then((data) => {
        setPosts(data.record.posts);
      });
  }, []);
  return (
    <>
      My posts
      <ul>
        {posts.map((post) => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </>
  );
}
```

---

**SSR**

```js
export default function MyPosts(props) {
  return (
    <>
      My posts
      <ul>
        {props.posts.map((post) => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </>
  );
}

export async function getServerSideProps(context) {
  const promise = await fetch(
    'https://api.jsonbin.io/v3/b/6342b4f62b3499323bd881c1'
  );
  const data = await promise.json();

  return {
    props: { posts: data.record.posts },
  };
}
```
