+++
title = "5-Smoke Test"
weight = 5
+++
Before testing the full proxy behavior, first make sure **API Gateway can successfully invoke your Lambda**.

- In your HTTP API, open **Stages** (under **Deploy**) and select your stage (e.g., `prod`).
  - It will look like: *https://abc123.execute-api.us-east-1.amazonaws.com/prod*
    ![Invoke URL](/images/invoke-url.png)

- Now test that API Gateway can reach your Lambda by calling your route directly (usually `/proxy`):

{{% code file="terminal" codeLang="bash" %}}
  curl -i "https://abc123.execute-api.us-east-1.amazonaws.com/prod/proxy"
{{% /code %}}

### What you should see

You are **not** checking whether the upstream API works yet.

For this smoke test, you are only checking **whether the Lambda runs at all**.

A correct result will show:

- A **2xx**, **4xx**, or **5xx** response — **any** response from your Lambda code
- A JSON body that clearly comes **from your Lambda**, not API Gateway  
  - (For example: `{"message": "ok"}` or `{"error": "missing required query parameter 'id'"}` depending on your handler logic.)

### What you’re validating here

- API Gateway route exists  
- API Gateway can invoke your Lambda  
- Lambda executes and returns *something*  
- You're hitting your function, not a `404` from API Gateway

Once this smoke test passes, you can move on to testing the **actual proxy call** with parameters and CORS headers.

{{% panel %}}
💨 **Why We Do a Smoke Test**

Before working with real data, it helps to confirm the basics: Can **API Gateway** actually reach your **Lambda**?
This step isolates and checks the wiring, so beginners don’t end up debugging upstream APIs, CORS, or parameters before the function is even running.

A smoke test gives you a clear signal:

- Any response from your Lambda (even an error like `{"error":"missing required query parameter 'id'"}`) means the integration works.

- A `404` from API Gateway means the route isn’t mapped yet.

This quick check builds confidence and ensures you're testing new features on a solid foundation.
{{% /panel %}}