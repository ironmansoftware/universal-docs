---
description: Monitoring PowerShell Universal with Application Insights.
---

# Monitoring

PowerShell Universal automatically integrates with Microsoft Application Insights to provide monitoring and alerting for your system.

## Configuring Application Insights

Within the Azure Portal, you will need to create a new Application Insights resource. Once it's been created, you will need to copy the instrumentation key.

![Application Insights Information](../.gitbook/assets/image%20%28195%29.png)

Next, paste your instrumentation key into the [Settings file ](../config/settings.md)for PowerShell Universal. Finally, restart the PowerShell Universal server. Application monitoring will now be enabled.

```text
  "ApplicationInsights": {
    "InstrumentationKey": "73b84b67-6fc9-4c37-9f54-000000000000"
  },
```

## Viewing Monitoring Data

Within the Azure Portal, you can view the Application Insights resource to view information about your PowerShell Universal server. This will include data such as failed responses, server response time, server requests and availability. You'll also be able to setup alerts to monitor for particular conditions of the PowerShell Universal server.

