+++
title = "8-Return Response"
weight = 8
+++

## Returning the Final Response to the Browser

Once the upstream API call succeeds and you’ve read the response body, the handler’s final job is returning a proper HTTP response back to the browser.  
AWS Lambda requires a specific structure: `APIGatewayV2HTTPResponse` (for HTTP API payload v2).

---

### Using `APIGatewayV2HTTPResponse`

Here’s the pattern from the minimal example:

{{% code file="example/main_example.go" codeLang="go" %}}
return events.APIGatewayV2HTTPResponse{
    StatusCode: resp.StatusCode,
    Body:       string(bodyBytes),
    Headers:    corsHeaders(),
}, nil
{{% / code %}}
👉 To see how this fits into the whole handler, visit **[Minimal Example](/appendix/minimal-example/)**.

This does three important things:

1. **StatusCode**  
   Forwards the upstream API’s status code (200, 404, 500, etc.).  
   Your handler does *not* decide success vs. error — the upstream API does.

2. **Body**  
   Sends the raw JSON from the upstream API directly to the browser.

3. **Headers**  
   Adds the minimal required CORS headers so the browser is allowed to read the response.

---

### Adding CORS Headers

All responses — success or error — must include CORS headers so the browser doesn’t block them.

Your minimal example uses:

{{% code file="example/main_example.go" codeLang="go" %}}
func corsHeaders() map[string]string {
    return map[string]string{
        "Content-Type":                 "application/json",
        "Access-Control-Allow-Origin":  "*",
        "Access-Control-Allow-Methods": "GET,OPTIONS",
        "Access-Control-Allow-Headers": "Content-Type",
    }
}
{{% / code %}}

👉 To see how this fits into the whole handler, visit **[Minimal Example](/appendix/minimal-example/)**.

---

### Why This Matters

A proxy must stay predictable. By returning the upstream API’s status code and body unchanged, yet adding the headers required for the browser, your handler becomes a clean, reliable middle layer.

Next, we’ll look at handling errors intentionally so the frontend receives useful JSON even when things go wrong.
