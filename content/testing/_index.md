+++
title = "Testing"
weight = 8
+++

## 🧪 Overview
{{% note %}}
No frontend code is needed.
{{% /note %}}

This section shows how to verify your Lambda proxy is working **end-to-end** using only **curl** or **Insomnia**. The [Minimal Example Test](/testing/minimal-test) is appropriate if your setup does not expect parameters. If your setup expects parameters, please review the [Optional Parameterized Test](/testing/optional-params-test). 

These tests ensure:

- API Gateway can invoke your Lambda  
- Your Lambda can reach the upstream API  
- Your API key and base URL are being used correctly  
- CORS headers are returned  

#### References:
- [`curl`](https://curl.se/docs/httpscripting.html)
- [Insomnia](https://developer.konghq.com/insomnia/)