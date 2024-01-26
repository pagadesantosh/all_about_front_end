### Commmon security issues in javascript

- **Includes Cross-site-scripting (XSS)**:

  - <u>Sanitize user inputs, **_use Content Security Policy headers_** and **_encode user generated content_**</u>

<br/>

- **Cross site Request Forgery (CSRF)**:

  - <u>**_Use anti-CSRF tokens_**</u>, validate and sanitize inputs on the server side.

<br/>

- **Insecure data storage**:
  - Use <u>**_secure mechanisms for storing sensitive data_**</u>, such as **HTTPs**, **secure cookies** and **encrypted databases**.

---

### Explain the Same-Origin Policy in the context of JavaScript security.

- The **Same Origin Policy (SOP)** is a security measure in web browsers that <u>**_restricts web pages from making requests to a different domain_**</u> than the one that served the web page.
- This policy <u>**_prevents malicious scripts from accessing sensitive data across different regions_**</u>.
- To work around SOP, <u>**_developers can use techniques like Cross-Origin Resource Sharing (CORS) or JSONP_**</u>

-----

### What is the importance of HTTPS in securing web applications, and how does it work?

- HTTPS (Hyper Text Transfer Protocol Secure) is essential for securing data transmission between a user's browser and a website.
- It encrypts the data using SSL/TLS, preventing eavesdropping and man-in-the-middle attacks.
- HTTPS ensures the integrity and confidentiality of user data.
- To implement HTTPs, a website needs an SSL/TLS certificate, which verifies the site's identity and enables secure communication.

-----

###