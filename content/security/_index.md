+++
title = "Security & Abuse Considerations"
weight = 9
+++

This pattern **improves** security compared to calling a public API directly from your frontend, but it does **not** make your app bulletproof.

Think of this Lambda as a **small, reasonably safe middle layer** for personal projects and demos—not a full production security solution.

---

## What This Lambda Protects (and What It Doesn’t)

### What it *does* protect

- **Keeps your upstream API key out of the browser.**  
  The key lives in **Lambda environment variables**, not in your JavaScript bundle, not in GitHub, and not in your HTML.

- **Lets you control what gets sent upstream.**  
  You own the code, so you can:
  - Fix the URL and HTTP method  
  - Strip or validate query parameters  
  - Sanitize headers/body before forwarding

- **Gives you a single choke point.**  
  If something goes wrong, you can:
  - Comment out the `http.Get` call  
  - Return a static error response  
  - Turn off the Lambda integration in API Gateway

This is a big step up from **hard-coding an API key in frontend code**.

---

### What it *does not* protect

Because your frontend calls API Gateway directly, your **Lambda URL is effectively public**:

- Anyone who can see your web app’s network traffic (e.g., via browser dev tools) can discover the API Gateway URL.
- They can then call that URL directly from their own script or tool (curl, Postman, another website).

{{% warning %}}
**You should assume if a user can access your web page, they can figure out your Lambda endpoint and make requests to it.**
{{% /warning %}}

This is why this pattern is best for **low-risk use cases**:

- Personal projects  
- Portfolio demos  
- Learning exercises  
- Small hobby apps with modest traffic

It is *not* the right pattern for handling:

- Payments / billing  
- Sensitive personal data (PII)  
- Anything with strict compliance requirements  

---

### Always Keep Your Secret in Lambda

{{% warning %}}
**The most important rule:**
**Your upstream API key must live only in Lambda environment variables, never in your frontend code.**
{{% /warning %}}

Concretely, that means:

- ✅ Store the key using **Lambda environment variables** in the AWS Console.  
- ✅ Read it in Go with `os.Getenv("API_KEY")`.  
- ❌ Don’t hard-code the key in your Go file.  
- ❌ Don’t commit the key to GitHub.  
- ❌ Don’t add the key to `.env` files used by your frontend build.  

If your upstream API provider supports it, consider tightening the key itself:

- Restrict allowed **domains**, **IP ranges**, or **referrers**.
- Use a key with **limited scopes** or **read-only** permissions.

---

### Limiting Abuse and Cost

Even for small projects, you don’t want your endpoint to be abused or to generate surprise costs.

You can use a few simple AWS features to protect yourself:

#### 1. API Gateway Throttling

API Gateway lets you configure **rate limits**:

- A global limit (e.g., X requests per second)  
- A burst limit (short spikes)

Setting conservative limits helps avoid:

- Accidental infinite loops in your own code  
- Basic abuse (someone hammering the endpoint repeatedly)

You don’t need to learn everything about API Gateway to benefit from this—just know that **throttling exists and is a good safety net**.

---

#### 2. Budget Alerts

Even with throttling, it’s smart to set up a **budget alert** in AWS:

- You choose a low monthly dollar amount (e.g., $5–10).
- If your projected spend crosses that number, AWS emails you.

That way, if something unexpected happens (bug, abuse, misconfiguration), you get an early warning instead of a surprise bill.

---

#### 3. Keeping the Blast Radius Small

Because this is a **minimal** pattern, you can keep the “blast radius” small by design:

- Use this proxy only for **one or two specific endpoints**, not as a general “open proxy.”
- Reject unexpected inputs:
  - Only allow certain query parameters  
  - Return an error for unsupported paths or methods
- Don’t log or store sensitive data from users.

The simpler your handler, the easier it is to reason about what it can and cannot do.

---

### When This Pattern Is “Secure Enough”

This guide assumes a **non-production**, low-risk scenario:

- You’re calling a public API for things like:
  - Space images  
  - Weather data  
  - Movie info  
  - Other non-sensitive content
- You just need:
  - A stable way to bypass CORS  
  - A safe place for your API key  
  - A small backend you actually understand

In that context, this pattern is **a huge improvement** over exposing keys in the frontend, *as long as* you understand that:

- The endpoint can be discovered.  
- You should add basic throttling and a budget alert.  
- It’s meant for demos, learning, and small projects—not for high-security production workloads.

---

### When You’d Need More

If you eventually move toward a more serious app, you’d look at adding:

- **Authentication/authorization** (e.g., Cognito, Auth0, or your own auth layer)  
- **Stronger rate limiting / WAF rules**  
- **Separate environments** (dev, staging, prod)  
- **Infrastructure as Code** (Terraform, CDK, etc.)  

Those topics are beyond the scope of this guide—but this simple proxy is still a good mental foundation for understanding how security layers build up over time.