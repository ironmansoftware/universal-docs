---
description: New features in PowerShell Universal v5.
---

# 🆕 What's New in v5?

## New Admin Console

The admin console has been rebuilt using Blazor for ASP.NET. The look and feel are the same but more tightly associated with the backend Universal platform.

## Portal

The [PowerShell Universal Portal](broken-reference/) provides a simple-to-use access point for consumers of PSU resources. You can assign resources by role, and they will be grouped by tags in a searchable interface without the complexities of the admin console.

### Pages and Widgets

Portal [Pages ](portal/portal-pages.md)and [Widgets ](portal/portal-widgets/)provide easy-to-use UI components that you can visually position on pages, which can be assigned to roles. Widgets are built using Blazor and PowerShell accept parameters, and they are interactive.

## PowerShell Universal Gallery

The PowerShell Universal Gallery is now integrated directly in PowerShell Universal. Access pre-built solutions for your PowerShell Universal environment.

You can view the [Gallery repository here](https://github.com/ironmansoftware/gallery).

## Granular Permissions

Authorization within the platform is now configured via a[ granular permission system](security/enterprise-security/permissions.md) that controls which users have access to which resources. This also includes new roles for specific feature groups, so administrators do not need to configure privileges for every scenario.

## PostgreSQL Support

PostgreSQL is now supported as a persistence store. PostgreSQL is open source and free.

## Updated Runtimes

PowerShell Universal v5 is built on .NET 9 and PowerShell 7.5.

## gRPC Cmdlets

The Universal module now uses gRPC for all communication with the system. gRPC is an interprocess communication technology that is fast and runs over HTTP. By unifying on a single technology, the cmdlets now take advantage of all the granular privileges and help reduce technical debt in the platform.

## Windows PowerShell 5.1 and PowerShell 7 Environments

The Agent environment has been replaced with Windows PowerShell 5.1 and PowerShell 7 environments. These environments host the PowerShell engine, but they allow for better control of assembly loading to ensure more modules are compatible with PowerShell Universal.&#x20;
