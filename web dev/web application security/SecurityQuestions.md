#### 1. XSS vulnerability. Interviewers are especially looking out for this whenever you need to render user input. You almost never need to use .innerHTML. There's .textContent and $.text(). If you do have to render raw HTML, make sure you escape the contents first.

#### 2. User input that is being displayed in the URL has to be encoded first as well, or else there's also a potential for mischief where users can add additional query parameters.

---

### Cross Site Scripting (XSS):

- Cross-Site Scripting is a security vulnerability that **_allows an attacker to inject malicious scripts_**
- These **_scripts then execute in the context of the victim’s browser_**, potentially stealing sensitive information, hijacking user sessions, or performing other malicious actions.

**There are three main types of XSS attacks:**

- **Stored XSS**:

  - The malicious script is <u>**_stored on the web server_**</u> and served to users who visit a particular page or view a specific message
    <br>

- **Reflected XSS**:
  - The malicious script is embedded in a URL or another input field and the victim is tricked into clicking on a crafted link.
    <br>
- **DOM-based XSS**:
  - The attack occurs entirely on the client side, manipulating the Document Object Model (DOM) of a web page.
    <br>

**Points to remember**

- To prevent XSS attacks, developers **_should validate and sanitize user inputs_**, **_use output encoding_**, and **_implement security headers_** like **_Content Security Policy (CSP) to restrict the sources_** of executable scripts.
