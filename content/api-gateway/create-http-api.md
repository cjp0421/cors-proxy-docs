+++
title = "1-Create HTTP API"
weight = 1
+++

- Open API Gateway → Create API.  
![Create API](/cors-proxy-docs/images/create-api.png)

- Select HTTP API (not REST).  
![HTTP API](/cors-proxy-docs/images/http-api.png)

- Click **Build**.

- Name it (e.g., cors-proxy-api).  
![Name API](/cors-proxy-docs/images/name-api.png)

- Choose Lambda as the integration and select your Go function.  
![API Integrations](/cors-proxy-docs/images/api-integrations.png)

- Keep all defaults (auto-deploy + default stage).

- Click **Create**.