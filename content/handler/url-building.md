+++
title = "5-URL Building"
weight = 5
+++

## Turning the Incoming Request Into an Upstream URL

Once your handler has the API key and base URL from environment variables, the next step is constructing the **full URL** you will call on the upstream API.

This step is intentionally simple in the minimal example, but it's important to understand the pattern so you can customize it later.

---

### Using `BASE_URL` and API Key

Your Lambda function receives the base portion of the upstream API URL from the `BASE_URL` environment variable.  
You then append whatever path and query parameters the upstream API needs.

Example from the minimal handler:

{{% code file="example/main_example.go" codeLang="go" %}}
apiKey := os.Getenv("API_KEY")
baseURL := os.Getenv("BASE_URL")

upstreamURL := fmt.Sprintf("%s/data?apikey=%s", baseURL, apiKey)
{{% /code %}}

👉 To see how this fits in to the whole handler, visit **[Minimal Example]({{< relref "appendix/minimal-example" >}})**.

Here’s what’s happening:

- `BASE_URL` might be something like `https://api.example.com`
- `/data` is the specific endpoint you want to hit
- `apikey=%s` adds your secret key safely on the server side  
- `fmt.Sprintf` stitches it together into a single URL string

---

### Adding Query Parameters From the Frontend

If your frontend needs to send dynamic values—like `?search=moon`—you can pull them from the `event` and include them in the URL:

{{% code file="main.go" codeLang="go" %}}
search := req.QueryStringParameters["search"]
upstreamURL := fmt.Sprintf("%s/data?search=%s&apikey=%s", baseURL, search, apiKey)
{{% /code %}}
👉 View the version of the handler with parameters here: *[cors-proxy-handler with parameters](https://github.com/cjp0421/cors-proxy-handler/blob/main/main.go)*

This pattern keeps your handler flexible while still protecting your API key.

---

### Keep URL Logic Simple

For this tutorial, the goal is not to build a full routing system.  
A good rule of thumb:

- **BASE_URL** holds the root (env var)  
- **Your handler** adds the endpoint + query params  
- **Never** build URLs on the frontend that include your API key  

With this foundation, the next step is making the upstream HTTP request.
