---
description: Custom variable scopes to use in your PowerShell Universal apps.
---

# Custom Variable Scopes

## Custom Variable Scopes

Universal Apps expose three custom variable scopes using custom providers. These providers allow you to store your variables in scopes that make sense for a web application. The cache scope is used to store variables that can be used within any endpoint inside an app. The session scope is used to store variables that can be used for a single user's session of the app.

### Cache Scope

Cache scope is used to store a variable that will be available in any endpoint. Cache scope is useful for storing data that may be shown in more than one control or may be time consuming to look up. This could be helpful for querying machine performance counters (e.g. Active Directory, Azure).

Just like any other scope, cache variables are defined with a prefix and a colon separator.

```powershell
$Cache:Computers = Get-ADComputer
```

Once assigned, the `$Cache:Computer` variable is available within any endpoint.

```powershell
New-UDMonitor -Title Computers -Endpoint {
    $Cache:Computers.Length | Out-UDMonitorData
}
```

### Page Scope

Page scope stores variables in per browser tab or window. If a new tab is opened or the current one is closed, the state will be removed.

```powershell
New-UDForm -Content {
    New-UDTextbox -Id 'Name'
} -OnSubmit {
    $Page:Name = $EventData.Name
    Sync-UDElement -Id 'Name'
}

New-UDDynamic -Content {
    New-UDTypography $Page:Name
}
```

### Session Scope

Session scope is used to store a variable per session. A session is established when a user's browser first visit a dashboard. A cookie is stored in the user's browser that dictates that it is part of the session. Sessions have an idle timeout of 25 minutes.

Just like any other scope, cache variables are defined with a prefix and a colon separator.

```powershell
New-UDCheckbox -Label "Show chart" -OnChange {
   $Session:ShowChart = $EventData
}
```

Once assigned, the `$Session:ShowChart` variable is available in app event handlers. Session variables are not available in REST API endpoints or scheduled endpoints.

```powershell
New-UDColumn -Endpoint {
    if ($Session:ShowChart) {
         New-UDChart ...
    }
}
```

Once a session is terminated, the session variables are cleared.

#### Storing Credentials in Session Scope

Session scope is particularly useful for storing user credentials that should not be persisted beyond the user's session. This pattern allows apps to prompt for administrative credentials without storing them permanently, addressing security requirements where credentials must not be saved.

> ℹ️ **Information**
>
> Session variables expire when the user's session ends. This makes them ideal for storing sensitive data like credentials that should only exist during active use.

**Example: Prompting for Administrator Credentials**

This example demonstrates prompting users for credentials once per session and reusing them for privileged operations:

```powershell
# Check if credentials are already stored in the session
if (-not $Session:AdminCredentials) {
    # Prompt user for credentials (only happens once per session)
    $Session:AdminCredentials = Get-Credential -Message "Enter administrator credentials"
}

# Use the stored credentials for privileged operations
New-UDButton -Text 'Check ACL' -OnClick {
    try {
        # Execute command as the credentialed user
        $result = Invoke-Command -Credential $Session:AdminCredentials -ScriptBlock {
            Get-Acl C:\SensitiveFolder
        }
        
        Show-UDToast -Message "ACL retrieved successfully" -BackgroundColor Green
        Set-UDElement -Id 'aclOutput' -Content { 
            $result | Out-String 
        }
    }
    catch {
        Show-UDToast -Message "Failed: $($_.Exception.Message)" -BackgroundColor Red
    }
}

New-UDElement -Tag 'pre' -Id 'aclOutput'
```

**Key Points:**

* `$Session:AdminCredentials` stores credentials for the duration of the user's session only
* `Get-Credential` prompts the user once; subsequent operations reuse the stored credential
* `Invoke-Command -Credential` executes commands as the credentialed user
* Credentials are never persisted to disk or shared between users
* When the user's session ends, the credentials are automatically cleared

This approach is ideal for applications that perform ACL management, file system operations, or other tasks requiring elevated privileges without storing administrator credentials permanently.
