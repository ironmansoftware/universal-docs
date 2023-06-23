---
description: Rate limiting options for Universal.
---

# Rate Limiting

{% hint style="info" %}
Rate limiting requires a [license](https://ironmansoftware.com/pricing/powershell-universal).
{% endhint %}

PowerShell Universal provides the ability to rate limit requests made to the web server. Rate limiting can be configured on a per endpoint and per period. By default, the client IP address is used to rate limit clients.&#x20;

Configuration data for rate limits are stored in the `ratelimits.ps1` file.&#x20;

## Configuring Rate Limiting&#x20;

To configure rate limiting, you can visit the APIs / Rate Limiting page. Click the Add button and define a new rate limit rule.&#x20;

![](<../.gitbook/assets/image (460).png>)

{% hint style="warning" %}
Rate limiting affects all URLs for the server. If you enforce rate limiting that isn't correctly configured, you can negatively affect the management API.&#x20;
{% endhint %}

### Method

The Method is the HTTP method to for this rule. If you use `*` , all HTTP methods will be affected by this rule. You can also select a single method by picking it from the drop down.&#x20;

### Endpoint

The endpoint is the URL that you are rate limiting. You can rate limit all URLs by using a `*`. You can define specific URLs by define the relative path: `/api/user`.&#x20;

### Limit

The number of request in the time frame before rate limiting kicks in.&#x20;

### Period

The period over which the rate limit is counted. For example, if you select a period of 10 minutes and a limit of 100, then up to 100 requests can be made to the method and endpoint you have selected.&#x20;

## Allow Lists

To disable rate limiting for particular IP Addresses, clients and endpoints you can add them to the rate limiting allow lists. You will find these by clicking the settings button.&#x20;

![](<../.gitbook/assets/image (178).png>)

## API

* [New-PSURateLimit](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSURateLimit.txt)
* [Set-PSUSetting](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Set-PSUSetting.txt)
