---
description: This plugin enables C# support for API endpoints.
---

# C# API Endpoints

**Identifier:** `PowerShellUniversal.Language.CSharp`

This plugin creates a C#-based environment that can be used to create API endpoints with C# code. APIs created with C# are much faster than PowerShell-based endpoints. Endpoints run directly in the PowerShell Universal service. Any exception thrown from your endpoint will be handled and a valid status code will be returned to the caller.

You must create endpoints with the -Path parameter and specify the `C#` environment for the endpoint to function properly.

```powershell
New-PSUEndpoint -Url /csharp -Path csharp.cs -Environment 'C#'
```

**Defining an Endpoint**

Within the C# endpoint, there are two classes that are of interest. The first is the `request` variable that is passed to the endpoint. It is an `ApiRequest` object.

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

In your endpoint, you can access this variable automatically.

```csharp
if (request.ContentType == "application/json")
{
     // Do some stuff with JSON
}
```

The endpoint must return an `ApiResponse` object. This object has the following definition.

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

When defining an endpoint's content, understand that the code is being added to a dynamically named class with a single Execute function. Your code should be valid syntax for such a source file.

```csharp
using PowerShellUniversal;

public class c{id} : ExecutionClass {{ 
    public static ApiResponse Execute(ApiRequest request) 
    {{ 
        {fileContents} 

        return new ApiResponse();
    }} 
}}";
```

You can access the PowerShell Universal service container within your endpoint by accessing the `ServiceProvider` property in your endpoint. We currently do not document the internal services of PowerShell Universal.

```csharp
var database = ServiceProvider.GetService(typeof(IDatabase));
```

### References

You can control which assemblies are referenced by using the `#ref` keyword. The value can be a DLL file in the PowerShell Universal installation directory, or the full path to another assembly.&#x20;

```csharp
#ref PowerShellUniversal.Apis.dll
#ref C:\assemblies\markdiag.dll
```

### Namespace Using

You can reference a namespace using the `#using` keyword.&#x20;

```csharp
#using System.Management.Automation
```

### Variables

You can access variables in C# endpoints with `GetVariable`, `GetSecretString`, and `GetSecretCredential` methods.

```csharp
return new ApiResponse {
    StatusCode = 200
    Body = GetVariable("MyVar").ToString()
};
```

To access a `PSCredential`, you can do the following.&#x20;

```csharp
#ref System  
#ref System.Management.Automation

return new ApiResponse { 
    StatusCode = 200, 
    Body = GetSecretCredential("MyCred").UserName.ToString() 
};
```
