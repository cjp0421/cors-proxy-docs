+++
title = "7-Read Response"
weight = 7
+++

## Reading the Upstream Response Body

After the upstream API responds, the next step is to read its response body. Your handler doesn’t transform the JSON; it reads the bytes and forwards them back to the browser.

---

### Using `io.ReadAll`

The minimal example keeps this as simple as possible:

{{% code file="example/main_example.go" codeLang="go" %}}
bodyBytes, err := io.ReadAll(resp.Body)
if err != nil {
    return serverError(fmt.Errorf("failed to read upstream response: %w", err))
}
{{% / code %}}
👉 To see how this fits in to the whole handler, visit **[Minimal Example](/appendix/minimal-example/)**.

This does exactly what we need:

- Reads the entire response body from the upstream API  
- Returns an internal server error if something goes wrong  
- Leaves the body in `[]byte` form so you can send it back directly  

Since most public APIs return JSON, we don’t unmarshal or restructure anything here.

---

### Why We Keep It Simple

A true proxy is *pass-through*: whatever JSON the upstream API gives you should be returned to the browser unchanged.

This keeps your handler:

- small  
- predictable  
- easy to debug  
- free of unnecessary transformation logic  

Once you have the bytes, the next step is returning them to the browser with proper status codes and CORS headers.
