+++
title = "5-Smoke Test"
weight = 5
+++

- In your HTTP API, click **Stages** (under **Deploy**) and open the stage you created (e.g., *prod*).

- In **Stage Details**, copy the **Invoke URL**.  
  - It will look like: *https://abc123.execute-api.us-east-1.amazonaws.com/prod*
    ![Invoke URL](/images/invoke-url.png)

- To test your proxy endpoint, run the following command in a terminal (replace with your actual URL):

{{% code file="terminal" codeLang="bash" %}}
  curl -i "https://abc123.execute-api.us-east-1.amazonaws.com/prod/proxy"
{{% /code %}}

- Confirm the response shows:
  - **A successful status code** (200, 201, etc.)  
  - **The expected response body** from your upstream API  
  - **CORS headers**, such as: ``Access-Control-Allow-Origin: http://localhost:5173``

If these checks pass, your **API Gateway → Lambda** integration is working.
