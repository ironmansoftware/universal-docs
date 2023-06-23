---
description: New features in PowerShell Universal v4.
---

# What's New in v4?

## Event Hubs

Event Hubs allow client machines to receive events from the PowerShell Universal server and execute PowerShell locally. Event Hubs support authentication and transmitting data within the events.&#x20;

## Dashboards are Now Apps

Apps are a clearer description of what the previously named dashboard functionality represents. All the functionality of dashboards is still present in apps.&#x20;

## App Designer

A new drag and drop designer is now available for apps. A subset of controls can be used within the designer to visually layout and edit the properties of components.&#x20;

## Live App Documentation

PowerShell Universal now ships with live documentation for app components and features. You'll be able to quickly view examples and copy code directly into your apps.&#x20;

## App Components

We've added and updated components for apps. These include:

* Split Button
* Speed Dial
* Improved Data Grid&#x20;
* Updated Date and Time pickers

## Improved Diagnostics

### Health Checks&#x20;

PowerShell Universal will now periodically run health checks on the environment. These include checks on resource usage (CPU, memory, etc) and service account configuration.&#x20;

### Logging

The logging framework is now highly customizable, consistent and searchable. You can output to the file system, TCP, HTTP and even extend the framework by logging in your own custom PowerShell script.&#x20;

Logging can also be customized per feature (e.g. apps) and resource (e.g. a single app).&#x20;

## Updated Runtimes

The PowerShell Universal server has been updated to PowerShell 7.3 and .NET 7.&#x20;

## PowerShell Universal Modules

Modules can now include PowerShell Universal resources like scripts, schedules, apps and roles. This allows for distribution of functionality via standard package repositories.&#x20;

