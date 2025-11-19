+++
title = "Appendix"
weight = 10
+++

The appendix provides a few extra resources that support the main guide.

These are **optional**, but useful if you want to explore beyond the minimal setup.

---

## What You’ll Find Here

### **1. [Build Script]({{< relref "build-script" >}}) (Optional)**
A simple `build.sh` you can use to compile your Go handler for ARM64 and produce a ZIP file ready for Lambda upload.  
This is *not* required if you prefer building manually—it just automates the steps.

### **2. [Minimal Example]({{< relref "minimal-example" >}}) (Code)**
A fully self-contained, minimal version of the Lambda handler.  
This mirrors what the guide walks through, with nothing extra added.

---

## More Examples (External Repository)

{{% note %}}
The below repo is not required for following the main guide, but it’s a helpful reference if you want to expand the proxy or view handler tests.
{{% /note %}}

👉 **View the handler repo:**  
https://github.com/cjp0421/cors-proxy-handler

If you want to go a bit deeper, the handler’s GitHub repository includes:

- A **parameterized version** that forwards query params safely  
- **Unit tests** showing how the handler behaves under success/error conditions  
- A clear folder structure for exploring alternative patterns
