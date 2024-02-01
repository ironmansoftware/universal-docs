---
description: Plugins that extend the PowerShell Universal platform.
---

# Plugins

Plugins are functionality that are not enabled by default. A publicly available plugin API is currently being developed and will be released with a future version of PowerShell Universal. Below are a list of the plugins that are shipped with PowerShell Universal v4.2 and later.&#x20;

## Enabling Plugins

Plugins are enabled in `appsettings.json` or through environment variables. See [App Settings  ](../config/settings.md)for information on where to configure these options. Any changes made to the configuration will require a restart of the PowerShell Universal service.&#x20;

```json
{
    "Plugins": [
        "SQL",
        "PowerShellUniversal.Language.CSharp"
    }
}
```

## C# API Environment

**Identifier:** `PowerShellUniversal.Language.CSharp`

This plugin creates a C#-based environment that can be used to create API endpoints with C# code. APIs created with C# are much faster than PowerShell-based endpoints. Endpoints run directly in the PowerShell Universal service. Any exception thrown from your endpoint will be handled and a valid status code will be returned to the caller.&#x20;

You must create endpoints with the -Path parameter and specify the `C#` environment for the endpoint to function properly.

```powershell
New-PSUEndpoint -Url /csharp -Path csharp.cs -Environment 'C#'
```

**Defining an Endpoint**&#x20;

Within the C# endpoint, there are two classes that are of interest. The first is the `request` variable that is passed to the endpoint. It is an `ApiRequest` object.&#x20;

```csharp
public class ApiRequest
{
    public long Id { get; set; }
    public ICollection<KeyValue> Variables { get; set; } = new List<KeyValue>();
    public IEnumerable<ApiFile> Files { get; set; } = new List<ApiFile>();
    public string Url { get; set; }
    public ICollection<KeyValue> Headers { get; set; } = new List<KeyValue>();
    public byte[] Data { get; set; }
    public int ErrorAction { get; set; }
    public ICollection<KeyValue> Parameters { get; set; } = new List<KeyValue>();
    public string Method { get; set; }
    public ICollection<KeyValue> Cookies { get; set; } = new List<KeyValue>();
    public string ClaimsPrincipal { get; set; }
    public string ContentType { get; set; }
    public string[] Roles { get; set; }
}
```

In your endpoint, you can access this variable automatically.&#x20;

```csharp
if (request.ContentType == "application/json")
{
     // Do some stuff with JSON
}
```

The endpoint must return an `ApiResponse` object. This object has the following definition.&#x20;

```csharp
public class ApiResponse
{
    public int StatusCode { get; set; } = 200;
    public string Body { get; set; }
    public List<KeyValue> Cookies { get; set; } = new List<KeyValue>();
    public byte[] Data { get; set; } = Array.Empty<byte>();
    public string ContentType { get; set; } = "text/plain";
    public List<KeyValue> Headers { get; set; } = new List<KeyValue>();
    public ApiFile File { get; set; }
}
```

You can return a response by creating a new object and returning it from your endpoint.

```csharp
return new ApiResponse {
    StatusCode = 401
};
```

You can access the PowerShell Universal service container within your endpoint by accessing the `ServiceProvider` property in your endpoint. We currently do not document the internal services of PowerShell Universal.&#x20;

```csharp
var database = ServiceProvider.GetService(typeof(IDatabase));
```

## OpenTelemetry&#x20;

**Identifier:** `PowerShellUniversal.Plugins.OpenTelemetry`

OpenTelemetry is a collection of APIs, SDKs, and tools. Use it to instrument, generate, collect, and export telemetry data (metrics, logs, and traces) to help you analyze your software’s performance and behavior.

The plugin enables integration with the technology. You can use [App Settings](../config/settings.md) to configure where to send data. PowerShell Universal currently only exposes a single OTLP endpoint configuration. The below configuration would work with Prometheus.

```json
{    
    "OpenTelemetry": {
        "Otlp": {
            "Endpoint": "http://localhost:9090/api/v1/otlp/v1/metrics"
        }
    }
}
```

## YARP&#x20;

**Identifier:** `PowerShellUniversal.Plugins.YARP`

[YARP](https://microsoft.github.io/reverse-proxy/articles/index.html) (Yet Another Reverse Proxy) is a Microsoft project that allows ASP.NET Core applications to act as reverse proxies. PowerShell Universal only exposes this configuration but does not extend it in many regards. You can use [App Settings ](../config/settings.md)to configure the proxy and starting the PSU service will enable the YARP functionality. Follow the [YARP articles](https://microsoft.github.io/reverse-proxy/articles/index.html) to understand how to configure the service.&#x20;

The one extension that we do provide into YARP is the ability to specify a PSU role that is required for a particular proxy route. For example, the following would enforce the Administrator role.&#x20;

```json
{
    "ReverseProxy": {
        "Routes": {
            "route1": {
                "ClusterId": "cluster1",
                "AuthorizationPolicy": "AdministratorRolePolicy",
                "Match": {
                    "Path": "/code/{**catch-all}"
                },
                "Transforms": [
                    {
                        "PathRemovePrefix": "/code"
                    }
                ]
            }
        },
        "Clusters": {
            "cluster1": {
                "Destinations": {
                    "destination1": {
                        "Address": "http://localhost:8080"
                    }
                }
            }
        }
    }
}
```

You can replace the `Administrator` portion of the policy name to enforce a different role. For example: `ExecutorRolePolicy`.&#x20;
