+++
title = "Overview"
weight = 1
+++

Modern frontend applications often rely on public APIs—but many of those APIs do **not** include the correct CORS headers. When the browser blocks these calls, development stops instantly. 

This documentation shows you how to create a **minimal Go-based AWS Lambda proxy** using click-ops only (no Terraform, no pipelines). Your Lambda acts as a protected middle layer: it forwards requests from your frontend to the external API, injects your private API key, and returns the data with proper CORS headers. The result is a small, controlled, inexpensive backend ideal for personal projects, prototypes, and learning environments.

This guide is written specifically for **frontend developers with little backend knowledge.** Each step is deliberately simplified, focusing on the essentials and skipping everything unnecessary. Minimal prior AWS or Go knowledge is required.

---

### What This Guide Does *Not* Cover

To keep the workflow simple and approachable, the following topics are out of scope:

- Production-grade security hardening - while this is best practice for production applications, **this guide is intended for developers building demonstration, practice, or proof-of-concept applications**.

- Frontend frameworks - although it will cover how to call your proxy from a frontend, it does not teach React, Vite, or JavaScript fundamentals. **A basic understanding of these concepts is assumed**.

- Full backend frameworks - no server frameworks are used.

- Infrastructure as Code (IaC) - all steps use click-ops through the AWS Console.

- Advanced AWS architecture - no VPCs, private subnets, custom authorizers, IAM roles beyond the minimum, or multi-Lambda architectures.

- CI/CD pipelines - no GitHub Actions, CodePipeline, or automated deployments workflows are explained.

- Deep Go programming concepts - no need to understand interfaces, concurrency, generics, or package structure. 


This deliberate simplicity enables frontend developers with minimal backend experience to create and deploy a protected Lambda proxy without prior AWS or Go skills.


### High-Level Summary of Steps

Here’s what you will do in this guide, at a glance:

1. Understand the CORS problem, including why browsers block certain API calls and how a proxy solves it.

2. Create a simple Go Lambda function (click-ops only) with a simple handler.

3. Store your external API key securely using Lambda environment variables.

4. Connect the Lambda to API Gateway to create a public, browser-callable HTTPS endpoint.

5. Add CORS headers in the Lambda response.

6. Test the proxy using curl, your browser, or your frontend app.

7. Swap your frontend’s direct API call with your new endpoint.

This flow keeps the complexity low while delivering a fully working CORS-bypass proxy that you can reuse in any frontend project.