---
description: Role based access for dashboards.
---

# Role Based Access

{% hint style="warning" %}
This documentation is for the prelease version of PowerShell Universal. You can download pre-release versions on our [Downloads page](https://ironmansoftware.com/downloads).
{% endhint %}

When dashboard authentication is enabled, you can define the role that a user must be a part of in order to access the dashboard. Roles are configured on the Settings \ Security page or from within the `roles.ps1` configuration file. 

![](../.gitbook/assets/image%20%28138%29.png)

If a user attempts to visit a dashboard that they do not have access to, they will be presented with a Not Authorized page. 

![](../.gitbook/assets/image%20%28139%29.png)

