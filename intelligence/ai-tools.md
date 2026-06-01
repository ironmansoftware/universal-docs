---
description: Call PowerShell scripts in AI Agents and through MCP.
---

# AI Tools

AI Tools allow you to expose your PowerShell scripts as tools that agents can call in PSU and through the PSU MCP server. You can enforce authorization to limit who has access to the tools.&#x20;

## Create an AI Tool

Navigate to Intelligence / AI Tools and click Create AI Tool. Select a script to expose as an AI Tool. You can define whether you want to expose it as MCP by checking the MCP checkbox. Tools can also enforce authentication and authorization.&#x20;

### Description

The Description is very important for your tools. In order for agents to correctly select your tool, you need to provide a good description of when to call it and what it returns.&#x20;

### Parameters

Parameters are automatically discovered in your PowerShell scripts. It is very important to provide thorough comment-based help for your parameters to allow the agent to understand the use of your tool.

## Using a Tool in AI Agents

Within PSU AI Agents, you can assign tools by editing the agent properties and selecting the tool. Role based access controls will be enforce both at the agent prompt level and at the tool call level. The initiator of the prompt needs the proper roles in both cases.&#x20;

Calls to AI Tools will result in child jobs of the AI Agent prompt job.

## Using a Tool over MCP

Model Context Protocol (MCP) provides a mechanism to call agents remotely. PSU exposes your selected AI tools over a built in MCP server. You can access the MCP server at the `/api/v1/mcp` route. When connecting, you can specify an JWT bearer token to properly authenticate your agent. The configuration will depend on which agent you are using to connect to PSU.&#x20;

Calls to your tools via MCP will result in MCP jobs listed in your jobs table.&#x20;

## Access in GitHub Copilot

You can provide GitHub Copilot to your PowerShell Universal scripts by configuring the AI agent in VS Code.

In this example, we are using a script with a single call to Get-Process.

```powershell
Get-Process | Select-Object Name, Id
```

With the MCP plugin enabled, we can configure GitHub Copilot. You will need the extension installed before continuing. In VS Code, press `Ctrl+Shift+P` and search for `MCP: Add Server...`.

Select the HTTP option and enter the URL to the MCP server endpoint. You will need the `/api/v1/mcp` route. The full URL, by default, is `http://localhost:5000/api/v1/mcp`. Name the server whatever you would like.

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

If the server is configured properly, the Copilot plugin will list the number of tools.

With VS Code configured, we can now use our AI agent tool. Click the Copilot icon and open a new chat.

<figure><img src="../.gitbook/assets/image (307).png" alt=""><figcaption></figcaption></figure>

Within the chat window, you can prompt Copilot with a question such as `Can you please list all the processes as an array of strings in a new PowerShell scripts?` Copilot will call our PSU tool and retrieve the list of processes and then generate a PowerShell script in VS Code.

<figure><img src="../.gitbook/assets/image (310).png" alt=""><figcaption></figcaption></figure>

Because we also have an endpoint to start processes, you can also prompt Copilot to do so with a statement like: `Can you start a new process in PowerShell Universal named calc?`. This will cause the `calc.exe` process to start because the PSU endpoint will be called with that argument.
