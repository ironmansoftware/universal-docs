---
description: New features in PowerShell Universal v5.
---

# 🆕 What's New in v5?

## New Admin Console

The admin console has been rebuilt using Blazor for ASP.NET. The look and feel are the same but more tightly associated with the backend Universal platform.

## Portal

The [PowerShell Universal Portal](broken-reference) provides a simple to use access point for consumers of PSU resources.  Resources can be assigned by role and will be grouped by tags in a searchable interface without the complexities of the admin console.&#x20;

### Pages and Widgets

Portal [Pages ](portal/portal-pages.md)and [Widgets ](portal/portal-widgets/)provide easy to use UI components that can be visually positioned on pages that then can be assigned to roles. Widgets are built using Blazor and PowerShell, accept parameters and are interactive.

## Script Library

PowerShell Universal now ships with built in modules that can be install directly into the running instance to add resources without having to write code.&#x20;

The [Script Library is open source](https://github.com/ironmansoftware/scripts) and contributions to the library will ship with the product.&#x20;

## Granular Permissions

Authorization within the platform is now configured via a[ granular permission system](security/enterprise-security/permissions.md) that controls which users have access to which resources. This also includes new roles for specific feature groups, so administrators do not need to configure privileges for every scenario.&#x20;

## PostgreSQL Support

PostgreSQL is now supported as a persistence store. PostgreSQL is open source and free.

## Updated Runtimes

PowerShell Universal v5 is built on .NET 8 and PowerShell 7.4.

## gRPC Cmdlets

The Universal module now uses gRPC for all communication with the system. gRPC is an interprocess communication technology that is fast and runs over HTTP. By unifying on a single technology, the cmdlets now take advantage of all the granular privileges and helps reduce technical debt in the platform.&#x20;

## Windows PowerShell 5.1 and PowerShell 7 Environments

The Agent environment has been replaced with Windows PowerShell 5.1 and PowerShell 7 environments. These environments host the PowerShell engine but allow for better control of assembly loading to ensure more modules are compatible with PowerShell Universal. While pwsh.exe is still supported, we suggest utilizing PowerShell 7 when possible. The Windows PowerShell 5.1 environment is now a requirement for running this version of PowerShell and powershell.exe is no longer supported.

