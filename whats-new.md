---
description: What's new in PowerShell Universal.
---

# 📰 What's new?

## 2026.1&#x20;

### Devolutions Account Login

Login with a [Devolutions Account](https://docs.devolutions.net/portal/profile/create-devolutions-account/) and receive a free PowerShell Universal developer license. You can use this license for development and testing. It will activate the full feature set. This license cannot be used for production workloads. It requires accessing PowerShell Universal from the local machine.

### New Version Scheme

PowerShell Universal has aligned with other Devolutions' products and will use dated versions moving forward.

## 5.6

### Improved Notification Indicator

Notifications are now grouped by type in the drop down for the indicator and provides a quick way to view notifications of specific levels.

### Script Upload and Discovery

Upload scripts from your local machine to PowerShell Universal or discover scripts that are already on the server but not registered with the platform.

### SSH Key Support for Git

PowerShell Universal can now generate SSH keys for use when connecting with remote git repositories.

## 5.5

### Windows Forms Login

Login with Windows credentials without having to use Windows Authentication. Enter your user name and password and PowerShell Universal will perform a local login and evaluate your group membership for role-based access.

### Reference and Using Support for C# Endpoints

C# endpoints can now reference assemblies and include using statements to extend the functionality provided and simplify the code written.

## 5.4

### PSU Admin CLI

Access an in-browser terminal that is automatically authenticated with your user's permissions to invoke PSU cmdlets against the system.

### Script Metrics

Track success rates, execution time and target variables like where the job was run and as which user.

### Least Busy Load Balancer for Jobs

PSU will now select the least busy server to run jobs when multiple servers are valid targets for a job.

### PowerShell 7.5 and .NET 9.0

Updated to PowerShell 7.5 SDK and .NET 9.0 to support the latest features in both platforms.

## 5.3&#x20;

### SAML2 Metadata Support

Load SAML2 metadata when configuration authentication to easily enable logins from identity providers.

### Run as Support for APIs

Run API endpoints as alternate user accounts.

## 5.2&#x20;

### Git Settings and Branch Support

Switch between different git repositories and branches to quickly change the configuration of the PowerShell Universal server.

### PowerShell Repository Management

Register custom PowerShell repositories to allow for discovery and installation of PowerShell modules outside of the PowerShell Gallery.

### Vault Management

Register secret vaults in PowerShell Universal to more easily integrate with third-party vaults like Az.KeyVault and CyberArk.

## 5.0

### New Admin Console and Portal

The admin console has been rebuilt using Blazor for ASP.NET. The look and feel are the same but more tightly associated with the backend Universal platform. The [PowerShell Universal Portal](broken-reference/) provides a simple-to-use access point for consumers of PSU resources. You can assign resources by role, and they will be grouped by tags in a searchable interface without the complexities of the admin console.

### Granular Permissions

Authorization within the platform is now configured via a[ granular permission system](https://docs.powershelluniversal.com/security/enterprise-security/permissions) that controls which users have access to which resources. This also includes new roles for specific feature groups, so administrators do not need to configure privileges for every scenario.

### PostgreSQL Support

PostgreSQL is now supported as a persistence store. PostgreSQL is open source and free.

### Updated Runtimes

PowerShell Universal v5 is built on .NET 9 and PowerShell 7.5.

### gRPC Cmdlets

The Universal module now uses gRPC for all communication with the system. gRPC is an interprocess communication technology that is fast and runs over HTTP. By unifying on a single technology, the cmdlets now take advantage of all the granular privileges and help reduce technical debt in the platform.
