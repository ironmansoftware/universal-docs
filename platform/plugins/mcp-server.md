---
description: Enable a model context protocol server.
---

# MCP Server

{% hint style="warning" %}
This plugin is experimental and is only available in [PowerShell Universal 5.7.0 nightly builds](https://powershelluniversal.com/release/powershell-universal-nightly).&#x20;
{% endhint %}

**Identifier:** `PowerShellUniversal.Plugins.MCP`

The Model Context Protocol is a mechanism for communicating with AI agents, like GitHub CoPilot. You can enable this MCP plugin to expose your scripts as an MCP AI agent tool.&#x20;

Tools will include the following information to AI agents:

* Script title
* Description
* Parameters with name, type, help text, and mandatory flag.

{% hint style="danger" %}
The experimental MCP plugin does not enforce access controls.&#x20;
{% endhint %}

## Access in GitHub CoPilot

You can provide GitHub CoPilot to your PowerShell Universal scripts by configuring the AI agent in VS Code.&#x20;

In this example, we are using a script with a single call to Get-Process.&#x20;

```powershell
Get-Process | Select-Object Name, Id
```

With the MCP plugin enabled, we can configure GitHub Copilot. You will need the extension installed before continuing. In VS Code, press `Ctrl+Shift+P` and search for `MCP: Add Server...`.

Select the HTTP option and enter the URL to the MCP server endpoint. You will need the `/sse` route. The full URL, by default, is `http://localhost:5000/sse`. Name the server whatever you would like.

The resulting `settings.json` contents will look something like this.

```json
"mcp": {
    "servers": {
        "PSU": {
            "url": "http://localhost:5000/sse"
        }
    }
}
```

If the server is configured properly, the CoPilot plugin will list the number of tools.

<figure><img src="../../.gitbook/assets/image (313).png" alt=""><figcaption></figcaption></figure>

With VS Code configured, we can now use our AI agent tool. Click the Copilot icon and open a new chat.

<figure><img src="../../.gitbook/assets/image (307).png" alt=""><figcaption></figcaption></figure>

Within the chat window, you can prompt Copilot with a question such as `Can you please list all the processes as an array of strings in a new PowerShell scripts?` Copilot will call our PSU tool and retrieve the list of processes and then generate a PowerShell script in VS Code.

<figure><img src="../../.gitbook/assets/image (310).png" alt=""><figcaption></figcaption></figure>

Because we also have an endpoint to start processes, you can also prompt Copilot to do so with a statement like: `Can you start a new process in PowerShell Universal named calc?`. This will cause the `calc.exe` process to start because the PSU endpoint will be called with that argument.
