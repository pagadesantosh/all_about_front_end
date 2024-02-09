### Static Site Generation

- Where you will build the HTML once only during the build time and you deploy that build somewhere on your server (Ex: EC2)
- So by this, We created a static HTML file once during the build time
- Once content is generated it is same for every customer on your website (Ex: blogs)

```js
export default function MyPosts(props){
    return(
        <>
        There are my Posts
        <ul>
        {props.posts.map((post)=><li key={post.id}>{post.title}</li>)}
        </ul>
        <>
    )
}

//SSG
// Following code is fetching the data on the server

export async function getStaticProps(context){
    const promise = await fetch('https://api.jsonbin.io/v3/b/6342b4f62b3499323bd881c1')
    const data = await promise.json()

    return{
        props: {
            posts: data.record.posts
        }
    }
}
```

- Below code is to generate static site on client (Fetching the data on the client instead of fetching the data on the server )

```js
import { useEffect, useState } from 'react';

export default function MyPosts(props) {
  const [posts, setPosts] = useState([]);

  useEffect(() => {
    async function fetchData() {
      const promise = await fetch('URL');
      const data = await promise.json();
      setPosts(data.record.posts);
    }

    fetchData();
  }, []);

  return (
    <>
      There are my posts
      {posts.length ? (
        <ul>
          {posts.map((post) => (
            <li key={post.id}>{post.title}</li>
          ))}
        </ul>
      ) : (
        'Loading from API'
      )}
    </>
  );
}
```
