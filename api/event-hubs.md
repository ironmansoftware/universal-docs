---
description: Receive client events from the PowerShell Universal server.
---

# Event Hubs

Event Hubs provide the ability to connect client to the PowerShell Universal server. Once connected, the PowerShell Universal server can send messages to the connected clients and they will run a local PowerShell script block.&#x20;

## Creating an Event Hub

To create an event hub, click APIs \ Event Hub and click Create New Event Hub. Event Hubs are named and can choose to enforce authentication and authorization.

## Connecting an Event Hub

Once created, clients can connect to an event hub using the `Connect-PSUEventHub` cmdlet found in the Universal module. The cmdlet connects to the hub using a web socket and provides credentials, if necessary. When connecting, specify the `-ScriptBlock` parameter to define what will happen on the client when an event is received.&#x20;

```powershell
Connect-PSUEventHub -ComputerName http://localhost:5000 -Hub 'MyHub' -ScriptBlock {
     Write-Host "Event Received"
}
```

Objects sent from the hub will be available as `$_` or $`PSItem`.&#x20;

```powershell
Connect-PSUEventHub -ComputerName http://localhost:5000 -Hub 'MyHub' -ScriptBlock {
     Write-Host $_
}
```

## Send Events

From within the PowerShell Universal server, you can send events from a hub to connected clients using the `Send-PSUEvent` cmdlet.&#x20;

```powershell
Send-PSUEvent -Hub 'MyHub' -Data "Hello!"
```

The `-Data` parameter accepts an object and will be serialized using CLIXML and send to the client. The data will be deserialized before passing to the script block.&#x20;

## View Connected Clients

Within the PowerShell Universal server, you can view connected clients by clicking APIs \ Event Hubs and then clicking the Connections tab.&#x20;
