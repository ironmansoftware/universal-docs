---
description: Get started with PowerShell Universal
---

# Get Started

You can get up and running with PowerShell Universal by installing the `Universal` PowerShell Module.

```text
Install-Module Universal
Install-PSUServer -AddToPath -LatestVersion
Start-PSUServer -Port 8080 -Configuration {
    New-PSUEndpoint -Url '/hello' -Method GET -Endpoint {
        'Hello'
    }
    New-PSUDashboard -Name 'Dashboard' -BaseUrl '/dashboard' -Framework 'UniversalDashboard:Latest' -Content {
        New-UDDashboard -Title 'Hello, World' -Content {
            New-UDForm -Content {
                New-UDTextbox -Label 'Say Hi' -Id 'textbox'
            } -OnSubmit {
                Show-UDToast -Message $EventData.textbox
            }
        }
    }
}
```

Once your server is up and running, try executing a REST API request.

```text
Invoke-RestMethod http://localhost:8080/hello
```

You can also visit the dashboard.

```text
Start-Process http://localhost:8080/dashboard
```

Enter some text in the form to say hi. 



Visit the admin console to see all the features of PowerShell Universal. You can login with `admin` and any password. 

```text
Start-Process http://localhost:8080/admin
```

Learn more about the various features of PowerShell Universal

* [APIs](api/about.md)
* [Automation](automation/about.md)
* [Dashboards](dashboard/about.md)

