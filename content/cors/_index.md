+++
title = "CORS"
weight = 2
+++

## Understanding CORS
### CORS Overview  
CORS stands for cross-origin resource sharing, and it is a security mechanism for browsers. CORS enables a server to specify the origins, besides its own, that a browser is allowed to request resources from. An *origin* could be a domain, a protocol, or port. In modern web applications, browsers block *cross-origin requests* (i.e. requests from different origins) unless the server explicitly allows them. 

<style>
  .callout {
    font-size: 0.85rem;
    line-height: 1.6;
    margin-left: 3%;
    max-width: 90%;
  }
</style>

{{% panel %}}
##### 💡 **Example**  

<div class="callout">
   Your app at <strong>http://localhost:5173</strong> tries to fetch data from an external API <strong>https://api.someservice.com</strong>.
</div>
<br>
<div class="callout">
   If that service does not include an Access-Control-Allow-Origin header, the browser will block the request.
</div>

{{% /panel %}}

### Why Browsers Restrict External API Requests

Modern browsers follow a security rule called the Same-Origin Policy, which prevents one website from freely reading data returned by another website. This protects users from malicious sites trying to access information they shouldn’t.

However, developers often need to call APIs hosted on different domains. To support this safely, browsers introduced CORS. Essentially, it is a simple permission system where the API can explicitly say which origins are allowed to read its responses. If the API doesn’t provide that permission, the browser blocks the request.

This is why many public APIs work perfectly in tools like Postman or curl, but fail in the browser: the server hasn’t opted in to cross-origin access.

{{% panel %}}
📘 **What Is a Public API?**

<div class="callout">
A <strong>public API</strong> is an API that is openly accessible over the internet.  
Anyone can make requests to it, usually with just a free API key.
</div>
<br>
<div class="callout">
Public APIs include services like NASA, Pokémon, GitHub, and OpenWeather.  
They’re meant to be used by developers everywhere (as opposed to inside a company network).
</div>
<br>
<div class="callout">
Because they’re open, public APIs usually have rate limits and often do <strong>not</strong> allow
direct requests from the browser. Thus, many public APIs trigger CORS errors.
</div>
{{% /panel %}}


### Why a proxy server solves the issue  

A proxy server works because the Same-Origin Policy only applies inside the browser; servers do not have the same restriction. When your frontend calls your proxy instead of the public API directly, the browser sees the request as same-origin and allows it.

The proxy then makes the external API request on the server side, where no CORS restrictions apply. It receives the data, adds the proper CORS headers, and returns the response to your app.

This pattern avoids browser blocking, keeps your API key off the client, and gives you full control over how the request is handled.

{{% panel %}}
🧠 **Simple Mental Model**
<div class="callout">
Your frontend does <strong>not</strong> call the public API directly. Instead, it sends the request to your own small backend service (the “proxy”).  
</div>
<br>
<div class="callout">
The proxy makes the external API request on the server side, receives the data, and
returns it to your app with the proper CORS headers.
</div>
<br>
<div class="callout">
<strong>Browser → Your Proxy → Public API → Your Proxy → Browser</strong>
</div>
<br>
<div class="callout">
This avoids CORS issues and keeps your API key out of the frontend.
</div>
{{% /panel %}}

#### Check Your Understanding
Test your hacking skills (and understanding of CORS concepts) by completing this lab through PortSwigger's Web Security Academy:
- [CORS Vulnerability With Basic Origin Reflection](https://portswigger.net/web-security/cors/lab-basic-origin-reflection-attack)

#### References
MDN: [Cross-Origin Resource Sharing (CORS)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/CORS)<br>
AWS: [What is CORS?](https://aws.amazon.com/what-is/cross-origin-resource-sharing/)<br>
Postman: [What is CORS?](https://blog.postman.com/what-is-cors/)<br>
Geeks for Geeks: [Cross Origin Resource Sharing (CORS)](https://www.geeksforgeeks.org/websites-apps/cross-origin-resource-sharing-cors/)<br>
