---
description: Universal Automation triggers.
---

# Triggers

{% hint style="info" %}
This feature requires an [Automation license](../licensing.md).
{% endhint %}

Triggers allow for automation jobs to be started when certain events happen within PowerShell Universal. For example, this allows you to take action when jobs complete, the server starts or dashboards stop. Triggers are useful for assigning global error handling or sending notifications when certain things happen. 

![](../.gitbook/assets/image%20%28177%29.png)

{% hint style="info" %}
Triggered jobs will not cause additional triggers to start. Triggers are stored in the `triggers.ps1`.
{% endhint %}

## Trigger Events

The following types of events can be assigned a trigger. 

* Job Started
* Job Completed
* Job Requesting Feedback
* Job Failed
* Dashboard Started
* Dashboard Stopped
* Server Started
* Server Stopping

## Global Triggers

Global triggers will start the assigned script whenever the event type is invoked. 

For example, the `Script.ps1` will be run whenever any job is run. 

```text
New-PSUTrigger -Name 'Trigger' -EventType JobStarted -TriggerScript Script.ps1
```

## Resource Triggers

Resource triggers will start the assigned script when the event takes place on the selected resource. 

For example, the `Script.ps1` will be run whenever the `Dashboard` is stopped. 

```text
New-PSUTrigger -Name 'Trigger' -EventType DashboardStopped -TriggerScript Script.ps1 -Dashboard 'Dashboard'
```

## Event Metadata

Whenever a job is started from a trigger, it will be provided with metadata about object that caused the event to trigger. 

Triggers related to jobs will be provided a `$Job` parameter. 

```text
param($Job)

$Job
```

Triggers related to dashboards will be provided a `$Dashboard` parameter. 

```text
param($Dashboard)

$Dashboard
```

Triggers related to the server status will not receive a parameter.

## Related Cmdlets

* [New-PSUTrigger](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Universal/New-PSUTrigger.md)
* [Remove-PSUTrigger](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Universal/Remove-PSUTrigger.md)
* [Set-PSUTrigger](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Universal/Set-PSUTrigger.md)
* [Get-UAScript](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Universal/Get-UAScript.md)
* [Get-PSUDashboard](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Universal/Get-PSUDashboard.md)

