---
description: Receive client events from the PowerShell Universal server.
---

# Event Hubs

{% hint style="info" %}
Event Hubs require a [license](../licensing.md).
{% endhint %}

Event Hubs provide the ability to send PowerShell commands to connected [PowerShell Universal Agents](../config/agent.md) from the PowerShell Universal server. Agents are lightweight, cross-platform services that can run on edge nodes to allow PowerShell Universal to issue commands against them.

Event Hubs work in either a one-to-one communication method from the server to agent or in a fan out one-to-many communication method from an event hub at the server to all connected agents. Agents do not run jobs directly and require the use of `Invoke-PSUCommand` from other scripts running within the PowerShell Universal server. You can think of event hubs as a way to perform PowerShell Remoting without using the standard remoting transport.

## About

PowerShell Universal runs a web server with a websocket endpoint that is will listen for agents to connect to. This is referred to as the event hub. You can configure multiple event hubs per PowerShell Universal server with different names and security settings. Once an event hub is configured at the server, you can install an agent on any machine that can reach the PowerShell Universal via standard HTTP ports.&#x20;

The agent requires some configuration about where and how to connect to the server. Once this has been done, the agent can be started to connect the websocket connection to the server. After the connection is established, the server is then aware of the connected client. It will be registered within the hub and events can then be sent from the server to the agents.&#x20;

While you cannot schedule jobs to run on agents directly, you can run commands against agents, within jobs, APIs and apps within the server.&#x20;

## Basic Example

As an example, you may have a Linux PowerShell Universal agent run within your US Datacenter. The PowerShell Universal server, running in your EU Datacenter, has a configured event hub hub named Linux. On the server, you would configure the hub by using the `eventHubs.ps1` file or within the admin console.

```powershell
New-PSUEventHub -Name 'Linux'
```

On the agent side, you would then configure an `agent.ps1` file to instruct the agent where it should connect to the server.

```json
{
    "Connections": [
        {
            "Url": "http://eu.mycompany.local",
            "Hub": "Linux"
        }
    ]
}
```

With the event hub created and the agent configured, the agent will connect to the server and can now accept commands.&#x20;

Within the server, you can create a script that executes against the agent. While the script itself is not running against the agent, you can use the built-in `Invoke-PSUCommand` cmdlet to do so. Within your script, you could gather host information. Because the `-Computer` parameter is specified, this command will be run against the agent directly and return the host name back to the script executing in the server.

```powershell
Invoke-PSUCommand -Command "hostname" -Computer "linuxhost-12" 
```

Additionally, you can take actions against the entire hub of connected agents. If you wanted to, for example, restart all connected agents, you could span out across the hub.

```powershell
Invoke-PSUCommand -Command "reboot" -Hub "Linux"
```

## Creating an Event Hub

To create an event hub, click APIs \ Event Hub and click Create New Event Hub. Event Hubs are named and can choose to enforce authentication and authorization.

## Agent

You will need to install and configure the [PowerShell Universal Agent](../config/agent.md) to use Event Hubs. The agent is provided in multiple platforms, as an installable MSI on Windows and as a Docker container image.

## Send Events

From within the PowerShell Universal server, you can send events from a hub to connected clients using the `Send-PSUEvent` cmdlet (`Invoke-PSUCommand` is an alias to `Send-PSUEvent`).

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
