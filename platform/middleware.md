---
description: Customize HTTP requests in PowerShell Universal.
---

# Middleware

Middleware is run during each HTTP request by the PowerShell Universal server. It gives you the opportunity to customize features of the request like status code, headers and cookies.&#x20;

{% hint style="warning" %}
Since middleware is executed during each request, performance should be a consideration when implementing custom middleware.&#x20;
{% endhint %}

### Middleware.ps1

The middleware.ps1 file can be created in the `.universal` folder using the `New-PSUMiddleware` cmdlet.&#x20;

Each middleware instance receives a [HttpContext](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/use-http-context?view=aspnetcore-7.0) object when it is called. The middleware should return true or false. If false is returned, the middleware will stop passing the context to additional items on the middleware pipeline.

The below example adds a test cookie to the response.&#x20;

```powershell
New-PSUMiddleware -Name 'Middle' -ScriptBlock {
    param($HttpContext)
    $HttpContext.Response.Cookies.Append('X-Test', "Test")
    $true
}
```
