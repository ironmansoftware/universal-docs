---
description: Built in MCP Tools for PowerShell Universal development.
---

# Built In MCP Tools

PowerShell Universal includes several built-in MCP tools that help coding agents inspect PSU resources and learn the local command surface. These are available from the `/api/v1/mcp` endpoint.

These built-in tools are separate from your custom [AI Tools](ai-tools.md). In practice, they are most useful when an agent needs to inspect scripts, endpoints, apps, or cmdlet help before making a change.

To access them remotely, connect an MCP client to `/api/v1/mcp` and authenticate with a PSU app token. The built-in tools require `Administrator` or `Operator` access.

## Typical Flow

Most coding sessions follow a pattern like this:

1. Call `list_resource_types` to see what kinds of PSU resources are available.
2. Call `list_resources` to find the specific script, endpoint, app, or workflow you need.
3. Call `list_commands` or `list_app_commands` to discover the cmdlets available on that PSU server.
4. Call `command_help` for focused help on the cmdlet you plan to use.
5. Call `reload_resource` after changing configuration so PSU reloads the resource.

## list\_resource\_types

Returns the resource types available on the connected PSU instance, such as scripts, endpoints, apps, and workflows.

Use this first rather than guessing the available type names.

Example:

```text
list_resource_types
```

## list\_resources

Lists resources of a given type and returns them as JSON.

Parameters:

* `type` - The resource type to inspect. Use a value returned by `list_resource_types`.
* `filter` - A wildcard filter that matches resource names or descriptions.

Example:

```json
{
	"type": "<resource type from list_resource_types>",
	"filter": "deploy*"
}
```

## list\_commands

Searches for commands in a PowerShell module installed on the PSU server.

Parameters:

* `module` - The module name.
* `name` - A command name filter. Wildcards are supported.

This is usually followed by `command_help`.

Example:

```json
{
	"module": "Universal",
	"name": "*PSUAi*"
}
```

## command\_help

Returns help information for a command available on the PSU server.

Parameters:

* `module` - The module name.
* `command` - The command to inspect.
* `parameter` - Optional parameter name or wildcard pattern.
* `full` - Include the full help output.
* `examples` - Include examples.

Start with targeted help instead of always requesting the full help text.

Example:

```json
{
	"module": "Universal",
	"command": "Invoke-PSUAiAgent",
	"parameter": "Prompt",
	"full": false,
	"examples": true
}
```

## list\_app\_commands

Returns the app-specific cmdlets used to build PSU apps, especially `UD` component and interactivity commands.

Parameter:

* `filter` - A wildcard filter for the command name.

Example:

```json
{
	"filter": "New-UD*"
}
```

## reload\_resource

Reloads a PSU resource type after files or configuration have changed.

Parameter:

* `resourceType` - The resource type to reload.

Example:

```json
{
	"resourceType": "<resource type from list_resource_types>"
}
```

This is especially useful when an agent edits configuration through a local checkout or remote file system and then needs PSU to pick up the change.
