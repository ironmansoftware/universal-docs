---
description: Schedule scripts to run in PowerShell Universal.
---

# Schedules

Assign schedules to scripts to define frequency and other parameters for a script, such as run as credentials.

{% hint style="info" %}
Schedules are stored in the `schedules.ps1` configuration file.
{% endhint %}

## Scheduling a Job

To schedule a job, go to the Automation / Schedules page and click the New Schedule button. To schedule a script, go to the script's page and click Schedule.

You can define schedules based on simple selections like Every Minute or Every Hour, or you can define CRON expressions yourself for more configurable schedules. You can also run One Time schedules that run once at a later date.

You can also define under which user the scheduled job runs, as well as which PowerShell version it uses.

### Simple Schedules

Simple schedules are really just helpers for various standard CRON schedules. When you select one, it defines a CRON schedule for your script.

### CRON

CRON schedules use CRON expressions to define schedules. PowerShell Universal takes advantage of Chronos. For examples of valid expressions, [click here](https://github.com/HangfireIO/Cronos).

### One-Time

One-time schedules will run once in the future. You can select the time and day of when they will run.

### Continuous

Continuous schedules run over and over again. You can define a delay between each scheduled job run.

## Parameters

Schedules support setting parameters for scripts. For example, if you have a script that accepts a parameter, you can choose to pass a value to the parameter during the schedule.

```powershell
param($UserName)

$UserName
```

Within the modal for defining the schedule, you can set the parameter value.

When editing schedules from PowerShell, you can define the parameters on the `New-PSUSchedule` cmdlet. This cmdlet accepts a hashtable representing the scripts parameters so that you can pass the values in for your schedule.

```powershell
New-PSUSchedule -Script "MyScript.ps1" -Cron '* * * * *' -Parameters @{ UserName = 'adam' }
```

## Environments

When creating a schedule, you can specify the [environment](../config/environments.md) for your job to run. By default, it will use the default environment. You can define an environment in the UI by using the Environment drop down. You can define an environment using the `-Environment` parameter in `New-PSUSchedule`.

```powershell
New-PSUSchedule -Script "MyScript.ps1" -Cron '* * * * *' -Environment '7.1'
```

## Run As

You can define as which user to run the schedule by using the Run As selector in the UI. The Run As selector contains a list of PSCredential [variables](../platform/variables.md) you have defined. You need to define a PSCredential variable before the Run As selector is visible. By default, scheduled jobs run under the credentials of the user that is running PowerShell Universal.

You can define a Run As user in a script by using the `-Credential` parameter. The value should be the name of the variable that contains your credential.

```powershell
New-PSUSchedule -Script "MyScript.ps1" -Cron '* * * * *' -Credential 'MyUser'
```

## Computer

You can select the computer or computers on which to run the schedule. By default, schedules run on any available computer. If you select All Computers, the schedule runs on all computers connected to the PSU cluster. If you select a specific computer, the schedule runs on only that computer.

```powershell
New-PSUSchedule -Script "MyScript.ps1" -Cron '* * * * *' -Computer 'PSUNODE1'
```

## Conditions

You can define conditions that determine whether a schedule should be run. This is useful if you are using the same repository scripts for multiple environments. Currently, conditions cannot be defined within the admin console. Conditions are passed to the current script and schedule as parameters. The condition scriptblock runs within the integrated environment.

The condition needs to return true or false. Below is an example of a condition where the schedule only runs if there is an environment variable named `Slot` that contains the value `production`.

```powershell
New-PSUSchedule -Script "MyScript.ps1" -Cron '* * * * *' -Condition {
  $ENV:Slot -eq 'production'
}
```

## Pausing Schedules

You can pause a schedule by setting the Paused property. When a schedule is paused, it does not run. This is useful to stop a schedule from running without deleting it.

## Time Out

You can set a time out for scheduled jobs. The time out is the number of minutes before the scheduled job is canceled.

## Random Delay

The Random Delay property causes a schedule to start anywhere between 0 and 60 seconds from the scheduled time. This is useful when running many schedules at the same time. For example, if you had 10 schedules that start at midnight, you may want to set a random delay to limit resource contention on the PowerShell Universal service.

## Available in Branch

In multi-branch environments, it may be necessary to avoid running schedules based on the branch that is loaded in PowerShell Universal. You can use the `-AvailableInBranch`option on `New-PSUSchedule` to avoid having a schedule run when running in a certain branch. This value is also available in the admin console under the schedule settings when git is enabled.&#x20;

<figure><img src="../.gitbook/assets/image (269).png" alt=""><figcaption><p>Available in Branch</p></figcaption></figure>

## API

* [New-PSUSchedule](../cmdlets/New-PSUSchedule.txt)
* [Get-PSUSchedule](../cmdlets/Get-PSUSchedule.txt)
* [Remove-PSUSchedule](../cmdlets/Remove-PSUSchedule.txt)
