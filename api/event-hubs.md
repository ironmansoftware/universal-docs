---
description: Receive client events from the PowerShell Universal server.
---

# Event Hubs

{% hint style="info" %}
Event Hubs require a [license](../licensing.md).
{% endhint %}

Event Hubs provide the ability to connect client to the PowerShell Universal server. Once connected, the PowerShell Universal server can send messages to the connected clients and they will run a local PowerShell script block.

## Creating an Event Hub

To create an event hub, click APIs \ Event Hub and click Create New Event Hub. Event Hubs are named and can choose to enforce authentication and authorization.

## Agent

You will need to install and configure the [PowerShell Universal Agent](../config/agent.md) to use Event Hubs.&#x20;

## Send Events

From within the PowerShell Universal server, you can send events from a hub to connected clients using the `Send-PSUEvent` cmdlet.

```powershell
Send-PSUEvent -Hub 'MyHub' -Data "Hello!"
```

The `-Data` parameter accepts an object and will be serialized using CLIXML and send to the client. The data will be deserialized before passing to the script block.

You can also run commands. This does not require defining a script on the event hub client. You can also use the `Invoke-PSUCommand` alias to mimic native PowerShell behavior.

```powershell
Invoke-PSUCommand -Hub "MyHub" -Command "Start-Process" -Parameters @{
    FilePath = "Notepad"
}
```

## Receive Data from Clients

This feature is only available when sending data to an individual client, rather than all clients connected to a hub.

```powershell
$Connection = Get-PSUEventHubConnection | Where-Object UserName -eq 'Admin'
$Result = Send-PSUEvent -Hub 'Hub' -Data 'Say Hello!' -Connectionid $Connection.ConnectionId
Show-UDToast $Result
```

## Example: Running Scripts on Remote Machines

{% hint style="info" %}
This example provides a way to run scripts on remote machines without having to install another instance of PowerShell Universal.
{% endhint %}

This example allows for sending scripts to remote machines and executing them with a generic event hub script.

First, create an event hub in PowerShell Universal. This example does not use authentication.

Next, install the PowerShell Universal Agent on the remote machine. Create a configuration file in `%ProgramData%\PowerShellUniversal\agent.json`.

```json
{
    "Connections": [
        {
            "Url": "http://localhost:5000",
            "Hub": "eventHub",
            "ScriptPath": "script.ps1"
        }
    ]
}
```

Next, create a helper script.ps1 to receive the event hub data and process requests from PSU to invoke scripts. It creates a new temporary PS1 file and uses the `$EventData` passed down from the event hub message with the contents and parameters for the script.

```powershell
$TempFile = (New-TemporaryFile).FullName + ".ps1"
$EventData.Contents | Out-File -FilePath $TempFile
$Parameters = $EventData.Parameters
& $TempFile @Parameters
```

In PowerShell Universal, add a script that you want to run on the remote machine. In this example, it simply starts a process.

```powershell
param($Name)

Start-Process $Name
```

Finally, add another script that sends the event down to the client. This could be from an API or an App as well. Because the script on the agent is generic, it will just run whatever is passed to it.

```powershell
param($TargetComputer, $ProcessName)
 
Send-PSUEvent -Computer $TargetComputer -Data @{
    Contents = Get-Content StartAProcess.ps1 -Raw
    Parameters = @{
        Name = $ProcessName
    }
}
```

From here you could event use the script to schedule jobs to run on the remote machines using the agent.
