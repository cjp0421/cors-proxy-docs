+++
title = "6-HTTP Request"
weight = 6
+++

## Making the Upstream HTTP Request

Once you’ve built the full upstream URL, the handler’s next job is to make the actual HTTP request.  
For this tutorial, we keep it intentionally simple and use Go’s built-in `http` package.

---

### Using `http.Get`

The minimal example uses `http.Get`, which is perfect for straightforward proxy calls:

{{% code file="example/main_example.go" codeLang="go" %}}
resp, err := http.Get(upstreamURL)
if err != nil {
    return serverError(fmt.Errorf("failed to reach upstream API: %w", err))
}
defer resp.Body.Close()
{{% /code %}}

👉 To see how this fits in to the whole handler, visit **[Minimal Example]({{< relref "appendix/minimal-example" >}})**.

This does exactly what we need:

- Sends a GET request to the `upstreamURL` you constructed  
- Returns an error only if the API couldn’t be reached at all  
- Leaves status codes (200, 404, 500, etc.) up to the upstream API  
- Ensures the response body is closed when you're done with it  