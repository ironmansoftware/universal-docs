---
description: Learn about the Visual Studio Code extension for Universal.
---

# Visual Studio Code Extension

PowerShell Universal can be managed with the PowerShell Universal Visual Studio Code extension. It allows you to connect to a local Universal instance and manage APIs, dashboards and scripts.

## Installation

You can download the extension from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=devolutionsinc.devolutions-powershell-universal). You can also download the extension from within the Visual Studio Code extension pane. Search for Devolutions PowerShell Universal and click Install.

{% hint style="info" %}
The 2026.2.x extension requires a 2026.2.x server or later.
{% endhint %}

## Connections

The extension will prompt you for the URL and App Token used to connect to your PowerShell Universal instance. Follow the instructions within the extension when it starts up.

### Automatic Discovery of Developer Instance

If you are running PowerShell Universal that has been licensed as a developer instance, the VS Code extension will automatically discover and authenticate. There is no configuration you need to do on your part.&#x20;

### Configure Connections Manually

To add a new connection to a PowerShell Universal instance, click the Add Connection button. You will prompted for a name, URL and app token to establish the connection.&#x20;

### Active Connection

Using the connection pane, you always view resources for the select connection tree. Click the Connect button to set a connection to the Active connection. The Active connection influences how the Jobs tree view behaves. The Active connection's jobs will be shown with in the page.&#x20;

## Resources

The PowerShell Universal extension adds a new activity pane panel for PowerShell Universal. Resources are organized based in a similar manner as they are in the admin console. You can view resources like:

* API Endpoints and Docs
* Scripts, schedules, terminals and workflows
* Apps
* AI Agents
* Variables
* Tags

Some resources also provide actions within VS Code. Some examples are:

* Running scripts from VS Code
* Opening a terminal and executing commands
* Open a web browser to apps

## Jobs

You can view a list of jobs queued, running or run by the PowerShell Universal server in the jobs activity pane. Click the Filter icon to view active, completed or failed jobs. You can also include an optional filter string.&#x20;

## Virtual File System

From the connection tab, you can click the Connect button to activate the Virtual File System for the select PowerShell Universal instance. This will open the PSU repository directory in a virtual workspace in VS Code. You can view, edit, create and delete files directly in VS Code. Each change will then be reflected on the PSU server. Changes made through the PowerShell Universal extension will automatically reload resources like endpoints, apps and scripts so they will be immediately reflected in the PSU instance.

## MCP Server

When connecting to a PowerShell Universal developer instance, the MCP server for that instance will be configured automatically. This provides access to all the [built in MCP tools ](../intelligence/built-in-mcp-tools.md)provided by PSU.
