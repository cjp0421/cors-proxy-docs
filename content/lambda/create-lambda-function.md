+++
title = "2-Create Lambda Function"
weight = 2
+++

AWS Lambda can run Go code using a **“custom runtime.”** This simply means Lambda looks for a file named **bootstrap** inside your ZIP package and runs it.

To create the function:

1. Open **AWS Console → Lambda**  
![Search for Lambda]({{ "/images/sm-search-for-lambda.png" | relURL }})
<br>
<br>

2. Click **Create a function**  
![Create Lambda]({{ "/images/create-lambda-func.png" | relURL }})
<br>
<br>

3. Choose **Author from scratch**  
![Author from Scratch]({{ "/images/author-lambda-from-scratch.png" | relURL }})
<br>
<br>

4. Set:
   - **Runtime:** *Provide your own bootstrap (Amazon Linux 2023)*
   - **Architecture:** `x86_64`
   - **Function name:** something like `example-handler`  
   ![Runtime and Architecture]({{ "/images/choose-lambda-runtime-arch.png" | relURL }})
   - **Permissions:** create a new role with basic Lambda permissions  
   ![Author from Scratch]({{ "/images/lambda-permissions.png" | relURL }})

5. Click **Create function**
    <div class="large-image">
    
   ![Click Create]({{ "/images/create-func-lambda.png" | relURL }})

    </div>

You now have an empty Lambda function ready for your code.