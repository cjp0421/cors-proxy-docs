+++
title = "3-Upload to Lambda"
weight = 3
+++

Next, upload the ZIP file you built earlier.

1. On your Lambda function page, open the **Code** tab  
![Code Tab](/cors-proxy-docs/images/code-tab.png)

2. Click **Upload from → .zip file**
<div class="medium-image">

![Upload Zip](/cors-proxy-docs/images/upload-zip.png)

</div>

3. Select **function.zip**  
![Select Zip File](/cors-proxy-docs/images/select-zip-file.png)

4. Click **Save**

Lambda will automatically look for your `bootstrap` file and treat it as your main executable. No handler configuration is required.