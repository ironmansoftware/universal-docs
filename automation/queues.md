---
description: Custom job queues for scripts.
---

# Queues

You can assign computers to queues by using application settings. By default, every computer is assigned to the default queue and a queue specific to the computer itself. When you assign a computer to a custom queue, that queue will be available in the admin console and you can use the queue for ad-hoc script execution and schedules.&#x20;

{% hint style="warning" %}
Queues with no active computers will queue jobs indefinitely.&#x20;
{% endhint %}

## Configure a Queue

To a configure a computer to a specific queue, use the UniversalAutomation \ Queues setting.&#x20;

### appsettings.json

Assign a machine to a queue using an appsettings.json file.&#x20;

```powershell
"UniversalAutomation": {
    "Queues": ["windows7"],
}
```

### Environment Variable&#x20;

Assign a machine to a queue using an environment variable.&#x20;

```powershell
$ENV:UniversalAutomation__Queues = "windows7"
```
