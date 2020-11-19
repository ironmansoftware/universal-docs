# Schedules

Schedules can be assigned to scripts and allow you to define frequency and other parameters for a script such as run as credentials. 

{% hint style="info" %}
Schedules are stored in the `schedules.ps1` configuration file.
{% endhint %}

## Scheduling a Job 

To schedule a job, you can do so from the Automation / Schedules page and by clicking the New Schedule button. You can also schedule a script by click the Schedule option from the script's page. 

Schedules can be defined based on simple selections like Every Minute or Every Hour or you can define CRON expressions yourself for more configurable schedules. You can also run One Time schedules that run once at a later date. 

You can also define which user the scheduled job will run under as well as which PowerShell version to use. 

![](../.gitbook/assets/image%20%283%29.png)

### Simple Schedules

Simple schedules are really just helpers for various standard CRON schedules. When you select one, it will define a CRON schedule for your.

![](../.gitbook/assets/image%20%28143%29.png)

### CRON

CRON schedules use CRON expressions to define schedules. You can use a tool like [Crontab guru](https://crontab.guru/) to help define the schedule. 

![](../.gitbook/assets/image%20%28142%29.png)

### One Time

One time schedules will run once in the future. You can select the time and day of when they will run. 

![](../.gitbook/assets/image%20%28140%29.png)

### Continuous

Continuous schedules will run over and over again. You can define a delay between each scheduled job run. 

![](../.gitbook/assets/image%20%28141%29.png)

## Parameters

Schedules support setting parameters for scripts. For example, if you have a script that accepts a parameter, you can choose to pass a value to the parameter during the schedule. 

```text
param($UserName)

$UserName
```

Within the modal for defining the schedule, you will have the option to set the parameter value.

![](../.gitbook/assets/image%20%28180%29.png)

When editing schedules from PowerShell, you can define the parameters on the `New-PSUSchedule` cmdlet. This cmdlet accepts dynamic parameters so that you can pass the values in for your schedule. 

```text
New-PSUSchedule -Script "MyScript.ps1" -Cron '* * * * *' -UserName 'adam'
```

