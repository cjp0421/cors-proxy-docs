+++
title = "Minimal Example Test"
weight = 1
+++
## 🧪 Test the Minimal Proxy (No Parameters)

This test verifies the simplest version of your proxy:  
A Lambda that calls an upstream API using:

- a **base URL**, and  
- an **API token** stored as an environment variable.

If your route is `/proxy`, run:

**`curl`**
{{% code file="terminal" codeLang="bash" %}}
curl -i "https://abc123.execute-api.us-east-1.amazonaws.com/prod/proxy"
{{% /code %}}

**Insomnia**
1. Create a **GET** request  
2. Paste the same URL  
3. Click **Send**

### What You Should See

{{% code file="" codeLang="http" %}}
HTTP/1.1 200 OK
Content-Type: application/json
Access-Control-Allow-Origin: *
Access-Control-Allow-Methods: GET,OPTIONS

{
  "result": { ... upstream API JSON ... },
  "source": "upstream",
  "requestId": "example-id"
}
{{% /code %}}

This confirms:

- Your Lambda executed  
- Your Lambda **successfully used the API key and base URL**  
- CORS headers are present  
- The upstream API returned valid data  

---

### Common Errors in the Minimum Test

| Response | Meaning | Fix |
|---------|---------|-----|
| `401 Unauthorized` | API key is missing or incorrect | Check Lambda env variable |
| `403 Forbidden` | Wrong endpoint or blocked key | Confirm upstream API docs |
| `500` | Bug in Lambda code | Check CloudWatch logs |
| `502 Bad Gateway` | Upstream API error | Inspect error body |

---

### When You’re Ready to Move On

Your Lambda proxy is fully functional and ready for frontend integration if:

- The minimal proxy test returns valid upstream data  
- CORS headers appear  
- Optional parameterized requests work  

---

{{% panel %}}
💡 **What Your `curl` Request Actually Calls**

When you run:

``curl -i "https://abc123.execute-api.us-east-1.amazonaws.com/prod/proxy?city=London"``


You are calling:
🔁 **curl → your proxy → upstream API → back through proxy → curl output**

- API Gateway

  - which invokes → your Lambda

     - which calls → the upstream API using:

        - the base URL you configured

           - the API key stored in Lambda env vars

              - any parameters you pass (e.g., city=London)

Your curl request **NEVER** talks directly to the external API.
{{% /panel %}}