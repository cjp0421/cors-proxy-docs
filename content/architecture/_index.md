+++
title = "Architecture"
weight = 4
+++
## Architecture Overview

This guide uses a simple, lightweight architecture designed for frontend developers who need a safe way to call a public API that does **not** provide the correct CORS headers. Instead of calling the public API directly from the browser, your frontend sends the request to **your** AWS endpoint. Behind the scenes, a small Lambda function makes the upstream call on your behalf.

{{% panel %}}

### 🧠 Simple Mental Model

![Architecture Overview](/images/architecture-overview.png)

---

#### Request Flow

**1. Frontend → API Gateway**  
**Label:** `fetch request to your proxy`  
Your frontend calls the API Gateway URL instead of the upstream API.

**2. API Gateway → Lambda**  
**Label:** `invoke Lambda`  
API Gateway forwards the request exactly as-is to your Lambda function.

**3. Lambda → Public API**  
**Label:** `upstream API request (includes your API key)`  
Lambda reads your private API key from an environment variable and sends the request to the upstream API.

---

#### Response Flow

**4. Public API → Lambda**  
**Label:** `JSON response`  
The upstream API returns the raw data to Lambda.

**5. Lambda → API Gateway**  
**Label:** `return JSON + CORS headers`  
Lambda formats the response and adds the CORS headers your browser needs.

**6. API Gateway → Frontend**  
**Label:** `CORS-safe response`  
The browser receives normal JSON without CORS errors.

{{% /panel %}}

### Why This Architecture Works

- The browser only calls **your** URL, so CORS is no longer an issue.  
- Your private API key stays inside **Lambda environment variables**, never in your frontend code or GitHub Pages.  
- AWS handles the routing between components automatically; you only need to supply the Lambda code and configure a single API Gateway route.
