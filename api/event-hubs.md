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
