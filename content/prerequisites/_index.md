+++
title = "Prerequisites"
weight = 3
+++

Before we begin, this guide assumes a few simple prerequisites: an AWS account to deploy the proxy, Go installed to build the small handler, and a way to eventually make the HTTP request.


## AWS Account

{{< note >}}
This guide uses click-ops only. No CLI and no Terraform.
{{< /note >}}

You’ll deploy a small Lambda function and expose it through API Gateway. To do this, you’ll need:

- An AWS account with console access  
  - [Create or sign in to your AWS account](https://signin.aws.amazon.com/signup?request_type=register)
  - Permission to create Lambda and API Gateway resources

- (Optional) The ability to set a cost-protection budget alert  
  - [Configure a Budget Action → AWS Docs](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-action-configure.html)

---

## Go Installed

{{< note >}}
No prior Go knowledge required. All Go code in this guide is kept small, commented, and intentional.
{{< /note >}}

You’ll need Go installed so you can compile the tiny Lambda handler.

- A recent Go version  
  - [Install Go](https://go.dev/doc/install)

- Ability to run `go build` in your terminal  
  - [`go build` documentation](https://pkg.go.dev/cmd/go#hdr-Compile_packages_and_dependencies)

---

## Familiarity With API Calls

You should know how to make a basic HTTP request. If you'd like more information about how to do so with or without a frontend application, please see:

**HTTP request from a frontend application:**
- [`fetch()`](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)  
- [Axios](https://axios-http.com/docs/intro)

**HTTP request from a tool or terminal:**
- [`curl`](https://developer.ibm.com/articles/what-is-curl-command/)  
- [Postman](https://www.postman.com/downloads/)  
- [Insomnia](https://insomnia.rest/)
