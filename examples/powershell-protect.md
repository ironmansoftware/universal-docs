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

This configuration checks to see if the user is include the string `\\corp\human-resources` anywhere in their script. If they do, it sends an HTTP POST to the URL `http://localhost:8080/protect`

The body of the HTTP request will contain the computer name and user name separated by a comma.

```text
$Condition = New-PSPCondition -Property "script" -Contains -Value "\\corp\human-resources"$Block = New-PSPAction -Http -Address "http://localhost:8080/protect" -Format "{computerName},{userName}" -Name 'Universal'$Rule = New-PSPRule -Action $Block -Condition $Condition -Name "HR Share"$Config = New-PSPConfiguration -Rule $Rule -Action $Block -License "<License><Terms>PD94bWwgdmVyc2lvbj0iMS4wIj8+DQo8TGljZW5zZVRlcm1zIHhtbG5zOnhzaT0iaHR0cDovL3d3dy53My5vcmcvMjAwMS9YTUxTY2hlbWEtaW5zdGFuY2UiIHhtbG5zOnhzZD0iaHR0cDovL3d3dy53My5vcmcvMjAwMS9YTUxTY2hlbWEiPg0KICA8U3RhcnREYXRlPjIwMjAtMTItMTBUMjM6MTc6MzMuNTE1MTY1NVo8L1N0YXJ0RGF0ZT4NCiAgPFVzZXJOYW1lPmFkYW08L1VzZXJOYW1lPg0KICA8UHJvZHVjdE5hbWU+UG93ZXJTaGVsbFByb3RlY3Q8L1Byb2R1Y3ROYW1lPg0KICA8RW5kRGF0ZT4yMDIxLTEyLTEwVDIzOjE3OjMzLjUxNTE2NTVaPC9FbmREYXRlPg0KICA8U2VhdE51bWJlcj4xPC9TZWF0TnVtYmVyPg0KICA8SXNUcmlhbD5mYWxzZTwvSXNUcmlhbD4NCjwvTGljZW5zZVRlcm1zPg==</Terms><Signature>yRfAEsw2tExuT5icqeQiaLiTGA54ckYc1EqpANPhCq7l9mxj4FA6Xw==</Signature></License>"​Set-PSPConfiguration -Configuration $Config -FileSystem
```

### PowerShell Universal Configuration <a id="powershell-universal-configuration"></a>

This PSU configuration defines an endpoint to accept the POST data from PowerShell Protect. It then saves the data to a file. It also defines a dashboard that will read the data and display it in a table. This assumes that you have installed the PowerShell Universal module and server.

```text
Start-PSUServer -Port 8080 -Configuration {    New-PSUEndpoint -Url "/protect" -Method POST -Endpoint {        $Data = "$Env:Temp\data.csv"        if (-not (Test-Path $Data))        {            "computer,user" | Out-File $Data        }        $Body | Out-File $Data    }​    New-PSUDashboard -Name "Protect" -Content {        New-UDDashboard -Title 'Protect' -Content {            $Data = Import-Csv -Path "$Env:Temp\data.csv"            New-UDTable -Data $Data        }    }}
```

Here is an example of the output for the dashboard.![](https://gblobscdn.gitbook.com/assets%2F-MEuLp20fz-Rt56KSsmu%2F-MOEavYKAK53ueHeiHCF%2F-MOEilnbwR9aCdmFg5uc%2Fimage.png?alt=media&token=005e9fcb-1e9c-4bc3-bc46-2cfd5072bf1d)

