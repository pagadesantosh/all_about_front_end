### 1. List various events available in React.

#### Mouse Events
`onClick`: Triggered when a **mouse click** is detected.
`onDoubleClick`: Triggered when a **double click** is detected.
`onMouseDown`: Triggered when the **mouse button is `pressed`**.
`onMouseEnter`: Triggered when the mouse **pointer `enters` the element**.
`onMouseLeave`: Triggered when the mouse **pointer `leaves` the element**.
`onMouseMove`: Triggered when the mouse **pointer is `moving` over an element**.
`onMouseOut`: Triggered when the mouse **pointer `moves` `out` of an element**.
`onMouseOver`: Triggered when the mouse **pointer `moves` `over` an element**.
`onMouseUp`: Triggered when a mouse button is **`released over` an element**.

---

#### Keyboard Events
`onKeyDown`: Triggered when a **key is pressed `down`**.
`onKeyUp`: Triggered when a **key is `released`**.

---

#### Form Events
`onChange`: Triggered when the value of a `<input>`, `<select>`, or `<textarea>` element **has been changed**.

`onInput`: Triggered when an `<input>` or `<textarea>` value changes.

`onSubmit`: Triggered when a `form` is **submitted**.

--- 

#### UI Events
`onScroll`: Triggered when an element's scrollbar **is being `scrolled`**.
`onResize`: Triggered when a window or frame is `resized`.

----

#### Focus Events
`onFocus`: Triggered when an element **`receives` focus**.
`onBlur`: Triggered when an element **`loses` focus**.

-----

#### Drag Events
`onDrag`: Triggered when an element is **being `dragged`**.
`onDragEnd`: Triggered when a **drag operation is `completed`**.
`onDragEnter`: Triggered when a **dragged element `enters` a valid drop target**.
`onDragExit`: Triggered when an  **element is being dragged `leaves a valid drop` target**.
`onDragLeave`: Triggered when a **dragged element `leaves` a drop target**.
`onDragOver`: Triggered when an element is being `dragged over a drop` target.
`onDragStart`: Triggered when the user **`starts` `dragging`** an element.
`onDrop`: Triggered when a **dragged element is `dropped`** on a valid drop target.

----

#### Clipboard Events
`onCopy`: Triggered when the **user initiates a `copy` action** through the browser's user interface.
`onCut`: Triggered when the **user initiates a `cut` action** through the browser's user interface.
`onPaste`: Triggered when the **user initiates a `paste`** action through the browser's user interface.

--------

### 2. Local storage and session storage in the context of web browsers.

- Both are part of the Web Storage API which provides mechanisms for web applications <ins>**to store data in a web browser**</ins>.
- They allow the storage of data <ins>**in key-value pairs**</ins> and are more `intuitive` and `flexible` **than cookies**, with a `larger` `capacity`.

#### 1. localStorage

- provides a way to store data on the client's computer **for <ins>long-term storage**</ins>. 
- Data stored in localStorage <ins>**has no expiration time**</ins> 
- <ins>**remains stored**</ins> on the user's browser **until `explicitly` deleted**. 
- Changes made are saved and available for all `current` and `future` visits to the site.

#### Features of localStorage:
- **Persistence**: Data persists <ins>**even when the browser is `closed` and `reopened`**</ins>.
- **Capacity**: Typically allows about **5MB** of data to be stored, though this limit can vary by browser.
- **Scope**: Available from all windows/tabs with the same origin (protocol, host, and port).
- **Use Cases**: 
  - <ins>**Storing user preferences**</ins>, 
  - <ins>**saving the state**</ins> of a complex web application, 
  - or keeping user data available for prolonged periods without expiration.  

```js
// Storing data
localStorage.setItem('username', 'JohnDoe');

// Retrieving data
const username = localStorage.getItem('username');
console.log(username);

// Removing data
localStorage.removeItem('username');

// Clearing all data
localStorage.clear();
```

ii) sessionStorage
- sessionStorage is **`similar`** to localStorage in its method of storage, <ins>**but it has a shorter lifetime**</ins>. 
- Data stored in sessionStorage <ins>**gets cleared when the page session ends**</ins>. 
- A page session <ins>**lasts as long as the browser is open and survives over page reloads and restores**</ins>. 
- However, **opening a page in a new tab or window <ins>will start a new session</ins>**, which differs from localStorage where data is shared across all tabs and windows.

#### Features of sessionStorage:
- **Lifetime**: Data is **`cleared`** when the tab is closed.
- **Capacity**: Similar to localStorage, around `5MB` of data.
- **Scope**: Data is available **only within the `same` tab**/window that created it.
- **Use Cases**: 
  - Sensitive data that should not persist beyond the session, 
  - such as **form data entries** or 
  - single session-based games.

```js
// Storing data
sessionStorage.setItem('sessionName', 'SessionData');

// Retrieving data
const sessionData = sessionStorage.getItem('sessionName');
console.log(sessionData);

// Removing data
sessionStorage.removeItem('sessionName');

// Clearing all data within the session
sessionStorage.clear();
```
**Security**: 
  - Both are subject to the `same-origin` policy for security but do not transmit data with every server request like cookies, reducing the risk of interception by malicious actors.

----

### 3. Difference between using cookies and local storage as we can achieve the same stuff with local storage/ session storage as well?

#### 1. Storage Capacity
**Cookies**: Limited to about 4KB per cookie.
#### 2. Lifetime
**Cookies**: 
- Have expiration dates and can be set to persist past browser sessions until a specific expiration date. 
- They can also be made `session-only`, which expires when the browser session ends.
including page reloads and restores).

#### 3. Data Accessibility Across Sessions and Tabs
**Cookies**: 
- Data is sent automatically with every HTTP request made to the server, which can be used to maintain session state between the server and client.

#### 4. Security
**Cookies**: 
- Because **cookies are sent with every HTTP request**,
- they are **`vulnerable`** to cross-site request forgery (CSRF) attacks 
- and potentially to cross-site scripting (XSS) **if not properly secured with flags like `HttpOnly`**.


**localStorage/sessionStorage**: 
  - Generally more secure from interception, as the data is never transferred to the server unless explicitly done so by the client-side script. 
  - However, they are **still susceptible to XSS attacks** which can <ins>**allow an attacker to access storage through malicious scripts**</ins>.


#### 5. Use Cases
**Cookies**:
- Managing user sessions.
- Tracking user behavior for analytics.
- Personalization (storing user preferences and themes).


#### 6. Server Accessibility
**Cookies**: 
  - **Automatically sent to the server with every HTTP request**, which can be used to handle server-side read/write.

**localStorage/sessionStorage**: 
  - **Not accessible to the server** directly; 
  - data stored must be sent explicitly via AJAX or other HTTP methods if needed on the server.

----

    - Explore techniques for handling authentication and OAuth tokens on a web application's front-end.
    - JSX & component composition in React.


## React
    Describe your strategies which you have followed in your past for enhancing the performance of React applications
    different stages of react app
    What is JSX . Why do we need it. Does browser understands JSX directly
    do we have alternate for jsx
    props vs state
    arrays vs lists in react
    how can we decide right key to pass to list item
    which one you choose flux vs redux and why?
    Discuss the importance of routing in web applications and its relevance to React.
 
## Others
### what is difference between access token and id token
     
**Access Token**
- **Purpose**: 
  - An access token is **used to grant access to a resource**. 
  - It acts as a kind of "key" that **allows the holder to access APIs or resources securely**. 
  - The primary purpose of an access token is to **authorize API requests** made on behalf of the user.
- **Content**: 
  - Access tokens usually contain `scopes` and `grants` that specify what actions the application can perform and on what resources. 
  - They do not necessarily need to be understandable by the client or the resource owner.
- **Format**: 
  - The format of an access token can be opaque (such as a random string) or structured (such as `JWT` - JSON Web Tokens), depending on the authorization server. 
  - In the case of `JWT`, the token can carry a payload of claims, but these are meant for authorization, not for client use.
  
- **Usage**: 
  - It is **used by a client application to make authenticated requests to a server** or `API` that knows how to validate the token and check the permissions (scopes).



    code review steps you do
    You have an app with so many fields in the form. How do you show to user? How do you prevent repeated clicks of button?


## Below is a use case. How can we achieve this in react
    5 components that will call 5 different services to get data
    2 components should automatically rerender after every 30 secs
    3 components should rerender on click of a button
 
    use of pure component?
    can we make database call directly from react app? is it suggestible to do if possible?
    Have you worked on RestAPI services in backend or are you a pure frontend dev?
    What is synthetic event in react. Have you used in your project? What it will do?
