---
description: Anonymous data collected by Ironman Software about PowerShell Universal.
---

# Telemetry

PowerShell Universal collects opt-in telemetry data. During an MSI install, the UI will prompt for whether to collect telemetry data. You can also configure telemetry data on other systems to help us learn more about how PSU is used.&#x20;

## How do you configure Telemetry?

Telemetry is configured via the `appsettings.json` configuration system. If you have enabled telemetry and would like to disable it, you can do so by modifying the file in `%ProgramData%\PowerShellUniversal\appsettings.json`. It can also be enabled and disabled by setting the environment variable `PSUTelemetry`. Set the value to `true` to send telemetry.

## Why are we collecting telemetry?

Telemetry provides information about how the product is being used. It helps us make decisions about which features to focus on and provides feedback on error rates in new versions of the product.&#x20;

## What are we collecting?

Below are the following data items we collect and why we collect them.&#x20;

### Session ID

The session ID is a GUID generated on startup of the PowerShell Universal process. It isn't based on any info about the system and just used to correlate additional telemetry data sent by the process.&#x20;

### Version

This is the PowerShell Universal version being run. It allows us to see which versions of the product our users are using.&#x20;

### Operating System

We use the operating system to help determine which operating systems our product is being run to ensure we focus on quality and features for that platform.&#x20;

### Timestamp and Uptime&#x20;

The timestamp indicates when the telemetry data was sent. The Uptime value provides how long the PSU server is running. Timestamp is helpful for correlation of data and uptime is useful to see how long PSU servers are running to ensure we make the platform as stable as possible for the mean runtime.&#x20;

### Identity, Computer and Role Counts

We send the number of identities, computers and roles in a system to see how large PSU installations are. This helps us focus our development efforts to ensure the greatest number of installations are satisfied.&#x20;

### Resource Counts

We will send several resource counts to see how often certain resources are used and to what extent. These include:&#x20;

* Endpoints
* Apps
* Scripts
* Schedules
* Portal Pages

Highly used resources will receive more development.&#x20;

### License Status

License status information is useful for marketing purposes and to determine which features lead to licensed instances. Paying customers ensure we can support our development and support initiatives for the platform.&#x20;

### Errors in the Last Error

We use error notifications as a metric for determining how healthy PSU environments of particular version is. This can help provide data about the health of a release before too many customers are impacted.&#x20;

## How do we collect data?&#x20;

We do not use any third-party systems to collect or store data. PSU instances with telemetry enabled will send a telemetry request to Ironman Software, directly, once at startup and once an hour. Telemetry will have no impact on performance but does require internet access for the node with the feature enabled.&#x20;

If a firewall is in use, you will need to provide access to `ironmansoftware.com`.&#x20;

We use the standard HttpClient class in .NET to send this data and do not provide any custom headers to the request. We will use a proxy if it has been configured in PSU.&#x20;

## Will more data be collected?&#x20;

We may add more data points in future versions of the product. We will document any changes here and in the changelog. We will only collect anonymous information.
