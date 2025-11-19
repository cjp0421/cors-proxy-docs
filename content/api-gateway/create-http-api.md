+++
title = "1-Create HTTP API"
weight = 1
+++

- Open API Gateway → Create API.  
![Create API]({{ "/images/create-api.png" | relURL }})

- Select HTTP API (not REST).  
![HTTP API]({{ "/images/http-api.png" | relURL }})

- Click **Build**.

- Name it (e.g., cors-proxy-api).  
![Name API]({{ "/images/name-api.png" | relURL }})

- Choose Lambda as the integration and select your Go function.  
![API Integrations]({{ "/images/api-integrations.png" | relURL }})

- Keep all defaults (auto-deploy + default stage).

- Click **Create**.