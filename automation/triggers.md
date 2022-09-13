---
description: Trigger scripts when events happen with PowerShell Universal.
---

# Triggers

{% hint style="info" %}
This feature requires a[ license](../licensing.md).
{% endhint %}

Triggers allow for automation jobs to be started when certain events happen within PowerShell Universal. For example, this allows you to take action when jobs complete, the server starts or dashboards stop. Triggers are useful for assigning global error handling or sending notifications when certain things happen.

![](<../.gitbook/assets/image (170).png>)

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
* User Login
* Use of a Revoked App Token

### User Login

The user login event takes place when a user accesses PowerShell Universal. The script will receive a `$data` parameter with user information. The data structure is shown below.

```powershell
@{
    UserName = 'username'
    RemoteIpAddress = ''
    LocalPort = ''
    RemotePort = ''
}
```

### Use of a Revoked App Token

The app token event takes place when a revoked app token is used. The script will receive a `$data` parameter that contains the contents of the app token as a string.

## Global Triggers

Global triggers will start the assigned script whenever the event type is invoked.

For example, the `Script.ps1` will be run whenever any job is run.

```powershell
New-PSUTrigger -Name 'Trigger' -EventType JobStarted -TriggerScript Script.ps1
```

## Resource Triggers

Resource triggers will start the assigned script when the event takes place on the selected resource.

For example, the `Script.ps1` will be run whenever the `Dashboard` is stopped.

```powershell
New-PSUTrigger -Name 'Trigger' -EventType DashboardStopped -TriggerScript Script.ps1 -Dashboard 'Dashboard'
```

## Event Metadata

Whenever a job is started from a trigger, it will be provided with metadata about object that caused the event to trigger.

Triggers related to jobs will be provided a `$Job` parameter.

```powershell
param($Job)

$Job
```

Triggers related to dashboards will be provided a `$Dashboard` parameter.

```powershell
param($Dashboard)

$Dashboard
```

Triggers related to the server status will not receive a parameter.

## API

* [New-PSUTrigger](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSUTrigger.txt)
* [Remove-PSUTrigger](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Remove-PSUTrigger.txt)
* [Set-PSUTrigger](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Set-PSUTrigger.txt)
* [Get-PSUTrigger](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Get-PSUTrigger.txt)
