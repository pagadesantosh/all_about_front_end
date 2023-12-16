#### How do you define HTML5?

HTML5 is the most recent rendition of the Hypertext Markup Language, also referred to as the WWW (World Wide Web)'s fundamental language. This markup language augments a text file with bits of code, and this code, which we call markup, describes the structure of the document.

HTML5 introduces some new features including:

- Adding new parsing rules to enhance flexibility.
- Adding New attributes.
- Allow offline editing.
- Support (Web SQL)
- Support Protocol and MIME handler registration. These features can be used to change the way of user interaction with documents.

---

#### Advantages of using HTML5.?

HTML5 is the most recent rendition of HTML. HTML5 allows the creation of easier and more interactive websites by embedding video, audio, and graphics on the web page.

HTML5 supports multimedia technology and graphical content to the web without using any third-party plugins.

##### Some of the most important features added by HTML5 include:

- Geolocation
- Offline Application Cache
- Client-side database
- Error handling
- New Structure and new multimedia elements
- Browser Support and compatability

##### Supports Some New Application Programming Interface (API) like:

- Browser History management
- Drag and Drop
- 2D drawing on a web app
- Time media playback

##### Supported Applications include:

- Web Workers - javascript
- Local File access
- Application Cache
- Local data storage
- Local SQL databases

---

#### What are W3C and WHATWG?

- The World Wide Web Consortium (W3C) is a community of developers working towards setting global standards for development.

- WHATWG is short for Web Hypertext Application Technology Working Group. It was created during a W3C workshop by Apple, Mozilla and Opera Software in 2004. WHATWG is a community of developers focused on setting HTML standards to improve on user needs.

---

#### What are tags in HTML?

An HTML tag tells the browser how to render the HTML web page in a certain defined format. HTML uses angular brackets, < and >, to enclose the tags, the symbol / for closing the tag, and is used for many reasons like:

- changing the appearance of text,
- showing a graphic,
- linking to another web page.

For Example:

```js
<title> Educative - Interactive Learning </title>
```

---

#### What is an ‘attribute’ in HTML?

All HTML elements can have attributes that give added information about an element.

Attributes are placed directly after the name of a tag, inside the two angled brackets. Attributes only appear in opening tags or in self-closing tags. They can not be used within closing tags. Attributes usually come in name/value pairs, like name="value".

##### For example:

HTML links are specified with the < a > tag. The link address is specified in the href attribute:

```js
<a href='https://www.educative.io'>This is a link</a>
```

HTML images also have width and height attributes, which specify the width and height of the image respectively:

```js
 <img src="img.jpg" width="250" height="100">
```

The alt attribute details an alternative text to be used if an image cannot be displayed.

Screen readers can interpret the value of the alt attribute. This allows users, e.g. those with visual impairments, to “listen” to the webpage and hear its value.

```js
<img src="img.jpg" alt="e-learning">
```

---

#### Please name the media element tags introduced by HTML5.

The new media element tags introduced by HTML5 are listed below:

##### < audio >

Used for multimedia like sounds, audio streams, or music, embed audio content without any additional plug-in requirement like the flash player.

##### < video >

Used for video content like video streams or movie clips, embed video content, etc.

##### < source >

Used for multiple media resources in media elements, such as audio, video, picture, etc.

##### < embed >

Used for external applications or embedded content (a plug-in).

##### < track >

Used for adding subtitles or other files containing text in video or audio elements as the respective media play on a web page.

---

#### How many types of headings can an HTML document support?

HTML documents can support 6 levels of headings from level 1 to level 6 .

```js
<h1></h1> to <h6></h6>
```

The following is the general syntax for headings in HTML:

---

#### What does the HTML anchor tag < a > define?

The HTML anchor tag < a > defines a hyperlink that links one page to another page. The href attribute is the most important attribute of the HTML anchor tag that determines the link’s destination. Search engines use the anchor tag to decide the subject matter of the destination URL.

```js
<a href='...........'> Link Text </a>
```

---

#### What are ‘semantic elements’ in HTML5?

Semantic HTML provides meaning to the web page as opposed to just presentation. A < p > tag, for example, indicates that the enclosed text is a paragraph. This is both semantic and presentational as we as humans know what paragraphs are, and the browsers know how to display them.

On the other hand, tags such as < b > and < i > are not semantic markup. They only tell the browser how the text should look (bold or italic), and do not add meaning to the markup. In semantic HTML, these are replaced by < strong > for strong text and < em > for emphasized text respectively.

---

#### Some common types of lists in HTML5 that are used when designing a page.?

The most commonly used list tags in HTML5 are given below:

- ##### Definition list: Offers a list within it and takes a definition term and a detailed definition

  ```js
  <dt> </dt>
  ```

  ```js
  <dd> </dd>
  ```

- ##### Ordered list: Provides the user the required list in a numbered or alphabetical format.

  ```js
  <ol> </ol>
  ```

- ##### Unordered list: Offers the user the required list in a bullet format.

  ```js
  <ul>...</ul>
  ```

---

#### The minimum number of HTML5 tags that are required to create a web page.

A minimum of three HTML5 tags are therefore intuitively required to create a web page, namely

```js
<head> </head>
```

```js
<body> </body>
```

```js
<html> </html>
```

---

#### How would you define the purpose of style sheets?

Style sheets allow the building of transportable well-defined, and consistent style templates. These templates can be linked to several web pages, making it easy to maintain and change all the web pages’ look and feel within the website.

---

#### What are the aspects to consider when developing multilingual sites?

There are several aspects to consider while designing a multilingual site. Basic things include setting the default language, using Unicode encoding, being aware of standard font sizes and text direction, using the ‘lang’ attribute, and being aware of language word length (which may affect layout).

---

#### What is the purpose of <!Doctype html>?

The <!DOCTYPE> declaration is written at the top of every HTML5 page, and it instructs the web browser about the version and type of HTML being used in building the web document. This allows the browser to handle and load the web document properly.

In HTML & HTML5, the DOCTYPE declaration is case-insensitive.

Doctype declaration is only needed to enable a standard mode for documents that are written with the HTML5 syntax

There are three types of DOCTYPES, as mentioned below:

- Strict Doctype
- Frameset Doctype
- Transitional Doctype

```js
<!DOCTYPE html>
```

```js
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
"http://www.w3.org/TR/html4/strict.dtd">
```

```js
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
```

```js
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">
```

```js
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```

---

#### List out the page structure elements of HTML5?

```js
<header> - Used to define header for a document or a section
<nav> - Used to define container for navigation links
<section> - Used to define a section insided a document
<article> - Used to tag an independent self-contained article
<aside> - Defines the content separately (just like a sidebar)
<footer> - Used for tagging a footer inside a document or a section
<details> - Used to define any additional details
<summary>- Used to define a heading inside the <details> element
```

---

#### Given a certain website, what are the ways you could optimize its assets and reduce page load time?

As a basic optimization rule, we can decrease the download size of our web page contents and make fewer HTTP requests.

To optimize website assets, we can follow the below techniques:

- File compression
- File concatenation
- Offloading assets
- Re-organizing & Refining code
- Properly naming all assets
- Using CSS Sprites for Images
- Disabling e-tags
- using internal and external style sheets and minimizing inline CSS
- Using a CDN (content delivery network) for media files and hosting
- Hosting our website's assets on differnt domains while also reducing DNS lookups
- Using a domain that is cookie-free to place the assets and splitting them among different domains

---

#### What is an API? List the APIs available in HTML5.?

In HTML5 API (Application Programming Interface) is a means of creating numerous application using pre-constructed components. Developers can incorporate the functionality related to current APIs into their new websites.

The APIs in HTML5 are:

- Media API
- Data Transfer API
- Application Cache API
- User Interaction
- History API
- Constraint Validaton API
- Command API
- Text Track API
- HTML Web Workers
- HTML Drag and Drop
- HTML Application Cache
- HTML Local Storage
- HTML Geolocaton

---

#### What are the different types of storage in HTML5? Explain.?

In HTML5 , data can be stored in two ways: session storage, local storage

##### Session Storage: the data or details from only the users's current browsing session are stored. Once the users clsoes the browser, the storage data gets removed automatically.

##### Local Storage: The data stays safe and does not get cleared automaticallly when the user closes the browser. The data instead needs to be deleted manually to remove it from storage.

---

#### What are server-sent events?

A server-sent event is when a web page automatically receives updates from a server. This functionality used to be available earlier as well, except that is was not automated because the web page would have to check if there were any changes. The updates immediately arrive with server-sent events.

---

#### What is the difference between server-sent events and Web sockets in HTML5?

Websockets connections can provide both ship statistics to the browser and acquire information from the browser. A real-life example of an application that might use Websockets is a chat application.

server-sent events or (SSE) connections can solely push statistics to the browser. Online inventory prices or Twitter's updating timeline or feed are excellent examples of a utility that ought to benefit from SSE

---

#### What is an < iframe >, and what is it used for?

- This tag is used to specify a browsing context that is nested, or, in other words, an inline frame.

- This tag allows outside documents to be inserted in the main HTML with great ease.

- A common example of usage of inline frames is online advertising, where the contents of the iframe can be an ad from a third party.

```js
iframe introduce security risks. When an iframe is added to a page, the website becomes vulnerable to cross-site attacks.
```

---

#### Why are CSS links placed in the < head > < /head > tag ?

- Style sheets are linked in the head section of the HTML markup, allowing the browser to format and render the markup as it goes.

- If you place the style details at the bottom of the document, the browser must restyle and render the whole document from the top.

- First of all it takes longer if a browser needs to wait before it meets the end of a document before the style details can be added, it will probably have to render the page again, making the process slower.

- Secondly, it's going to look unprofessional. This scenario varies from the scripts included as the scripts can block loading until they are completed (meaning you could load them as late as possible)

---

#### List down all the building blocks that constitute HTML5.

- Semantics
- Connectivity and Communication with servers
- Offline Storage
- Multimedia
- 2D/3D graphics and effects
- Performance and intergration
- Device access
- Styling

---

#### How do you serve a page with content in multiple languages?

- This is one of the aspects of internationalization (i18n)
- When an HTTP request is made to a server, the requesting user agent usually sends information about language preferences, such as in the `Accept-Language` header.
- The server can then use this information to return a version of the document in the appropriate language is such an alternative is available.
- The returned HTML document should also declare the `lang` attribute in the `<html>` tag such as `<html lang="en"...</html/>`

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Multilingual Page</title>
  </head>
  <body></body>
</html>

To let a search engine know that the same content is available in different
languages `<link />` tags with the `rel=alternate` and `hreflang="de"`
attributes should be used Eg:
<link href="alternate" hreflang="de" href="http://de.example.com/page.html" />
```

---

#### What kind of things must you be wary of when designing or developing for multilingual sites?

##### Search Engine Optimization:

- Use the `lang` attribute on the `<html>` tag
- Include the locale in the URL (eg: en_US, zh_CN etc)
- Webpages should use below to tell search engines that there is another page at the specified `href` with the same content but for another language/locale

```html
link rel="alternate" hreflang="other_locale" href="url_of_locale"
```

##### Locale vs Language:

- Locale settings control how numbers, dates, and times display for your region
- Languages have different flavors in different countries, so it's important to differentiate languages for the target country

```html
en: en-US (American English), en-GB (British English) zh: zh-CN (Chinese
(Simplified)), zh,TW (Chinese (Traditional))
```

##### Predict locale but don't restrict:

- Servers can determine the locale/language of visitors via a combination of HTTP `Accept-language` headers and IP's.
- With these visitors can automatically select the best locale for the visitor.

##### Consider differences in the length of the text in different languages:

- Some content can be longer when written in another language, So be wary of layout.

##### Language reading direction:

- Languages like English and French are written from left-to-right, top-to-bottom.
- However some languages, such as Hebrew & Arabic, are written from right-to-left. This can affect the layout of your site, and the placement of elements on the page.

##### Do not concatenate translated strings

- The date today + date, it will break in languages with different word order.
- Use a template string with parameters substitution

##### Formatting dates and currencies

- Calendar dates are sometimes presented in different ways.
- Eg: May 31, 2023 in US, 31 May 2023 in Europe

##### Do not put text in images

- Putting text in images (e.g. png, gif, jpg etc.) is not a scalable approach.
- However to support image text translation, there needs to be a separate image created for each language which is not scalable workflow for designers.

---

#### Describe the difference between script, script async and script defer.

- Scripts tags are used to include Javascript on a web page.
- The async and defer attributes are used to change how/when the loading and execution of the script happens

i) **Plain Script tag**: When these are encountered, `HTML parsing is blocked`, `the script is fetched and executed immediately`. HTML parsing resumes after the script is executed.

ii) **async Script tag**: The script will be fetched in parallel to HTML parsing and executed as soon as it is available (before HTML parsing completes), and it will not necessarily be executed in order in which it appears in the HTML document.

- Use async when the script is independent of any other scripts on the page (Ex: analytics)

i) **Plain Script tag**: The script will be fetched in parallel to HTML parsing and executed when the document has been fully parsed, but before firing `DOMContentLoaded`.

- If there are multiple of them, each script is executed in the order they appeared in the HTML document.
- If a script relies on the fully parsed DOM, the `defer` attribute will be useful in ensuring that the HTML is fully parsed before executing.

---

#### What is progressive rendering?

- Technique used to improve the performance of a webpage (perceived load time), to render content for display as quickly as possible.

**Lazy Loading of Images**: Images on the page are not loaded all at once. The image is only loaded when the user scroll.

```js
<img loading='lazy'>
```

- Is a modern way to instruct the browser to defer loading of images that are outside of the screen until the user scroll near them.
- Use JS, to watch the scroll position and load the image when the image is about to come on screen (by comparing the coordinates of the image with the scroll position)

**Prioritizing visible content**

- Include only the minimum CSS/content/scripts necessary for the amount of page that would be rendered in the users browser first to display as quickly as possible,
- You can then use deferred scripts or listen for the `DOMContentLoaded/load` event to load in other resources and content

---

#### Why you would use a srcset attribute in an image tag? Explain the process the browser uses when evaluating the content of this attribute.

- When you want to serve different images to users depending on their device display width.
- Below example tells the browser to display the small, medium or large .jpg depending on client's resolution.
- The first value is the image name and the second line is the width of the image in pixels.
  Ex:

```js
<img src="small.jpg 500w, medium.jpg 1000w, large.jpg 2000w" alt="">
```

- `srcset` solve the problem whereby you want to serve smaller image files to narrow screen devices, as they don't need huge images like desktop displays do

---

#### What is the difference between canvas and svg?

#### Canvas

- uses **immediate mode graphics rendering**. Once a shape is drawn it's not remembered by canvas, if you want to change it, we need to redraw it.
- Better for pixel-based, well suited for video games where the scene changes for frequently.
- Less accessible as it doesn't support screen readers by default.

#### SVG(Scalar Vector Graphics):

- Uses retained mode graphics. SVG elements are part of the DOM. Each drawn shape is remembered as an object. If attributes of an SVG element are changed, the browser automatically rerenders the shape.
- Better for icons, charts & diagrams. These can scale to any size **without losing quality.**

---

#### What are empty elements in HTML?

- Empty elements are those that do not contain and do not require closing tags. They are also known as `void elements`.
- These elements typically have attributes but they do not have any text or child elements within them.

```js
<br>: Line Break
<hr>: Horizontal Rule
<img>: Image
<input>: Input field
<link>: external resource link
<meta> Metadata
```
