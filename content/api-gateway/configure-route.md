+++
title = "2-Configure Route"
weight = 2
+++

Once the API is created, you need to add a route that points to your Lambda.

1. In the left sidebar of your HTTP API, click **Routes** (under **Develop**).  
![Create Route](/cors-proxy-docs/images/create-route.png)
2. Click **Create**. This opens the “Create route” panel.  
3. In the **Method** dropdown, choose: ``ANY``
4. In the **Route** field, enter: ``/proxy`` 
5. Scroll down to **Integration target**.  
   - Click **Choose an integration**  
   - Select the Lambda integration you created earlier (it will be listed by name).  
    ![Route Integration](/cors-proxy-docs/images/route-integration-details.png)

6. Keep the Invoke permissions as they default.  
![Invoke Permissions](/cors-proxy-docs/images/route-invoke-permissions.png)

7. Click **Create** to save the route.

After saving, you should see a new row in the Routes table:  
![Final Routes Table](/cors-proxy-docs/images/final-route-screen.png)