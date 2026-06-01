---
description: Built in MCP Tools for PowerShell Universal development.
---

# Built In MCP Tools

PowerShell Universal ships with several MCP tools defined to provide enhanced development with coding agents, like GitHub Copilot. You can connect to the `/api/v1/mcp` endpoint to access these tools. You will need an administrator app token to do so.&#x20;

## list\_resource\_types

Returns the type of resources provided by this instance of PowerShell Universal. This will include information about the resource type (e.g. endpoints, scripts, apps) like why the agent would need to know about them and what they do. Because resource types can change over time, this provides a mechanism to allow for dynamic retrieval about them.&#x20;

## list\_resources

Lists resources defined within the system. This accepts a `type` and a `filter` parameter to allow agents to inspect and search for resources in the system. Resources will be returned as JSON back to the agent.&#x20;

## list\_commands

Allows the agent to search for commands in modules installed on the PSU server. This accepts a `module` and a `filter` parameter to perform the search. This is typically paired with `command_help` to learn more about commands available to the agent. This is useful when editing scripts locally that then need to run on the PSU server.&#x20;

## command\_help

Returns help information about a command. This accepts `module`, `command`, `parameter`, `full`, and `examples` parameters. The `parameter` parameter is the name of the parameter to return the help for. The `full` and `examples` parameters are passed to `Get-Help` to provide more complete context for a command.&#x20;

## list\_app\_commands

Due to the complexity and unique command surface for apps, PSU exposes this command to provide better guidance when building PSU apps. This accepts a `filter` parameter and will return information about components and interactivity cmdlets used in the app framework.

## reload\_resource

This tool allows agents to reload resources. This is useful if you are working locally or remote, via the VS Code virtual file system. If the agent makes changes to configuration files, this provides the agent a way to reload them to then inspect the results of its work.
