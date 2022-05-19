# Schedules

Schedules can be assigned to scripts and allow you to define frequency and other parameters for a script such as run as credentials.

{% hint style="info" %}
Schedules are stored in the `schedules.ps1` configuration file.
{% endhint %}

## Scheduling a Job

To schedule a job, you can do so from the Automation / Schedules page and by clicking the New Schedule button. You can also schedule a script by click the Schedule option from the script's page.

Schedules can be defined based on simple selections like Every Minute or Every Hour or you can define CRON expressions yourself for more configurable schedules. You can also run One Time schedules that run once at a later date.

You can also define which user the scheduled job will run under as well as which PowerShell version to use.

![Create a Schedule](<../.gitbook/assets/image (317) (1) (1).png>)

### Simple Schedules

Simple schedules are really just helpers for various standard CRON schedules. When you select one, it will define a CRON schedule for your script.

![](<../.gitbook/assets/image (143).png>)

### CRON

CRON schedules use CRON expressions to define schedules. You can use a tool like [Crontab guru](https://crontab.guru/) to help define the schedule.

![](<../.gitbook/assets/image (142).png>)

### One Time

One time schedules will run once in the future. You can select the time and day of when they will run.

![](<../.gitbook/assets/image (140).png>)

### Continuous

Continuous schedules will run over and over again. You can define a delay between each scheduled job run.

![](<../.gitbook/assets/image (141).png>)

## Parameters

Schedules support setting parameters for scripts. For example, if you have a script that accepts a parameter, you can choose to pass a value to the parameter during the schedule.

```powershell
param($UserName)

$UserName
```

Within the modal for defining the schedule, you will have the option to set the parameter value.

![](<../.gitbook/assets/image (180).png>)

When editing schedules from PowerShell, you can define the parameters on the `New-PSUSchedule` cmdlet. This cmdlet accepts dynamic parameters so that you can pass the values in for your schedule.

```powershell
New-PSUSchedule -Script "MyScript.ps1" -Cron '* * * * *' -UserName 'adam'
```

## Environments

When creating a schedule, you have the option to specify the [environment ](../config/environments.md)for your job to run. By default, it will use the default environment. You can define an environment in the UI by using the Environment drop down. You can define an environment using the `-Environment` parameter in `New-PSUSchedule`.

```powershell
New-PSUSchedule -Script "MyScript.ps1" -Cron '* * * * *' -Environment '7.1'
```

## Run As

You can define which user to run the schedule as by using the Run As selector in the UI. The Run As selector contains a list of PSCredential [variables](../platform/variables.md) you have defined. You will need to define a PSCredential variable before the Run As selector is visible. By default, scheduled jobs will run under the credentials of the user that is running PowerShell Universal.

You can define a Run As user in a script by using the `-Credential` parameter. The value should be the name of the variable that contains your credential.

```powershell
New-PSUSchedule -Script "MyScript.ps1" -Cron '* * * * *' -Credential 'MyUser'
```

## Conditions

Conditions can be defined that determine whether a schedule should be run. This is useful if you are using the same repository scripts for multiple environments. Currently, conditions cannot be defined within the admin console. Conditions are passed the current script and schedule as parameters. The condition scriptblock is run within the integrated environment.&#x20;

The condition needs to return true or false. Below is an example of a condition where the schedule will only run if there is an environment variable named `Slot` that contains the value `production`.&#x20;

```powershell
New-PSUSchedule -Script "MyScript.ps1" -Cron '* * * * *' -Condition {
  $ENV:Slot -eq 'production'
}
```

## Pausing Schedules

You can pause a schedule by setting the Paused property. When a schedule is paused, it will not run. This is useful to stop a schedule from running but not delete it.&#x20;

## Time Out

You can set a time out for scheduled jobs. The time out is the number of minutes before the scheduled job is canceled.&#x20;

## Random Delay

The Random Delay property causes a schedule to start anywhere between 0 and 60 seconds from the scheduled time. This is useful when running many schedules at the same time. For example, if you had 10 schedules that start at midnight, you may want to set a random delay to limit resource contention on the PowerShell Universal service.&#x20;

## API

* [New-PSUSchedule](../cmdlets/New-PSUSchedule.txt)
* [Get-PSUSchedule](../cmdlets/Get-PSUSchedule.txt)
* [Remove-PSUSchedule](../cmdlets/Remove-PSUSchedule.txt)

