+++
title = "5-Test Lambda"
weight = 5
+++

The example handler does not expect any input.  
This makes testing very easy.

To test:

1. Go to the **Test** tab  
![Test Tab]({{ "/images/test-tab.png" | relURL }})

2. Click **Configure test event**  
![Configure Test Event]({{ "/images/create-test-event.png" | relURL }})

3. Use this minimal JSON:

```json
{}
```

4. Save and click **Test**

You should see a green success banner. Click on the triangle to see:  
![Success Message]({{ "/images/execute-success-show-headers.png" | relURL }})

- StatusCode: `200`
- CORS headers added (i.e. "Access-Control-Allow-Origin": "*")
- A simple JSON message (whatever your example code returns)
- No errors in the log output

This confirms your Go code is running successfully inside Lambda.