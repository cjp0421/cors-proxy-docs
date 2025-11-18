+++
title = "4-Deploy"
weight = 4
+++

Your routes and CORS settings are not live until you deploy them to a stage.

1. In your HTTP API, click **Stages** in the left sidebar (under **Deploy**).  

<div class="dropdown-image">

![Stages](/images/stages.png)

</div>

2. Click **Create**.  
![Create Stage](/images/create-stage.png)

3. In **Stage Details**  
   - In **Stage name**, enter: `prod`
   - **Description** is optional
![Name Stage](/images/name-stage.png)

4. In **Stage Deployment**, toggle on *Enable automatic deployment*. 
   - This ensures the API auto-deploys every time you update routes or CORS.
   ![Enable Auto Deploy](/images/enable-auto-deploy.png)

6. Click **Create**.


{{% panel %}}
💡 **What’s a stage?** 

A stage is a named version of your API configuration (routes, integrations, CORS). With automatic deployment enabled, any changes you make will appear immediately in your `prod` stage.

{{% /panel %}}