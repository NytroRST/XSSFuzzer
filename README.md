**XSS Fuzzer**

XSS Fuzzer is a simple application written in plain HTML/JavaScript/CSS which generates XSS payloads based on user-defined vectors using multiple placeholders which are replaced with fuzzing lists.

It offers the possibility to just generate the payloads as plain-text or to execute them inside an iframe. Inside iframes, it is possible to send GET or POST requests from the browser to arbitrary URLs using generated payloads.

**Why?**

XSS Fuzzer is a generic tool that can be useful for multiple purposes, including:

* Finding new XSS vectors, for any browser
* Testing XSS payloads on GET and POST parameters
* Bypassing XSS Auditors in the browser
* Bypassing web application firewalls
* Exploiting HTML whitelist features

**Example**

In order to fuzz, it is required to create placeholders, for example:

* The [TAG] placeholder with fuzzing list: img svg.
* The [EVENT] placeholder with fuzzing list: onerror onload.
* The [ATTR] placeholder with fuzzing list: src value.
* The payloads will use the mentioned placeholders, such as:

```html
<[TAG] [ATTR]=Something [EVENT]=[SAVE_PAYLOAD] />
```

The [SAVE_PAYLOAD] placeholder will be replaced with JavaScript code such as alert(unescape('[PAYLOAD]'));. 

This code is triggered when an XSS payload is successfully executed.

The result for the mentioned fuzzing lists and payload will be the following:

```html
<img src=Something onerror=alert(unescape('%3Cimg%20src%3DSomething%20onerror%3D%5BSAVE_PAYLOAD%5D%20/%3E')); />
<img value=Something onerror=alert(unescape('%3Cimg%20value%3DSomething%20onerror%3D%5BSAVE_PAYLOAD%5D%20/%3E')); />
<img src=Something onload=alert(unescape('%3Cimg%20src%3DSomething%20onload%3D%5BSAVE_PAYLOAD%5D%20/%3E')); />
<img value=Something onload=alert(unescape('%3Cimg%20value%3DSomething%20onload%3D%5BSAVE_PAYLOAD%5D%20/%3E')); />
<svg src=Something onerror=alert(unescape('%3Csvg%20src%3DSomething%20onerror%3D%5BSAVE_PAYLOAD%5D%20/%3E')); />
<svg value=Something onerror=alert(unescape('%3Csvg%20value%3DSomething%20onerror%3D%5BSAVE_PAYLOAD%5D%20/%3E')); />
<svg src=Something onload=alert(unescape('%3Csvg%20src%3DSomething%20onload%3D%5BSAVE_PAYLOAD%5D%20/%3E')); />
<svg value=Something onload=alert(unescape('%3Csvg%20value%3DSomething%20onload%3D%5BSAVE_PAYLOAD%5D%20/%3E')); />
```

When it is executed in a browser such as Mozilla Firefox, it will alert the executed payloads:

```html
<svg src=Something onload=[SAVE_PAYLOAD] />
<svg value=Something onload=[SAVE_PAYLOAD] />
<img src=Something onerror=[SAVE_PAYLOAD] />
```

**Sending requests**

It is possible to use a page vulnerable to XSS for different tests, such as bypasses for the browser XSS Auditor. The page can receive a GET or POST parameter called payload and will just display its unescaped value.

**Website**

A live version can be found at https://xssfuzzer.com 

**Contact**

The application is in beta state so it might have bugs. If you would like to report a bug or provide a suggestion, you can use the GitHub repository or you can send me an email to contact [a] xssfuzzer.com.
