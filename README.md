# Cross-Origin Resource Sharing

Modern browsers use a
[same-origin policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy) that will prevent you from making AJAX request from your domain to another. Those of you using external APIs may have seen this error:

```
XMLHttpRequest cannot load https://www.example.com/api. No 'Access-Control-Allow-Origin'
header is present on the requested resource. Origin http://localhost:8080 is therefore
not allowed access.
```

Fear not! This error message is hinting at something called [Cross-Origin Resource Sharing](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS). Many APIs are CORS enabled. You may need to get an API key first, so check the documentation.

But what if the API you want to use is not configured for CORS? No worries! That is exactly what this demo is for. Since we can't access the API with an AJAX call on the client side, we will instead make regular web request from within our own server. This server will act as a proxy, accepting the AJAX request from the client, accessing the external API, then forwarding the response to the client.


Take a look at `lib/server.js` (a simple application using the `express` framework) and `views/index.html`.

* `GET '/'` gives us `index.html`
* The `<script>` in `index.html` makes an AJAX to an external API, but the same-origin policy prevents it
* It makes another AJAX call to `/cors`. This one will work fine, since domain of the request matches the domain of the page we are on
* The server makes a request to the external API, then sends the body of that response along to the client

## Running the Demo

```
npm install
npm start
open http://localhost:8080
```
