+++
title = "Optional Parameterized Test"
weight = 2
+++

## 🧪 Optional: Test a Parameterized Request
{{% note %}}
This example assumes that you are calling an api that returns data about city's by city name.
{{% /note %}}

If you later expand your proxy to accept query parameters, such as:

```
/proxy?city=London
```

Run:

**`curl`**
{{% code file="terminal" codeLang="bash" %}}
curl -i "https://abc123.execute-api.us-east-1.amazonaws.com/prod/proxy?city=London"
{{% /code %}}

**Insomnia**
- Add a **GET** request  
- Add query parameters in the “Query” tab  
- Send  
- Confirm the data reflects the parameter  

#### Expected Example

{{% code file="terminal" codeLang="json" %}}
{
  "city": "London",
  "temperature": 18.2,
  "units": "C"
}
{{% /code %}}

This confirms your Lambda correctly forwarded the parameter to the upstream API.

---

### Verifying CORS Headers

Check for:

{{% code file="" codeLang="http" %}}
Access-Control-Allow-Origin: *
Access-Control-Allow-Methods: GET,OPTIONS
{{% /code %}}

If these show up in every response, your frontend will not hit CORS issues.

---

### Common Testing Issues & Fixes

| Problem | Likely Cause | Fix |
|--------|--------------|-----|
| **403 Missing Authentication Token** | Wrong path (e.g., forgot `/proxy`) | Double-check the full URL and route in API Gateway |
| **500 Internal Server Error** | Bug in your Lambda | Check CloudWatch logs; log the error from the handler |
| **No CORS headers** | Handler didn’t attach them | Add CORS headers to every response path (success + error) |
| **Timeouts** | Lambda can’t reach upstream API | Verify upstream URL and that the API is reachable |
| **200 OK but empty/odd data** | Upstream API didn’t like your parameters | Try a known-good example from the upstream API docs |