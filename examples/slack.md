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

![](../.gitbook/assets/image%20%28200%29.png)

## Send Slack Message on Failed Job

This following example uses [Universal Automation](../automation/about.md). This example requires a [license](../get-started/licensing.md).

This example takes advantage of triggers to send a message to Slack when a job fails within PowerShell Universal. We define two scripts. The first script simply throws and error and is set to fail by using the `-ErrorAction Stop` setting. The second script receives the job that failed and sends a message to the team's Slack channel.

```text
Start-PSUServer -Port 8080 -Configuration {

    Set-PSULicense -Key 'license'

    New-PSUScript -Name 'ScriptFailed' -ScriptBlock {
        $Body = @{
            text = "Job $($Job.Id) failed!!"
        } | ConvertTo-Json

        Invoke-RestMethod -Uri 'https://hooks.slack.com/services/00000000/00000000/000000000000000' -Body $Body -Method POST
    }

    New-PSUScript -Name 'FailingScript' -ScriptBlock {
        throw "NoooooO!"
    } -ErrorAction Stop

    New-PSUTrigger -Name 'ScriptFailed' -TriggerScript 'ScriptFailed.ps1' -EventType 'JobFailed'
} 
```

When the failing script is running, it will report failure in the UI.

![](../.gitbook/assets/image%20%28199%29.png)

Due to the failure, the trigger will execute and send a message to Slack. 

![](../.gitbook/assets/image%20%28201%29.png)



