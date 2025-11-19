+++
title = "3-Confirm CORS Setup"
weight = 3
+++

## How This Guide Handles CORS

This guide uses **Lambda-managed CORS headers**, not API Gateway’s built-in CORS feature.

Your handler already returns:

- `Access-Control-Allow-Origin: *`
- `Access-Control-Allow-Methods: GET,OPTIONS`
- `Access-Control-Allow-Headers: Content-Type`

With HTTP APIs, if you also turn on API Gateway CORS, it can interfere with or override the headers coming from your Lambda. That’s exactly what caused the problems you just fixed.

For this tutorial, the safest setup is:

> **Leave CORS disabled in API Gateway and let your Lambda own CORS completely.**

---

## Step 3 – Confirm CORS Is Disabled in API Gateway

![Configure CORS](/cors-proxy-docs/images/select-cors-to-configure.png)

In your HTTP API:

- In the left sidebar, under **Develop**, click **CORS**.
- Check the CORS settings panel:
  - If there is a toggle or banner showing CORS is **disabled**, you’re good — you don’t need to change anything.
  - If CORS is currently **enabled**, turn it **off** or clear the configuration and save.

After saving, you should see that CORS is not configured at the API Gateway level for this HTTP API.

{{% panel %}}
👀 **Why We Leave CORS Disabled Here**

- Your Lambda already sends `Access-Control-Allow-*` headers.
- With API Gateway CORS disabled, those headers pass straight through to curl and the browser.
- This keeps all CORS logic in one place (the handler), which is easier to understand and debug.

If you ever decide to:
- add custom headers from the frontend, or  
- support more methods (POST, PUT, etc.),  

you can either:
- extend the Lambda’s CORS headers, or  
- switch to using API Gateway’s CORS config instead.  

That’s beyond the scope of this “minimal proxy” tutorial, so we keep it simple and let the handler handle CORS.
{{% /panel %}}

👉 For reference, AWS’s docs on HTTP API CORS live here:  
[Configure CORS for HTTP APIs in API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-cors.html)
