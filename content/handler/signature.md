+++
title = "3-Function Signature"
weight = 3
+++

Your Lambda handler is a normal Go function with a very specific signature.  
API Gateway sends your frontend request into this function, and Lambda expects a structured response in return.

{{% code file="example/main_example.go" codeLang="go" %}}
func Handler(ctx context.Context, event events.APIGatewayProxyRequest) (events.APIGatewayProxyResponse, error) {
    // logic here
}
{{% / code %}}

👉 To see how this fits in to the whole handler, visit **[Minimal Example](/appendix/minimal-example/)**.

### Parameters

#### `ctx context.Context`  
Provided by Lambda. Mostly used for timeouts or cancellation, but required even if you don’t use it.

#### `event events.APIGatewayProxyRequest`  
Represents the incoming HTTP request after API Gateway formats it.  
Common fields you’ll use:

- `QueryStringParameters`
- `Headers`
- `Body`
- `Path`

This is the data you use to build the upstream API request.

### Return Values

Your handler must return:

{{% code file="example/main_example.go" codeLang="go" %}}
(events.APIGatewayProxyResponse, error)
{{% /code %}}

#### `APIGatewayProxyResponse`  
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
As long as you follow it exactly, Lambda knows how to pass requests in and send responses back out with proper CORS.
