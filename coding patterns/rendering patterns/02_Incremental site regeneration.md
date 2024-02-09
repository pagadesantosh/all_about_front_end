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

```js
export default async function handler(req, res) {
  // Check for secret to confirm this is a valid request
  if (req.query.secret !== 'jscafe') {
    return res.status(401).json({ message: 'Invalid token' });
  }

  try {
    // this should be the actual path not a rewritten path
    // e.g. for "/blog/[slug]" this should be "/blog/post-1"
    const body = req.body;
    if (!body) return res.status(400).json({ message: 'Body missing' });
    const pathToRevalidate = body.pathToRevalidate;
    await res.revalidate(pathToRevalidate);
    return res.json({ revalidated: true });
  } catch (err) {
    // If there was an error, Next.js will continue
    // to show the last successfully generated page
    return res.status(500).send('Error revalidating');
  }
}
```

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/ded1813c-0fe5-416e-8926-1cc6f2b789cb)
