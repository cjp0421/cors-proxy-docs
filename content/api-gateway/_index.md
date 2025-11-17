+++
title = "API Gateway"
weight = 7
+++
<style>
    .lambda-header {
        display: flex;
    }
    .lambda-img {
        align-content: center;
        margin: 15px;
        padding-top: 20px;
    }
    .panel-body p {
        font-size: .85rem;
    }
</style>

<div class="lambda-header">

<div class="lambda-img">

![AWS Lambda](/images/api-gateway.png)
</div>

With your Lambda handler built and tested, the next step is to expose it through API Gateway so your frontend can call it from the browser. We will use the simplest possible setup: a single HTTP API, one route that points to your Lambda, and basic CORS settings so the browser is allowed to make the request.

</div>

{{% panel %}}

💡 **What Is API Gateway?**

API Gateway is a service that gives your Lambda function a real, public HTTPS URL that your frontend can call. When a request comes in, API Gateway:

- Receives the browser’s request

- Passes that request to your Lambda

- Returns the Lambda’s response

- Handles required CORS behavior so the browser doesn’t block the call

In short: API Gateway is a way to make your Lambda reachable from the browser while ensuring the request is allowed under the browser’s CORS rules.
{{% /panel %}}

👉 **Learn more about API Gateway here:**
- AWS: [Amazon API Gateway](https://aws.amazon.com/api-gateway/)
- IBM: [What Is an API Gateway?](https://www.youtube.com/watch?v=hWRRdICvMNs)