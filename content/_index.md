---
date: 2025-11-14
lastmod: 2025-11-15

title: Home title
description: Text about this post
---

# CORS, Public APIs, and Getting Back to Making Frontend Magic

## What This Guide Covers

Many public APIs do not return the CORS headers required by modern browsers. This leaves frontend developers blocked; CORS policies are enforced by the browser, not your frontend code.

This guide walks through a simple solution: creating a small, secure serverless proxy that forwards requests to the external API, adds the required CORS headers, and keeps your private API key hidden from the browser. The result is a reliable way to continue building your frontend application without depending on the upstream API’s CORS configuration.

### Who This Guide Is For

- Frontend developers blocked by CORS when using public APIs
- Students or early-career devs needing a severless pattern for a toy or portfolio application
- Static-site developers (GitHub Pages, Vite, React)

---

### When to Use This Pattern

- You are building a frontend-only project (React, Vite, static site, GitHub Pages).

- You need to call a public API that does not allow browser requests.

- You want to keep your API key secret and out of client-side code.

- You only need a proxy; it's out of scope to create and manage a full backend server.

- You want a repeatable, minimal pattern for using AWS Lambda without diving into complex cloud concepts.

- You need a low-cost, low-maintenance solution suitable for demos, prototypes, or personal projects.

---


### What You Will Learn
- Why CORS errors occur  
- How to create and deploy a Go Lambda using the AWS Console  
- How to store upstream API keys securely using environment variables  
- How to expose the Lambda through API Gateway  
- How to test the proxy from the browser or CLI  
- How to integrate the proxy into your frontend code  
- How the documentation structure works (Hugo + GitHub Pages)