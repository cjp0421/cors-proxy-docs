+++
title = "Handler"
weight = 4
+++

The handler is the core of this entire proxy pattern. It’s the one piece of Go code that actually runs inside AWS Lambda and performs the work your frontend can’t do on its own. In this pattern, the handler is the “bridge” between your browser request and the upstream API.

👉 If you want the fastest path, start with **[Project Structure](/handler/project-structure/)** (to set up your project files), then jump to **[Minimal Example](/appendix/minimal-example/)** (a complete, working handler you can copy and paste).

🧠 If you want to go deeper, explore the **line-by-line breakdown** in the individual pages:

- imports  
- function signature  
- environment variables  
- building the upstream request  
- reading the response  
- returning the final JSON  
- handling errors  
- testing locally

<style>
 .panel-body li, .panel-body p {
      font-size: .85rem;
   }
   .panel {
      max-width: 80%;
   }
</style>

{{% panel %}}

##### 🚥 Data Flow Through Handler

🔁 *event → Go handler → public API → CORS-safe response*

1. Receive a request from API Gateway  
   *This is the browser request coming through your public Lambda URL.*

   <br>
2. Call the upstream API  
   *This is where you talk to the real API you want data from. The handler can safely include your API key because it runs on the server, not in the browser.*

   <br>
3. Return the upstream JSON  
   *Whatever the upstream API returns, your handler forwards back to your frontend.*

   <br>
4. Include CORS headers  
   *These headers tell the browser “yes, you’re allowed to read this response,” which solves the CORS problem entirely.*

   <br>
5. Handle errors cleanly  
   *If something goes wrong (e.g. missing query parameters, missing API key, upstream API failure) the handler should return a clear JSON error instead of crashing.*

{{% /panel %}}
