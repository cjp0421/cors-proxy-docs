+++
title = "10-Main Function"
weight = 10
+++

## Why the Main Function Comes Last

Once your handler is fully built, the last piece of the puzzle is telling AWS Lambda **which function to run** when your Lambda is invoked. That’s the job of `main()`.

Unlike traditional Go programs, your Lambda does not start a server, listen on a port, or run a loop.  
It only needs one line that hands your handler to AWS.

---

### Where the Main Function Belongs

In this tutorial, both the **handler** and the **main function** live in the same file: **main.go**.  
This is the simplest and most common structure for a small Lambda project.

```
/
├─ main.go        ← handler + main function together
├─ build.sh
├─ go.mod
├─ go.sum
```
👉 **View the file structure of the reference repo here:** *[cors-proxy-handler](https://github.com/cjp0421/cors-proxy-handler?tab=readme-ov-file)*

Keeping everything inside `main.go` makes the full request flow easy to follow, and it avoids unnecessary files for such a small proxy.

### The Minimal Main Function

The example handler uses the standard AWS Lambda Go runtime:

{{% code file="example/main_example.go" codeLang="go" %}}
func main() {
    lambda.Start(handler)
}
{{% / code %}}
👉 To see how this fits in to the whole handler, visit **[Minimal Example]({{< relref "appendix/minimal-example" >}})**.

Here’s what this does:

- Registers your `handler` function with the Lambda runtime  
- Tells AWS: “When this Lambda runs, execute *this* function”

---

### Why This Simplicity Matters

Keeping `main()` this minimal means:

- all request/response behavior stays in one place (the handler)  
- your Lambda behaves predictably and is easy to extend later  

🎉 At this point, your handler is complete! 🎉

The final step is running it locally to confirm everything works before deploying it to AWS.