+++
title = "9-Error Handling"
weight = 9
+++

## Returning Clear Errors (and Why It Matters)

A proxy should return clear, consistent JSON errors that prevent raw Go errors or crashes. Every error response **also** needs CORS headers so the browser can actually read it.

The minimal example includes two small helpers to make this simple:

{{% code file="example/main_example.go" codeLang="go" %}}
func clientError(msg string) (events.APIGatewayProxyResponse, error) {
    return events.APIGatewayProxyResponse{
        StatusCode: 400,
        Body:       fmt.Sprintf(`{"error": "%s"}`, msg),
        Headers:    corsHeaders(),
    }, nil
}

func serverError(err error) (events.APIGatewayProxyResponse, error) {
    return events.APIGatewayProxyResponse{
        StatusCode: 500,
        Body:       fmt.Sprintf(`{"error": "%s"}`, err.Error()),
        Headers:    corsHeaders(),
    }, nil
}
{{% / code %}}
👉 To see how this fits in to the whole handler, visit **[Minimal Example]({{< relref "appendix/minimal-example" >}})**.

---

### Do You Need `clientError`?

The minimal example doesn’t call `clientError`, but it is included template because:

- It shows how to return a **400-level** error when the *caller* makes a mistake  
  (e.g., missing query parameters, invalid input)
- It gives users a simple pattern to expand on later as needed

In the minimal version, all current failures are internal (missing env vars, network failures), so only `serverError` is used. **Therefore, if you are not using query parameters or user input, you do not need to include ```clientError()``` in your handler.**

---

### What the Handler Actually Uses

Inside the handler, internal failures are routed through `serverError`:

{{% code file="example/main_example.go" codeLang="go" %}}
if apiKey == "" {
    return serverError(fmt.Errorf("missing API key"))
}
if baseURL == "" {
    return serverError(fmt.Errorf("missing BASE_URL"))
}
{{% / code %}}
👉 To see how this fits in to the whole handler, visit **[Minimal Example]({{< relref "appendix/minimal-example" >}})**.

This ensures all internal errors:

- return JSON  
- include CORS headers  
- forward a clear message to the frontend

That’s all the error handling the minimal proxy needs.
