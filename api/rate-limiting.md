---
description: Rate limiting options for Universal.
---

# Rate Limiting

{% hint style="info" %}
Rate limiting requires a [license](https://ironmansoftware.com/pricing/powershell-universal).
{% endhint %}

PowerShell Universal lets you rate limit requests made to the web server. You can configure rate limiting per endpoint and per period. By default, the client IP address rate limits clients.

Configuration data for rate limits are stored in the `ratelimits.ps1` file.

## Configuring Rate Limiting

To configure rate limiting, visit the APIs / Rate Limiting page. Click the Add button and define a new rate limit rule.

{% hint style="warning" %}
Rate limiting affects all URLs for the server. If you enforce rate limiting that isn't correctly configured, you can negatively affect the management API.
{% endhint %}

### Method

The method is the HTTP method to for this rule. If you use `*` , this rule affects all HTTP methods. You can also select a single method by picking it from the drop down.

### Endpoint

The endpoint is the URL that you are rate limiting. You can rate limit all URLs by using a `*`. You can define specific URLs by defining the relative path: `/api/user`.

### Limit

This is the number of requests in the time frame before rate limiting kicks in.

### Period

This is the period over which the rate limit is counted. For example, if you select a period of 10 minutes and a limit of 100, then up to 100 requests can be made to the method and endpoint you have selected.

## Allow Lists

To disable rate limiting for particular IP Addresses, clients, and endpoints, add them to the rate limiting allow lists. Find these by clicking the settings button.

The below example prevents the loopback adapter from being rate limited.

```powershell
Set-PSUSetting -RateLimitIpAddressAllowList @("127.0.0.1")
```

## Example: Limit Custom API

Limits callers of the `/api/users` endpoint to 100 requests per minute.&#x20;

```powershell
New-PSURateLimit -Endpoint "GET|/api/users" -TimeSpan "00:01:00" -Limit 100
```

## Example: Limit Management API

Limits callers of the management API to 100 requests per second.&#x20;

```powershell
New-PSURateLimit -Endpoint "*|/api/v1/*" -TimeSpan "00:00:01" -Limit 100
```

## API

* [New-PSURateLimit](../cmdlets/New-PSURateLimit.txt)
* [Set-PSUSetting](../cmdlets/Set-PSUSetting.txt)
