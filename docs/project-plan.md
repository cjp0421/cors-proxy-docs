# User Story

**As a** frontend developer who is blocked by CORS when calling a public API,  
**I want** a clear, step-by-step guide for creating a simple Go-based AWS Lambda proxy using click-ops,  
**so that** I can successfully route API requests through my own server, keep my upstream API key secure, and continue building my application without backend complexity.

---

# Acceptance Criteria

### **AC1 — CORS Explanation**
- The documentation clearly explains what CORS is, why it occurs, and why browsers block certain external API calls.
- Includes a simple diagram or mental model of the proxy pattern (frontend → Lambda → public API → response).

### **AC2 — Architecture Overview**
- A high-level diagram or description of the request flow through Lambda and API Gateway is included.
- The explanation assumes no advanced AWS background.
- Mentions that the Lambda acts as a “secure middle layer” where sensitive API keys live.

### **AC3 — Lambda Creation Steps (Click-Ops)**
- Step-by-step instructions walk the user through creating an AWS Lambda function with Go runtime using the AWS Console.
- Only essential settings are required (name, runtime, basic permissions).
- Documentation instructs users to store the upstream API key **only as a Lambda environment variable**, not in frontend code or GitHub Pages.

### **AC4 — Go Handler Explanation**
- The guide explains what the Go handler needs to do conceptually:  
  - receive event  
  - call external API using the stored environment variable  
  - return JSON  
  - include CORS headers
- No deep Go knowledge is required.

### **AC5 — API Gateway Wiring**
- The documentation covers attaching the Lambda to API Gateway.
- User can deploy a stage and retrieve the public endpoint URL.

### **AC6 — Testing the Proxy**
- User can test the proxy using browser, curl, or a simple frontend call.
- Documentation provides expected success responses and troubleshooting steps.

### **AC7 — Hugo Site Structure**
- The final site is built in Hugo with clear navigation.
- Content is organized into logical sections (Overview, CORS, Lambda creation, API Gateway, Testing, Security, etc.).

### **AC8 — Repo Requirements**
- A GitHub repo contains the Hugo project with clean version history.
- `public/` and generated files are properly ignored via `.gitignore`.
- README includes project description and local run instructions.

### **AC9 — Security & Abuse Prevention**
- Documentation includes a dedicated section describing security considerations:  
  - The Lambda endpoint will be technically public if called from a browser.  
  - Sensitive upstream API keys must remain in Lambda environment variables.  
  - Basic protection patterns are explained (API Gateway throttling, budgets/alerts, optional concurrency limits).  
  - Notes that this pattern is safe for personal projects, demos, and small apps, but production systems require more robust authentication.  
- User understands the limitations and trade-offs of public, browser-callable proxy endpoints.

---
## Product Overview

**Goal:**  
Create a Hugo-based documentation site explaining how to resolve CORS issues by building a simple Go handler deployed as an AWS Lambda using click-ops. The guide teaches the core concepts of proxying requests, securely storing upstream API keys inside Lambda, wiring API Gateway, and safely exposing a minimal endpoint for frontend use.

**Intended Audience:**  
Frontend developers without backend experience who need a fast, secure, lightweight way to bypass CORS restrictions when consuming public APIs. The project is intentionally scoped small so it can be understood quickly and used as a reference pattern.

**Outcome:**  
A small but complete documentation artifact demonstrating skill in:

- Technical writing  
- Instructional design  
- Clear explanation of cloud concepts  
- Go and AWS Lambda architecture  
- Secure handling of API keys in serverless environments  
- Hugo and docs-as-code workflows  
- Git-based version-controlled content  
- Product thinking based on real developer pain points  
- Awareness of abuse prevention and safe public endpoint practices

This creates a portfolio-ready example aligned with roles in documentation, eLearning, SaaS onboarding, developer education, or technical enablement—while demonstrating your ability to think about security and user experience holistically.
