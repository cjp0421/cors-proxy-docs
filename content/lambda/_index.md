+++
title = "Lambda"
weight = 6
+++

<style>
    .lambda-header {
        display: flex;
    }
    .lambda-img {
        align-content: center;
        margin: 15px;
        padding-top: 28px;
    }
    .panel-body p {
        font-size: .85rem;
    }
</style>

<div class="lambda-header">

<div class="lambda-img">

![AWS Lambda](/images/lambda.png)
</div>

This section walks you through deploying a minimal Go handler to AWS Lambda using your existing build.sh script. This example does not read query parameters, headers, or request bodies—it always returns the same JSON response. The goal here is to learn the Lambda workflow in its simplest form before adding more advanced logic later.
</div>
You will:

- Build the handler locally using build.sh

- Create a new Lambda function using the custom runtime (bootstrap)

- Upload the generated function.zip deployment package

- Test the handler directly in the Lambda console using a minimal event payload

{{% panel %}}
💡 **What is AWS Lambda?**

AWS Lambda is a service that lets you run small pieces of code **in the cloud** without creating or managing servers. You upload your function, and AWS runs it only when it’s needed—automatically handling servers, scaling, and uptime for you.

Think of it as:

**“I give AWS my code, and it runs it on demand.”**

No servers to configure, no machines to maintain, no background processes. You only pay when your function actually runs.

👉 Learn more about AWS Lambda here: [What is AWS Lambda?](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)

{{% /panel %}}
