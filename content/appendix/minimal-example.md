+++
title = "Minimal Example (Code)"
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

func handler(ctx context.Context, req events.APIGatewayV2HTTPRequest) (events.APIGatewayV2HTTPResponse, error) {
	apiKey := os.Getenv("API_KEY")
	baseURL := os.Getenv("BASE_URL")

	if apiKey == "" {
		return serverError(fmt.Errorf("missing API key"))
	}
	if baseURL == "" {
		return serverError(fmt.Errorf("missing BASE_URL"))
	}

	upstreamURL := fmt.Sprintf("%s/data?apikey=%s", baseURL, apiKey)

	resp, err := http.Get(upstreamURL)
	if err != nil {
		return serverError(fmt.Errorf("failed to reach upstream API: %w", err))
	}
	defer resp.Body.Close()

	bodyBytes, err := io.ReadAll(resp.Body)
	if err != nil {
		return serverError(fmt.Errorf("failed to read upstream response: %w", err))
	}

	return events.APIGatewayV2HTTPResponse{
		StatusCode: resp.StatusCode,
		Body:       string(bodyBytes),
		Headers:    corsHeaders(),
	}, nil
}

func clientError(msg string) (events.APIGatewayV2HTTPResponse, error) {
	return events.APIGatewayV2HTTPResponse{
		StatusCode: 400,
		Body:       fmt.Sprintf(`{"error": "%s"}`, msg),
		Headers:    corsHeaders(),
	}, nil
}

func serverError(err error) (events.APIGatewayV2HTTPResponse, error) {
	return events.APIGatewayV2HTTPResponse{
		StatusCode: 500,
		Body:       fmt.Sprintf(`{"error": "%s"}`, err.Error()),
		Headers:    corsHeaders(),
	}, nil
}

func corsHeaders() map[string]string {
	return map[string]string{
		"Content-Type":                 "application/json",
		"Access-Control-Allow-Origin":  "*",
		"Access-Control-Allow-Methods": "GET,OPTIONS",
		"Access-Control-Allow-Headers": "Content-Type",
	}
}

func main() {
	lambda.Start(handler)
}
{{% /code %}}