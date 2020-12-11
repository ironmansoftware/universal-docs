---
description: Examples integrating with PowerShell Protect.
---

# PowerShell Protect

{% hint style="info" %}
[More information about PowerShell Protect can be found on our website. ](https://store.ironmansoftware.com/powershell-protect/)
{% endhint %}

## Display Log Messages in PowerShell Universal <a id="display-log-messages-in-powershell-universal"></a>

This example configures PowerShell Protect to send log messages to a PowerShell Universal instance. It sends HTTP POST requests to the configured server.

### PowerShell Protect Configuration <a id="powershell-protect-configuration"></a>

This configuration checks to see if the user has included the string `\\corp\human-resources` anywhere in their script. If they do, it sends an HTTP POST to the URL `http://localhost:8080/protect`

The body of the HTTP request will contain the computer name and user name separated by a comma.

```text
Start-PSUServer -Port 8080 -Configuration {
    New-PSUEndpoint -Url "/protect" -Method POST -Endpoint {
        $Data = "$Env:Temp\data.csv"
        if (-not (Test-Path $Data))
        {
            "computer,user" | Out-File $Data
        }
        $Body | Out-File $Data
    }

    New-PSUDashboard -Name "Protect" -Content {
        New-UDDashboard -Title 'Protect' -Content {
            $Data = Import-Csv -Path "$Env:Temp\data.csv"
            New-UDTable -Data $Data
        }
    }
}
```

### PowerShell Universal Configuration <a id="powershell-universal-configuration"></a>

This PSU configuration defines an endpoint to accept the POST data from PowerShell Protect. It then saves the data to a file. It also defines a dashboard that will read the data and display it in a table. This assumes that you have installed the PowerShell Universal module and server.

```text
Start-PSUServer -Port 8080 -Configuration {    New-PSUEndpoint -Url "/protect" -Method POST -Endpoint {        $Data = "$Env:Temp\data.csv"        if (-not (Test-Path $Data))        {            "computer,user" | Out-File $Data        }        $Body | Out-File $Data    }​    New-PSUDashboard -Name "Protect" -Content {        New-UDDashboard -Title 'Protect' -Content {            $Data = Import-Csv -Path "$Env:Temp\data.csv"            New-UDTable -Data $Data        }    }}
```

Here is an example of the output for the dashboard.![](https://gblobscdn.gitbook.com/assets%2F-MEuLp20fz-Rt56KSsmu%2F-MOEavYKAK53ueHeiHCF%2F-MOEilnbwR9aCdmFg5uc%2Fimage.png?alt=media&token=005e9fcb-1e9c-4bc3-bc46-2cfd5072bf1d)

