+++
title = "3-Enable CORS"
weight = 3
+++

![Configure CORS](/images/select-cors-to-configure.png)
- In your HTTP API, **click**: 
  - **CORS** (under the **Develop** section in the left sidebar)

- In the top-right of the panel, click **Configure**.
  - This opens a side panel or modal with all the editable fields.

- In the **Allow Origins** box, enter the testing URL you intend to use.
  - e.g. *http://localhost:5173*

- In **Allow Methods**, add:
  - GET
  - OPTIONS

- In **Allow Headers**, add: *Content-Type*

- Leave everything else at the defaults.
![CORS](/images/api-gateway-cors-config.png)

- Click **Save** at the bottom of the configuration panel.

{{% panel %}}
👀 **What You Should See After Saving:**

- Access-Control-Allow-Origin → http://localhost:5173

- Access-Control-Allow-Methods → GET, OPTIONS

- Access-Control-Allow-Headers → Content-Type

- Other fields remain empty/use default values
{{% /panel %}}

👉 Learn more about CORS and AWS API Gateway here: [Configure CORS for HTTP APIs in API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-cors.html)