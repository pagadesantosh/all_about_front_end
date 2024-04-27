## MISC
    - List various events available in React.
    - Local storage and session storage in the context of web browsers.
    - Difference between using cookies and local storage as we can achieve the same stuff with local storage/ session storage as well?
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
