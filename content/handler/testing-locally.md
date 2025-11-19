+++
title = "11-Testing Locally"
weight = 11
+++

## What “Testing Locally” Means in This Guide

This tutorial keeps things simple: no SAM, no LocalStack, and no Lambda emulator.  
When we say “test locally,” we mean:

- making sure your handler **builds cleanly**
- confirming your environment variables load correctly
- optionally running small debug checks using `go run`

The full end-to-end test will happen inside the AWS Console using the **Test** button.

---

### 1. Sanity Check: Does It Build?

From the root of your project (where `main.go` and `build.sh` live):

{{% code file="" codeLang="sh" %}}
go build ./...
{{% / code %}}

You should see **no errors**.  
This verifies that your imports, the v2 handler signature, and general Go structure are correct.

You can also run your build script:

{{% code file="" codeLang="sh" %}}
./build.sh
{{% / code %}}

If it completes successfully and produces `function.zip`, your code is ready to upload to Lambda.

---

### 2. Optional: Run with Local Environment Variables

If you want to do simple experiments — such as checking that your environment variables load or printing the constructed upstream URL — you can run your code locally with temporary debugging.

#### Step 1: Set your environment variables  
Run these **in your terminal**, inside your project folder:

{{% code file="" codeLang="sh" %}}
export API_KEY="your-test-key"
export BASE_URL="https://example.com"
{{% / code %}}

These match the variables you will later configure in the Lambda console.

#### Step 2: Add a temporary debug print (optional)

Inside your `handler` function, you might add:

{{% code file="example/main_example.go" codeLang="go" %}}
fmt.Println("Debug upstreamURL:", upstreamURL)
{{% / code %}}

This lets you verify the URL looks correct.

#### Step 3: Run your program

{{% code file="" codeLang="sh" %}}
go run main.go
{{% / code %}}

Because your handler is designed for Lambda, this does **not** simulate a real request — but Go will still execute the file, run your `main()` function, and print any debug output.

It is useful for:

- confirming environment variables load
- checking your string formatting
- verifying nothing panics
- spotting mistakes before uploading to AWS

If you don’t need debug prints, you can skip this step entirely.

---

### 3. If You Want Real Tests

To keep the tutorial focused, we don’t include automated tests here.  
However, the reference repo contains simple examples that call the handler function directly:

👉 **View the tests in the reference repo:** [cors-proxy-handler-tests](https://github.com/cjp0421/cors-proxy-handler/blob/main/main_test.go)

These are optional but useful if you want to expand your proxy or validate more complex behavior.

---

### 4. Full Testing Happens Later

Local checks are only meant to catch basic issues before you upload your code.  
The **real** end-to-end test — where you send an event through Lambda and see the upstream API’s response — will happen later in the section dedicated to **deploying and testing your Lambda function**.

There, you’ll walk through:

- uploading your deployment package  
- setting environment variables in the Lambda console  
- using the built-in **Test** feature to trigger your function  
- confirming the JSON response from your upstream API  

For now, it’s enough to know your handler builds cleanly and your environment variables load correctly. The full deployment steps come next.