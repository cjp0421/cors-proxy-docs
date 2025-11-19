+++
title = "2-Create Lambda Function"
weight = 2
+++

AWS Lambda can run Go code using a **“custom runtime.”** This simply means Lambda looks for a file named **bootstrap** inside your ZIP package and runs it.

To create the function:

1. Open **AWS Console → Lambda**  
![Search for Lambda](/cors-proxy-docs/images/sm-search-for-lambda.png)
<br>
<br>

2. Click **Create a function**  
![Create Lambda](/cors-proxy-docs/images/create-lambda-func.png)
<br>
<br>

3. Choose **Author from scratch**  
![Author from Scratch](/cors-proxy-docs/images/author-lambda-from-scratch.png)
<br>
<br>

4. Set:
   - **Runtime:** *Provide your own bootstrap (Amazon Linux 2023)*
   - **Architecture:** `x86_64`
   - **Function name:** something like `example-handler`  
   ![Runtime and Architecture](/cors-proxy-docs/images/choose-lambda-runtime-arch.png)
   - **Permissions:** create a new role with basic Lambda permissions  
   ![Author from Scratch](/cors-proxy-docs/images/lambda-permissions.png)

5. Click **Create function**
    <div class="large-image">
    
   ![Click Create](/cors-proxy-docs/images/create-func-lambda.png)

    </div>

You now have an empty Lambda function ready for your code.