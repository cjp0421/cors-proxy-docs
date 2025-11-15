---
date: 2017-10-19T15:26:15Z
lastmod: 2019-10-26T15:26:15Z
publishdate: 2018-11-23T15:26:15Z

title: Home title
description: Text about this post
images:
- images/pexels-photo-196666.jpeg
---

# What Problem This Guide Solves

Many public APIs do not return the CORS headers required by modern browsers. When this happens, your frontend code fails—even though the API itself works perfectly. This leaves frontend developers blocked with errors they cannot fix, because CORS policies are enforced by the browser, not your code.

This guide provides a simple solution: creating your own small, secure serverless proxy that forwards requests to the external API, adds the required CORS headers, and keeps your private API key hidden from the browser. The result is a reliable way to continue building your frontend without depending on the upstream API’s CORS configuration.

## When This Pattern Is Useful

This pattern is ideal for situations where:

You are building a frontend-only project (React, Vite, static site, GitHub Pages).

You need to call a public API that does not allow browser requests.

You want to keep your API key secret and out of client-side code.

You do not want to manage a full backend server.

You need a low-cost, low-maintenance solution suitable for demos, prototypes, or personal projects.

You want a repeatable, minimal pattern for using AWS Lambda without diving into complex cloud concepts.

It’s especially helpful for students, junior developers, or anyone who needs a quick, secure workaround without building an entire system around it.

## High-Level Summary of Steps

Here’s what you will do in this guide, at a glance:

Understand the CORS problem
Why browsers block certain API calls, and how a proxy solves it.

Create a simple Go Lambda function (click-ops only)
No frameworks, no deep Go knowledge—just a minimal handler.

Store your external API key securely
Using Lambda environment variables, never in frontend code or GitHub.

Connect the Lambda to API Gateway
This creates a public, browser-callable HTTPS endpoint.

Add CORS headers in the Lambda response
So your frontend can successfully make requests.

Test the proxy
Using curl, your browser, or your frontend app.

Swap your frontend’s direct API call with your new endpoint
Your proxy forwards the request, adds the key, returns the result.

Deploy the documentation site using Hugo
So you have a clean, portfolio-ready guide illustrating the entire process.

This flow keeps the complexity low while delivering a fully working CORS-bypass proxy that you can reuse in any frontend project.