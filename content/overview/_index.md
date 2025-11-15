+++
title = "Overview"
weight = 1
+++

## What This Guide Covers
Modern frontend applications often rely on public APIs—but many of those APIs do **not** include the correct CORS headers. When the browser blocks these calls, development stops instantly. This guide walks you through a simple, reliable pattern for bypassing CORS restrictions **without** building a full backend or learning complex AWS infrastructure.

This documentation shows you how to create a **minimal Go-based AWS Lambda proxy** using click-ops only (no Terraform, no pipelines). Your Lambda acts as a secure middle layer: it forwards requests from your frontend to the external API, injects your private API key, and returns the data with proper CORS headers. The result is a small, controlled, inexpensive backend—perfect for personal projects, prototypes, and learning environments.

This guide is written specifically for **frontend developers with little or no backend experience.** Each step is deliberately simplified, focusing on the essentials and skipping everything unnecessary. No prior AWS or Go knowledge is required.

---

## What This Guide Does *Not* Cover

This guide is intentionally focused and does not attempt to teach every aspect of AWS, Go, or backend development. To keep the workflow simple and approachable, the following topics are out of scope:

- Full backend frameworks
  No Go Fiber, Gin, Echo, Node/Express, or other server frameworks are used.

- Infrastructure as Code (IaC)
  Tools such as Terraform, AWS CDK, or Serverless Framework are not part of this guide. All steps use click-ops through the AWS Console.

- Advanced AWS architecture
  This guide avoids topics like VPCs, private subnets, custom authorizers, IAM roles beyond the minimum, or multi-Lambda architectures.

- Production-grade security hardening
  We do not cover authentication systems, API Gateway authorizers, WAF setup, or rate-limiting strategies beyond basic AWS throttling.

- CI/CD pipelines
  No GitHub Actions, CodePipeline, or automated deployments are used.

- Deep Go programming concepts
  You do not need to understand interfaces, concurrency, generics, or package structure. We stick to a single, simple handler.

- Frontend frameworks
  The guide shows how to call your proxy from a frontend, but does not teach React, Vite, or JavaScript fundamentals.

This deliberate simplicity ensures that frontend developers with minimal backend experience can successfully create, deploy, and use a secure Lambda proxy—even without prior AWS or Go skills.

## What You Will Learn
- Why CORS errors occur  
- How to create and deploy a Go Lambda using the AWS Console  
- How to store upstream API keys securely using environment variables  
- How to expose the Lambda through API Gateway  
- How to test the proxy from the browser or CLI  
- How to integrate the proxy into your frontend code  
- How the documentation structure works (Hugo + GitHub Pages)

---

## Who This Guide Is For

- Frontend developers blocked by CORS when using public APIs
- Students or early-career devs needing a severless pattern
- Static-site developers (GitHub Pages, Vite, React)
- Anyone wanting a simple, low-maintenance backend solution
