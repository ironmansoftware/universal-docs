---
description: Examples of integrating Slack with PowerShell Universal.
---

# Slack

## Send Message to Slack

This example uses [Universal API](../api/about.md).

This example uses a custom Slack webhook to send a message from a Universal API. 

```text
Start-PSUServer -Port 8080 -Configuration {
    New-PSUEndpoint -Url "/slack" -Method POST -Endpoint {

        $Body = @{
            text = "Hello"
        } | ConvertTo-Json

        Invoke-RestMethod -Uri 'https://hooks.slack.com/services/0000000000/00000000/00000000000000000' -Body $Body -Method POST
    }
} 
```

You can invoke this API by calling `Invoke-RestMethod`

```text
Invoke-RestMethod http://localhost:8080/slack -Method POST
```

The following message will show up in Slack.

![](../.gitbook/assets/image%20%28199%29.png)

