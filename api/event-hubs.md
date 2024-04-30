---
description: Receive client events from the PowerShell Universal server.
---

# Event Hubs

Event Hubs provide the ability to connect client to the PowerShell Universal server. Once connected, the PowerShell Universal server can send messages to the connected clients and they will run a local PowerShell script block.

## Creating an Event Hub

To create an event hub, click APIs \ Event Hub and click Create New Event Hub. Event Hubs are named and can choose to enforce authentication and authorization.

## Connecting an Event Hub

Once created, clients can connect to an event hub using the `Connect-PSUEventHub` cmdlet found in the Universal module. The cmdlet connects to the hub using a web socket and provides credentials, if necessary. When connecting, specify the `-ScriptBlock` parameter to define what will happen on the client when an event is received.

```powershell
Connect-PSUEventHub -ComputerName http://localhost:5000 -Hub 'MyHub' -ScriptBlock {
     Write-Host "Event Received"
}
```

Objects sent from the hub will be available as `$_` or $`PSItem`.

```powershell
Connect-PSUEventHub -ComputerName http://localhost:5000 -Hub 'MyHub' -ScriptBlock {
     Write-Host $_
}
```

## Send Events

From within the PowerShell Universal server, you can send events from a hub to connected clients using the `Send-PSUEvent` cmdlet.

```powershell
Send-PSUEvent -Hub 'MyHub' -Data "Hello!"
```

The `-Data` parameter accepts an object and will be serialized using CLIXML and send to the client. The data will be deserialized before passing to the script block.

## Receive Data from Clients

As of 4.1, you can now receive data back from clients. This feature is only available when sending data to an individual client, rather than all clients connected to a hub.

```powershell
$Connection = Get-PSUEventHubConnection | Where-Object UserName -eq 'Admin'
$Result = Send-PSUEvent -Hub 'Hub' -Data 'Say Hello!' -Connectionid $Connection.ConnectionId
Show-UDToast $Result
```

From the client side, you would return the data from the script block.

```powershell
Connect-PSUEventHub -Hub 'Hub' -ScriptBlock {
    Write-Host $EventData 
    "Hello!"
}
```

## Event Hub Client Installer

While you can use the Universal module to connect to event hubs, it may not be the most resilient configuration for your environment. The Event Hub Client Installer provides a MSI that installs a Windows services that will connect to event hubs and run scripts.

### eventHubClient.json

After installing the MSI, you will need to configure the client by using an `eventHubClient.json` file. This file should be created in `%ProgramData%\PowerShellUniversal`. Changes to this file require a restart of the Event Hub Client service.

{% hint style="warning" %}
The installer will not create the folder or file automatically.&#x20;
{% endhint %}

This JSON file configures the Event Hub Client to connect to the hub and run scripts when invoked.

```json
{
    "Connections": [
        {
            "Url": "http://localhost:5000",
            "Hub": "eventHub",
            "AppToken": "tokenXyz",
            "ScriptPath": "script.ps1"
        }
    ]
}
```

### Options

The below options can be included in the `eventHubClient.json` file.

#### Connections

These are the connections to Event Hubs. Each connection can contain it's own URL, hub, authentication and script to execute.

#### Url

The URL of the PowerShell Universal service.

#### Hub

The name of the Event Hub.

#### AppToken

The app token used to authentication against the hub.

#### UseDefaultCredentials

Windows Authentication will be used to authenticate against the hub.

#### ScriptPath

The script to execute when an event is received. This script is read into memory and not from disk. Variables such as `$PSScriptRoot` are currently not supported.

## Example: Running Scripts on Remote Machines

{% hint style="info" %}
This example provides a way to run scripts on remote machines without having to install another instance of PowerShell Universal.
{% endhint %}

This example allows for sending scripts to remote machines and executing them with a generic event hub script.&#x20;

First, create an event hub in PowerShell Universal.  This example does not use authentication.

Next, install the Event Hub Client on the remote machine. Create a configuration file in `%ProgramData%\PowerShellUniversal\eventHubClient.json`.

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

Next, create a helper script.ps1 to receive the event hub data and process requests from PSU to invoke scripts. It creates a new temporary PS1 file and uses the `$EventData` passed down from the event hub message with the contents and parameters for the script.&#x20;

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

Finally, add another script that sends the event down to the client. This could be from an API or an App as well. It uses `Get-PSUEventHubConnection` to get the target computer’s connection ID and then sends an event with the contents of a script and any parameters for that script. Because the script on event hub side is generic, it will just run whatever is passed to it.

```powershell
param($TargetComputer, $ProcessName)
 
$Connection = Get-PSUEventHubConnection | Where-Object { $_.Computer -eq $TargetComputer -and -not $_.Disconnected } | Select-Object -First 1
Send-PSUEvent -Hub eventHub -ConnectionId $Connection.ConnectionId -Data @{
    Contents = Get-Content StartAProcess.ps1 -Raw
    Parameters = @{
        Name = $ProcessName
    }
}
```

From here you could event use the script to schedule jobs to run on the remote machines using the event hub client.&#x20;

&#x20;
