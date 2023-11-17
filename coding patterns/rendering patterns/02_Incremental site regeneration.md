- Incremental site regeneration enables you to `use static-generation on a per-page basis`, `without` needing to `rebuild the entire site`.
- With ISR, you can retain the benefits of static while scaling to millions of pages.
- To use ISR, add the `revalidate prop` to `getStaticProps`
- I wanted to get updated data every time without manual build (next build && next export), so over here the revalidation comes into picture for ISG

```js
// ISG

export default function MyPosts(props) {
  return (
    <>
      My posts
      <ul>
        {props.myPosts.map((post) => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </>
  );
}

export async function getStaticProps(context) {
  const promise = await fetch(
    'https://api.jsonbin.io/v3/b/6342b4f62b3499323bd881c1'
  );
  const data = await promise.json();

  return {
    props: { myPosts: data.record.posts },
    revalidate: 10, //re-validate after every 10 seconds
  };
}
```
