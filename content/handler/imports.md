+++
title = "2-Imports"
weight = 2
+++
{{% code file="example/main_example.go" codeLang="go" %}}
package main

import (
	"context"
	"fmt"
	"io"
	"net/http"
	"os"

	"github.com/aws/aws-lambda-go/events"
	"github.com/aws/aws-lambda-go/lambda"
)

{{% /code %}}
👉 To see how this fits in to the whole handler, visit **[Minimal Example](/appendix/minimal-example/)**.

- context – AWS passes context about the Lambda invocation (timeouts, metadata).

- encoding/json – used to decode/encode JSON.

- fmt – string formatting.

- io – reading the response body.

- net/http – making HTTP requests to your upstream API.

- os – reading environment variables (your API key).

- events – AWS-provided request/response types for API Gateway.

- lambda – AWS package that turns your Go function into a Lambda handler.

