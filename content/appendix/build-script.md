+++
title = "Build Script (Code)"
weight = 4.3
+++

This script compiles your Go handler for AWS Lambda’s Linux environment and packages it into the function.zip file that Lambda expects. Run it each time you want to deploy an updated version of your handler.

```
#!/bin/bash

# Exit immediately if any command fails.
# This protects you from uploading a broken binary.
set -e

# Remove any previous build artifacts so we always start clean.
# bootstrap  = compiled Lambda binary
# function.zip = the deployment package uploaded to AWS Lambda
rm -f bootstrap function.zip

echo "▶️ Building Go binary for AWS Lambda..."

# Compile the Go program for the AWS Lambda platform:
#   GOOS=linux   → Lambda runs Linux under the hood
#   GOARCH=amd64 → 64-bit x86 architecture (matches most Lambda runtimes)
#
# The output file *must* be named "bootstrap" for a custom Go runtime.
GOOS=linux GOARCH=amd64 go build -o bootstrap

echo "📦 Creating deployment package..."

# Zip the bootstrap binary — this is what Lambda executes.
# It contains only the 'bootstrap' executable.
zip function.zip bootstrap

echo "✅ Done! Upload function.zip to your Lambda function."

# to use this script to produce a zip file to upload to AWS, in the terminal run:
# chmod +x build.sh
# ./build.sh
```