+++
title = "1-Build Lambda Package"
weight = 1
+++

To prepare your Go function for Lambda, you’ll use the provided `build.sh` script.
This script compiles your code for AWS’s Linux runtime and packages it into a ZIP file that Lambda can run.

### 💻 macOS or Linux Users:

{{% code file="terminal" codeLang="bash" %}}
chmod +x build.sh   # first time only
./build.sh
{{% /code %}}

When it finishes, you’ll see two new files:

{{% note %}}
**Note:**<br>
Do not commit the below files to git or upload them to Github. Add both of them to the .gitignore file in your handler repository (if they are not already there). 

👉 See the example respository .gitignore [here](https://github.com/cjp0421/cors-proxy-handler/blob/main/.gitignore).
{{% /note %}}

- **bootstrap** – the compiled Linux binary  
- **function.zip** – the file you’ll upload to Lambda  

{{% warning %}}
### 🚨 Windows Users

The `build.sh` script is written for macOS/Linux and will not run directly in the Windows command prompt. To use it on Windows, run the commands through **WSL (Windows Subsystem for Linux)** or **Git Bash**, both of which support Unix-style shell scripts.

This ensures your Lambda package is built correctly for AWS’s Linux runtime.

{{% /warning %}}