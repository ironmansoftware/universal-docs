---
description: What's new in PowerShell Universal.
---

# 📰 What's new?

## 2026.2

### AI Agent Jobs

Configure AI Agent with access to OpenAI, Anthropic and local LLM models to run prompts within the PowerShell Universal jobs engine. Define agent context and assign AI tools to allow agents to execute PowerShell scripts in a secure manner. Integrate AI agent prompts directly into Workflows.

### AI and MCP Tools

Expose PowerShell scripts for consumption by local AI agents or through Model Context Protocol (MCP) for agents running outside PowerShell Universal. Tools automatically create the proper metadata for each script and expose its description and parameters. Execution of tools are logged in the job history table and protected by role-based access controls.&#x20;

### Built-In MCP Tools

Built-In MCP tools provide better context to agents working with the PSU platform. Tools that return information about resource types, resources, and commands ensure that agents can more accurately and quickly build solutions autonomously.

### Workflows

A new workflow engine allows users to chain together PowerShell scripts and AI agent prompts in a visual designer to quickly compose automation solutions. Workflows feature the same ability as scripts for execution, schedule and security.&#x20;

### Visual Studio Code Extension

A fully redesigned VS Code extension offers easier configuration, views of resource with linked instances, virtual file system support for remote editing and automatic configuration of the PSU MCP server to enable GitHub Copilot and other agents to access and inspect the platform. By blending PSU MCP with the virtual file system, agents can build solutions with live PSU instances and verify their work.

### Enhanced File-Based Change Tracking

File-based change tracking can now inspected to see all the changes that are made to disk when using PSU. By default, changes will can be registered and users can decide whether to reload resources affected by the file changes. Optionally, changes can be applied automatically to quickly iterate on local PSU instances.&#x20;

### .NET 10 and PowerShell 7.6

The platform now targets .NET 10 and PowerShell 7.6 for integrated environments, the PowerShell host processes and agent.&#x20;

### Deployment-by-Module

PowerShell Universal configurations can now be deployed through modules, including installing required modules, from registered PowerShell Resource Repositories. This provides an approach to build and version configuration artifacts without having to rely on git directly in PSU.&#x20;

