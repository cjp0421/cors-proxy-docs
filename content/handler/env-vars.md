+++
title = "4-Environment Variables"
weight = 4
+++

## Why the Handler Uses Environment Variables

Your handler needs two pieces of information the browser cannot safely hold:

- your upstream API key  
- the upstream API’s base URL  

These values should **never** be hardcoded into your Go file or exposed in your frontend. 

Environment variables allow you to keep them inside Lambda, where the browser can’t access them.

{{% note %}}
**Note:** <br>
You’ll add the actual API key later when you create your Lambda function in the AWS Console.
{{% /note %}}

## Reading Environment Variables in Go

Go makes this simple using `os.Getenv`:

{{% code file="example/main_example.go" codeLang="go" %}}
apiKey := os.Getenv("API_KEY")
baseURL := os.Getenv("BASE_URL")
{{% /code %}}
👉 To see how this fits in to the whole handler, visit **[Minimal Example]({{< relref "appendix/minimal-example" >}})**.

If either value is missing, your handler should fail early and return a clear JSON error. 

{{% code file="example/main_example.go" codeLang="go" %}}
if apiKey == "" {
	return serverError(fmt.Errorf("missing API key"))
}
if baseURL == "" {
	return serverError(fmt.Errorf("missing BASE_URL"))
}
{{% /code %}}

This avoids confusing, hard-to-debug behavior.

---
### Why This Matters

By keeping secrets in environment variables, you:

- avoid exposing API keys to end users  
- prevent leaking credentials in GitHub  
- support different values per environment (dev, prod, etc.)  
- keep your handler file clean and simple

Your handler now has everything it needs to build secure upstream requests.

<style>
   .panel {
      max-width: 80%;
   }
</style>
{{% panel %}}
👀 **Looking Ahead: Setting Environment Variables in Lambda**

When you create your Lambda function (later in this guide), you will:

1. Configure your lambda to use your **environment variables**
2. Add the key/value pairs:
   - `API_KEY`: *this is where you’ll paste your real API key.*  
   - `BASE_URL`: *this is the base url of the api you are calling.*
3. Save the configuration.
4. Deploy your updated function.
5. Lambda loads these values automatically at runtime.
{{% /panel %}}