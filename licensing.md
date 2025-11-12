---
description: Licensing options for PowerShell Universal
---

# 🔑 Licensing

PowerShell Universal is licensed per server. We provide licenses for individuals and organizations.

You can purchase a license on [our website](https://ironmansoftware.com/pricing/powershell-universal).

## What's a server?

A server is a single running instance of PowerShell Universal.

### What if I have multiple containers?

The license applies to each container instance and not the container host. For example, if you have 10 container instances running, you will need 10 licenses.

### What if I have multiple sites on a single IIS server?

Each website running PowerShell Universal will need a license and not a single license for the entire IIS server.

## Install a License

To install a license, click Settings \ License. Click the Add License button to upload your license file. You can also install licenses using the `Set-PSULicense` cmdlet. Offline licenses do not require an internet connection but will need to be reinstalled when the subscription expires, in you wish to update the version of PowerShell Universal. Online licenses require an internet connection and access to `https://ironmansoftware.com` in order to verify subscription status.

You can use the `PSULICENSE` environment variable to set a license. The value of this environment variable needs to be the contents of the license file.

Proxy configuration can be done by clicking Settings \ General and configuring the proxy URI and, optionally, credentials. You can also configure proxy settings with the `Set-PSUSetting` cmdlet.

### Account-Based Licensing

When using account-based licensing, you will enter your account's license key. Whenever you activate a PowerShell Universal server, it will assign a license to computer. This license key does not change so there is no need to install a new license when renewing. You can view the assigned computers and account license key in your Ironman Software account.

The PowerShell Universal server needs to have access to ironmansoftware.com.

<figure><img src=".gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### Offline Licenses

Offline license files are required for environments that do not have internet access. You will need to install a new license file when you plan to upgrade to a version past the expiration date of the license.

### Online Licenses

Online licenses work the same as offline but check the subscription status on ironmansoftware.com. The license is tied to a specific subscription and may require a change after renewal. We recommend account-based licensing over online licenses.

## Developer Licenses

When a server license is purchased, you will be able to generate developer licenses for users building solutions for your team. Their intent is to be used by individual developers in their local environments. Do not use developer licenses when hosting a server for remote access for testing or production. Instances of PowerShell Universal running with a Developer License will display a water mark in the admin console and any apps stating they are intended only for development purposes.

You can generate a developer license on the Settings \ License page by clicking the Generate Developer License button.

![Generate Developer License](<.gitbook/assets/image (96).png>)

## Licensed Features

The following features of PowerShell Universal require a license.

* Debugging Tools
* Enterprise Authentication
  * OpenID Connect
  * SAML2
  * WS-Federation
  * Windows Authentication
  * Custom Authentication Scripts
  * Client Certificate
  * App Tokens
* Enterprise Authorization
  * Permissions
  * Custom Authorization Scripts
* Platform
  * Git Support
  * Module Management
  * Non-Database Credential Vaults
  * SQL Support
  * PostgreSQL Support
  * Published Folders
  * Cache Management
  * Computer Groups
  * Translations
* Settings
  * Branding
  * Tags
* APIs
  * Event Hubs
  * OpenAPI Documentation
* Automation
  * Triggers
  * Terminals
  * Tests
* Apps
  * App Page Editor
  * App Function Editor
