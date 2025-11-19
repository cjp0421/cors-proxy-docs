+++
title = "3-Function Signature"
weight = 3
+++

Your Lambda handler is a normal Go function with a very specific signature.  
API Gateway (using HTTP API payload **v2**) sends your frontend request into this function, and Lambda expects a structured response in return.

{{% code file="example/main_example.go" codeLang="go" %}}
func Handler(
    ctx context.Context,
    event events.APIGatewayV2HTTPRequest,
) (events.APIGatewayV2HTTPResponse, error) {
    // logic here
}
{{% / code %}}

👉 To see how this fits in to the whole handler, visit **[Minimal Example]({{< relref "appendix/minimal-example" >}})**.

### Parameters

#### `ctx context.Context`  
Provided by Lambda. Mostly used for timeouts or cancellation, but required even if you don’t use it.

#### `event events.APIGatewayV2HTTPRequest`  
Represents the incoming HTTP request after API Gateway formats it (using the v2 HTTP API format).  
Common fields you’ll use:

- `QueryStringParameters`
- `Headers`
- `Body`
- `RawPath` / `PathParameters` (if you enable them)

This is the data you use to build the upstream API request.

### Return Values

Your handler must return:

{{% code file="example/main_example.go" codeLang="go" %}}
(events.APIGatewayV2HTTPResponse, error)
{{% /code %}}

#### `APIGatewayV2HTTPResponse`  
This becomes the HTTP response back to the browser.  
You’ll set:

- `StatusCode`
- `Headers` (including your CORS headers)
- `Body` (usually upstream JSON)

#### `error`  
Return an error to indicate an internal failure.  
Most of the time, you’ll handle errors yourself and return JSON so the browser sees a clean message.

### Why This Matters

This signature is the contract between your Go code and AWS.  
Using the correct **v2 request/response types** ensures that HTTP API passes your CORS headers straight through to the browser, and your handler behaves like any standard server endpoint.
