+++
title = "3-Upload to Lambda"
weight = 3
+++

Next, upload the ZIP file you built earlier.

1. On your Lambda function page, open the **Code** tab  
![Code Tab]({{ "/images/code-tab.png" | relURL }})

2. Click **Upload from → .zip file**
<div class="medium-image">

![Upload Zip]({{ "/images/upload-zip.png" | relURL }})

</div>

3. Select **function.zip**  
![Select Zip File]({{ "/images/select-zip-file.png" | relURL }})

4. Click **Save**

Lambda will automatically look for your `bootstrap` file and treat it as your main executable. No handler configuration is required.