---
description: Examples of PowerShell Universal configurations.
---

# Examples

This page contains examples of PowerShell Universal configurations. All examples are built using single-file hosting and configuration. These examples assume that you have PowerShell Universal installed. To install PowerShell Universal, use the following command line. 

```text
Install-Module Universal
Install-PSUServer -AddToPath
```

You can login to PowerShell Universal using the username `admin` and any password. 

{% hint style="info" %}
Have an example of an API, Dashboard or Script that you think would fit nicely on this page? Feel free to open a pull-request on our [documentation repository](https://github.com/ironmansoftware/universal-docs). 
{% endhint %}

## Table of Contents

* Active Directory
  * [Reset Password](active-directory.md#reset-password)
  * [List Locked Accounts](active-directory.md#list-locked-accounts)
  * [Restore Deleted User](active-directory.md#restore-deleted-user)
* Hyper-V
  * [Virtual Machine Creator](hyper-v.md#virtual-machine-creator)
* Image Processing
  * [Convert JPEG to PNG](image-processing.md#convert-jpeg-to-png)
  * [Convert JPEG to PNG API](image-processing.md#convert-jpeg-to-png-api)
  * [Rate Limited API](image-processing.md#rate-limited-conversion-api)
* Monitoring
  * [Windows Performance Counter Dashboard](monitoring.md#windows-performance-counter-charts)
* Slack
  * [Send a Message to Slack](slack.md#send-message-to-slack)
  * [Send a Message to Slack when a Script Fails](slack.md#send-slack-message-on-failed-job)

