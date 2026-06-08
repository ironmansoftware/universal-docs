---
description: Call PowerShell scripts in AI Agents and through MCP.
---

# AI Tools

AI Tools let you expose PowerShell scripts as callable tools for AI Agents and for external MCP clients. They are useful when you want a model to retrieve PSU data, run a controlled action, or hand structured output back into a prompt.

Each tool can require authentication, enforce roles, and optionally be exposed over MCP.

## Create an AI Tool

Navigate to Intelligence / AI Tools and click Create AI Tool. Select the script to expose, then decide whether the tool should be available:

* only to PSU AI Agents
* to both AI Agents and MCP clients by enabling `MCP`

If `Authenticated` is enabled, the caller must be signed in. If roles are also assigned, the caller must have at least one of those roles.

### Description

The description is one of the most important parts of the tool. It should tell the model:

* when to use the tool
* what the tool returns
* whether the tool changes state
* any important parameter expectations

Short, concrete descriptions work best.

### Parameters

Parameters are discovered automatically from the PowerShell script. Comment-based help is strongly recommended because PSU uses it to build better tool descriptions and parameter schemas.

This example script makes a good AI Tool because it has clear parameters and predictable output:

```powershell
<#
.SYNOPSIS
Returns the top running processes by CPU usage.

.PARAMETER Count
The number of processes to return.
#>
param(
        [Parameter()]
        [int]$Count = 5
)

Get-Process |
        Sort-Object CPU -Descending |
        Select-Object -First $Count Name, Id, CPU
```

Expose it as a tool:

```powershell
New-PSUAiTool -Name 'Get Running Processes' `
    -Description 'Returns the top running processes by CPU usage.' `
    -ScriptFullPath '/tools/Get-RunningProcesses.ps1' `
    -Authenticated `
    -Role @('Operator') `
    -Mcp
```

Useful cmdlets include:

* `Get-PSUAiTool`
* `New-PSUAiTool`
* `Set-PSUAiTool`
* `Remove-PSUAiTool`

For example, to review tools:

```powershell
Get-PSUAiTool
Get-PSUAiTool -Name 'Get Running Processes'
```

## Using a Tool in AI Agents

Within an AI Agent, assign tool names directly or use wildcard patterns such as `ticket_*` or `*`. PSU only makes the matching tools available to that agent.

Role-based access is enforced at both levels:

* the user must be allowed to run the agent
* the user must also be allowed to run the tool

Tool executions started by an agent appear as child jobs of the AI prompt job.

Example agent configuration:

```powershell
Set-PSUAiAgent -Name 'SupportAgent' -Tool @('Get Running Processes', 'ticket_*')
```

## Using a Tool over MCP

Model Context Protocol (MCP) allows remote clients such as GitHub Copilot to discover and call your tools. PSU exposes MCP at `/api/v1/mcp`.

Only tools with `Mcp` enabled are listed to MCP clients.

When exposed over MCP, tool names are normalized for the client. For example, spaces and periods are converted to underscores.

When an MCP client connects, PSU filters the visible tools based on:

* whether the tool is marked for MCP
* whether the caller is authenticated when required
* whether the caller has at least one required role

Calls made through MCP appear as MCP jobs in the Jobs page.

If your client supports bearer tokens, provide a PSU app token when connecting to the MCP endpoint.

## Access in GitHub Copilot

GitHub Copilot can call PSU tools when VS Code is configured to connect to the PSU MCP server.

In this example, the tool wraps a script that returns running processes:

```powershell
Get-Process | Select-Object Name, Id
```

With the MCP extension enabled, press `Ctrl+Shift+P` and run `MCP: Add Server...`.

Choose the HTTP option and enter the MCP endpoint URL. By default, this is `http://localhost:5000/api/v1/mcp`.

The resulting `settings.json` contents will look something like this.

```json
"mcp": {
    "servers": {
        "PSU": {
            "url": "http://localhost:5000/api/v1/mcp"
        }
    }
}
```

If the connection is successful, Copilot will show the number of available tools.

You can then ask Copilot to use the PSU tool. For example:

```text
Use the PSU tool to list the top 5 processes and create a PowerShell script that writes them to JSON.
```

If you also expose a tool that starts a process, a prompt like this can trigger that action:

```text
Use the PSU tool to start a new process named calc.
```

Keep tool descriptions and parameter help clear so Copilot can choose the correct tool without trial and error.
