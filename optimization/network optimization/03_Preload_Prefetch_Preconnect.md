```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>PRELOAD PREFETCH PRECONNECT</title>

    <!-- PRELOADING STARTS -->
    <link rel="preload" as="script" href="script2.js" />
    <link rel="preload" as="style" href="style2.css" />
    <!-- PRELOADING ENDS -->

    <!-- PREFETCH START-->
    <link rel="prefetch" href="index3.html" />
    <link rel="prefetch" as="script" href="script3.js" />
    <!-- PREFETCH ENDS -->

    <!-- PRECONNECT START-->
    <link rel="preconnect" href="https://api.my-app.com/" />
    <!-- PRECONNECT ENDS -->

    <!-- USING STYLES -->
    <link rel="stylesheet" href="style1.css" />
    <link rel="stylesheet" href="style2.css" />
  </head>
  <body>
    <a href="index3.html">index3.html</a>
  </body>
  <!-- USING JS -->
  <script src="script1.js"></script>
  <script src="script2.js"></script>
</html>
```

---

<u>**Ex:**</u> By default (without preload, without prefetch, without preconnect), below is how the browser loads

```html
<!-- STYLES -->
<head>
  <link rel="stylesheet" href="style1.css" />
  <link rel="stylesheet" href="style2.css" />
</head>
<body>
  <a href="index3.html">index3.html</a>
</body>
<!-- JS -->
<script src="script1.js"></script>
<script src="script2.js"></script>
```

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/411a15ff-cdc8-4ae0-b4e0-4433907d99de)

---

**preload** - If you want to load some script or css first because of the priority (ex: I want to load script2 before script1)

<u><b>Note:</b></u> If you preload something and don't consume it, then browser hints you a warning on the console

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/45ddee6c-8dda-4d82-aeaa-e0d455559d2b)

```html
<!-- PRELOADING STARTS -->
<link rel="preload" as="script" href="script2.js" />
<link rel="preload" as="style" href="style2.css" />
<!-- PRELOADING ENDS -->
```

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/734c8785-6700-4eca-b83a-fad8509457b1)

---

**prefetch** - If you want to load some html or script before you have actually been into that html file (ex: Loading 2nd html file in main html page itself)

- When user actually been into the 2nd html file it shows like those files/scripts are cached

<u><b>Note:</b></u> Apply prefetch for only those when you are so much sure that this page is going to be opened.

**Ex:** Registering an user requires 3 pages, you can prefetch the 2nd page into 1st page and similarly 3rd page into 2nd page.

```html
<!-- PREFETCH START-->
<link rel="prefetch" href="index3.html" />
<link rel="prefetch" as="script" href="script3.js" />
<!-- PREFETCH ENDS -->
```

##### index3.html is loaded before the user actually navigated to index3.html

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/8539aaaf-333e-4449-b89c-3862ac2dad04)

##### index3.html shows the cache (once index3.html is opened)

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/7221f4ae-a087-4382-8ecf-eb09c6cd56b6)

---

**preconnect**- when you are actually loading some contents from other domain (let's say CDN).

- So when you are making a new connection with a new domain (which usually takes time)

- thereby preconnect helps to make this call beforehand between two different domains

- handshake happens only once per domain, so if the handshake is done already then going forward it no need to do the handshake again

```html
<!-- PRECONNECT START-->
<link rel="preconnect" href="https://api.my-app.com/" />
<!-- PRECONNECT ENDS -->
```

---
