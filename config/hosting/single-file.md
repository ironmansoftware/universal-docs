---
description: Single-file hosting and configuration for PowerShell Universal.
---

# Single-File

{% hint style="danger" %}
Single-file hosting is deprecated and will be removed in the next major version. 
{% endhint %}

## Single File Hosting and Configuration

You can configure and run the PowerShell Universal server from the command line. The `Start-PSUServer` and `Install-PSUServer` cmdlets can be used to install, configure and run a Universal instance in a single file.

### Installing

To install from the command line, use `Install-PSUServer`. By default, it will store the latest version of the PowerShell Universal Server to the `$Env:ProgramData\PowerShellUniversal` folder. You can specify an alternate path and optionally add the older to the `$Env:Path` environment variable .

```text
Install-PSUServer -AddToPath
```

Once the server is installed, you can start it with `Start-PSUServer`.

### Configuration

You can configure PowerShell Universal from the command line using `Start-PSUServer` and the `-Configuration` parameter. You can use the same cmdlets that you would use in the various configuration files but utilize a single file. You should save this file and then execute the PS1 file. Any changes to the file will be auto-reloaded.

```text
Start-PSUServer -Port 8080 -Configuration {
    New-PSUEndpoint -Method GET -Url '/user' -Endpoint { "User1" }
    New-PSUEndpoint -Method POST -Url '/user' -Endpoint { $Body }
    New-PSUPublishedFolder -Path C:\images -RequestPath /images
    New-PSUDashboard  -Name 'Dashboard' -BaseUrl '/' -Framework "UniversalDashboard:Latest" -Content {
       New-UDDashboard -Title 'Test' -Content {
           New-UDTypography -Text 'Hello, world!'
       }
    }  
} -ExecutablePath "$Env:ProgramData\PowerShellUniversal\Universal.Server.exe"
```

### Limitations

Single file hosting has some limitations in terms of scoping. Variables, functions and modules used within the parent scope or the configuration script block scope will not be accessible in the dashboard, endpoint or script content scopes.

```text
$MyVariable = "Nice"

Start-PSUServer -Port 8080 -Configuration {
    # $MyVariable available here
    New-PSUEndpoint -Method GET -Url '/user' -Endpoint { 
        # $MyVariable not available here
    }
    New-PSUDashboard  -Name 'Dashboard' -BaseUrl '/' -Framework "UniversalDashboard:Latest" -Content {
       # $MyVariable not available here
       New-UDDashboard -Title 'Test' -Content {
           New-UDTypography -Text 'Hello, world!'
       }
    }  
}
```

You can work around these limitations by using variables and environments.

```text
$MyVariable = "Nice"

Start-PSUServer -Port 8080 -Configuration {
    New-PSUVariable -Name 'MyVariable' -Value $MyVariable
    # $MyVariable available here
    New-PSUEndpoint -Method GET -Url '/user' -Endpoint { 
        # $MyVariable available here
    }
    New-PSUDashboard  -Name 'Dashboard' -BaseUrl '/' -Framework "UniversalDashboard:Latest" -Content {
       # $MyVariable available here
       New-UDDashboard -Title 'Test' -Content {
           New-UDTypography -Text 'Hello, world!'
       }
    }  
}
```

## Referencing Other Files

The single-file hosting and configuration does not actually require the use of a single file. Rather, it means that you have a single entry point for the hosting and configuration of your PowerShell Universal server. You can reference other files within the `-Configuration` script block parameter.

For example, if you wanted to load endpoints from a nested folder, you could do the following.

```text
Start-PSUServer -Port 8080 -Configuration {
    Get-ChildItem (Join-Path $PSScriptRoot 'endpoints') | ForEach-Object {
        & $_.FullPath
    }
}
```

With this configuration, you can have an `endpoints` folder within the same directory as your root file and they will be loaded automatically when the server starts of the files change.

