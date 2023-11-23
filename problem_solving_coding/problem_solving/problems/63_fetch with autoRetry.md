## fetch with autoRetry

**Approach Taken**

1. async function fetchWithAutoRetry takes two parameters: this function has try catch
2. 1st param is a function that performs the api call, 2nd param is the maxCount it can retry for
3. try will simply call the function (ex: return await fetchAPIURL())
4. catch will have 2 things, if count <=1 then throw new Error('Max retry exceeded')
5. recursively call the function with count-1 (ex: return await fetchWithAutoRetry(fetchResource, count - 1))
6. fetchResource function return fetch(url).then(res)=>{return res.json()}.then((data)=>{return data}).catch((err)=>{throw err})
7. million dollar question is fetchWithAutoRetry(()=>fetchAPIURL(url), maxCount).then(()=>{}).catch(()=>{})

```js
async function fetchWithAutoRetry(fetchResource, count) {
  try {
    // Attempt the fetch call
    //Here, the function awaits the resolution of the fetchResource function. If fetchResource throws an error (for example, a network failure or server error), control moves to the catch block.
    return await fetchResource();
  } catch (error) {
    if (count <= 1) {
      // If the retry count has been exceeded, throw the error
      throw new Error('Maximum retry attempts exceeded');
    }

    // If there's an error, and we haven't exceeded the retry count, try again
    return await fetchWithAutoRetry(fetchResource, count - 1);
  }
}

// Usage Example
function fetchResource(url) {
  return fetch(url)
    .then((response) => {
      if (!response.ok) {
        // Handle HTTP errors
        throw new Error(`HTTP error: Status ${response.status}`);
      }
      return response.json();
    })
    .then((data) => {
      // You can add additional checks here for data validity
      return data;
    })
    .catch((error) => {
      // Network failures and other errors are caught here
      throw error;
    });
}

const maxRetries = 3; // Maximum number of retries
const url = 'https://jsonplaceholder.typicode.com/posts/1';

fetchWithAutoRetry(() => fetchResource(url), maxRetries)
  .then((data) => console.log('Data fetched:', data))
  .catch((error) => console.error('Failed to fetch data:', error));
```

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/89d13951-e09f-41bf-9ea7-b2388746a80b)
