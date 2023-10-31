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
<a href="https://www.educative.io">This is a link</a>
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
<a href="..........."> Link Text </a>
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
