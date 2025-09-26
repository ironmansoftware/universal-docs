---
description: Endpoint configuration for Universal APIs.
---

# Endpoints

Endpoints are defined by their URI and HTTP method. Calls made to the Universal server that match your defined API endpoint and method execute the API endpoint script.

```powershell
New-PSUEndpoint -Url '/endpoint' -Method 'GET' -Endpoint {
   "Hello, world!"
}
```

To invoke the above method, you can use `Invoke-RestMethod`.

```powershell
Invoke-RestMethod http://localhost:5000/endpoint
```

When defining endpoints in the management API, you can skip the `New-PSUEndpoint` call, as the admin console defines it.

![API Properties](<../.gitbook/assets/image (442).png>)

The only contents that you need to provide in the editor are the script you wish to call.

![API Content](<../.gitbook/assets/image (550).png>)

{% hint style="warning" %}
Avoid using endpoint URLs that match internal PowerShell Universal Management API URLs, as this causes unexpected behavior. You can reference the [OpenAPI documentation](openapi.md#management-api-documentation) for the [Management API](../config/management-api.md) to verify that none of the URLs match.
{% endhint %}

## HTTP Methods

Endpoints can have one or more HTTP methods defined. To determine which method is used by an endpoint, use the built-in `$Method` variable.

```powershell
New-PSUEndpoint -Url '/user' -Method @('GET', 'POST') -Endpoint {
    if ($Method -eq 'GET')
    {
       Get-User
    }
    else {
       New-User
    }
}
```

## Variable URL

URLs can contain variable segments. You can denote a variable segment using a colon (`:`). For example, the following URL would provide a variable for the ID of the user. The `$Id` variable will be defined within the endpoint when it is executed. Variables must be unique in the same endpoint URL.

```powershell
New-PSUEndpoint -Url '/user/:id' -Method 'GET' -Endpoint {
   Get-User -Id $Id
}
```

To call this API and specify the ID, do the following:

```powershell
Invoke-RestMethod http://localhost:5000/user/123
```

## Query String Parameters

Query string parameters are automatically passed into endpoints as variables that you can then access. For example, if you have an endpoint that expects an `$Id` variable, you can provide it in the query string.

```powershell
New-PSUEndpoint -Url '/user' -Method 'GET' -Endpoint {
   Get-User -Id $Id
}
```

The resulting `Invoke-RestMethod` call must then include the query string parameter.

```powershell
Invoke-RestMethod http://localhost:5000/user?Id=123
```

When using multiple query string parameters, ensure that your URL is surrounded by quotes so PowerShell translates it properly. Including an ampersand (&) without quotes will cause issues in both Windows PowerShell and PowerShell 7.

```powershell
Invoke-RestMethod "http://localhost:5000/user?Id=123&name=tim"
```

### Security Considerations

When accepting input via Query String parameters you may be vulnerable to [CWE-914: Improper Control of Dynamically-Identified Variables](https://cwe.mitre.org/data/definitions/914.html). Consider using a `param` block to ensure that only valid parameters are provided to the endpoint.

Below is an example of CWE-914. Include a `$IsChallengePassed` query string parameter to bypass the challenge.

```powershell
New-PSUEndpoint -Url "/api/v1.0/CWE914Test" -Description "Vulnerable to CWE-914" -Endpoint {
	if($ChallengeInputData -eq "AcceptableInput") {
		$IsChallengePassed = $true
	}
	if($IsChallengePassed) {
		"Challenge passed. Here is Sensitive Information"
	} else {
		"Challenge not passed"
	}
}
```

In order to avoid this particular issue, you can use a `param` block.

```powershell
New-PSUEndpoint -Url "/api/v1.0/CWE914Test" -Description "Not Vulnerable to CWE-914" -Endpoint {
	Param(
		$ChallengeInputData
	)
	if($ChallengeInputData -eq "AcceptableInput") {
		$IsChallengePassed = $true
	}
	if($IsChallengePassed) {
		"Challenge passed. Here is Sensitive Information"
	} else {
		"Challenge not passed"
	}
}
```

## Headers

Request headers are available in APIs using the `$Headers` variable. The variable is a hashtable. To access a header, use the following syntax:

```powershell
$Headers['Content-Type']
```

## Cookies

Request cookies are available in APIs using the `$Cookies` variable. The variable is a hashtable. To access a cookie, use the following syntax:

```powershell
$Cookies['Request-Cookie']
```

Send back request cookies with the `New-PSUApiResponse` cmdlet. Use the `-Cookies` parameter with a supplied hashtable.

```powershell
New-PSUApiResponse -StatusCode 200 -Cookies @{
    ResponseCookie = '123'
}
```

## Body

To access a request body, you will simply access the `$Body` variable. Universal `$Body` variable will be a string. If you expect JSON, you should use `ConvertFrom-Json`.

```powershell
New-PSUEndpoint -Url '/user' -Method Post -Endpoint {
    $User = ConvertFrom-Json $Body 
    New-User $User
}
```

To call the above endpoint, specify the body of `Invoke-RestMethod`.

```powershell
Invoke-RestMethod http://localhost:5000/user -Method Post -Body "{'username': 'adam'}"
```

## Live Log

You can view the live log information for any endpoint by clicking the log tab. Live logs include URL, HTTP method, source IP address, PowerShell streams, status code, return Content Type, and HTTP content length.

You can write to the live log from within your endpoints with cmdlets like `Write-Host`.

<figure><img src="../.gitbook/assets/image (67).png" alt=""><figcaption><p>Endpoint Live Log</p></figcaption></figure>

## Testing

You can use the Test tab in the Endpoint editor to test your APIs. Using this Test tool, you can adjust headers, the query string, and body. You can also adjust the Authentication and Authorization for the test.&#x20;

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption><p>Endpoint Test Tab</p></figcaption></figure>

When using the test tab, any changes to the values of the test will result in an updated Code block that you can then use within PowerShell. Click the Code tab to view the test code.&#x20;

```powershell
Invoke-RestMethod -Uri 'http://localhost:5000/test-api?Page=1' -Headers @{'X-Custom-Header' = 'Value';} -Method 'POST'
```

Additionally, tests performed within the tester will be stored for 30 days to allow for retesting without having to reconfigure all the properties. Clicking the Apply button will setup the Test tool with the same properties.&#x20;

<figure><img src="../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption><p>Test History</p></figcaption></figure>

## Form Data

You can pass data to an endpoint as form data. Form data will pass into your endpoint as parameters.

```powershell
New-PSUEndpoint -Url '/user' -Method Post -Endpoint {
    param([Parameter(Mandatory)]$userName, $FirstName, $LastName)
     
    New-User $UserName -FirstName $FirstName -LastName $LastName
}
```

You can then use a hashtable with Invoke-RestMethod to pass form data.

```powershell
Invoke-RestMethod http://localhost:5000/user -Method Post -Body @{ 
    UserName = "adriscoll"
    FirstName = "Adam"
    LastName = "Driscoll"
}
```

## JSON Data

You can pass JSON data to an endpoint and it will automatically bind to a param block.

```powershell
New-PSUEndpoint -Url '/user' -Method Post -Endpoint {
    param([Parameter(Mandatory)]$userName, $FirstName, $LastName)
     
    New-User $UserName -FirstName $FirstName -LastName $LastName
}
```

You can then send JSON data to the endpoint.

```powershell
Invoke-RestMethod http://localhost:5000/user -Method Post -Body (@{ 
    UserName = "adriscoll"
    FirstName = "Adam"
    LastName = "Driscoll"
} | ConvertTo-Json) -ContentType 'application/json'
```

## Param Block

You can use a `param` block within your script to enforce mandatory parameters and provide default values for optional parameters such as query string parameters. Variables such as `$Body`, `$Headers` and `$User` are provided automatically.

In the below example, the `$Name` parameter is mandatory and the `$Role` parameter has a default value of Default.

```powershell
New-PSUEndpoint -Url '/user/:name' -Endpoint {
    param([Parameter(Mandatory)$Name, $Role = "Default")
}
```

When using the `param` block with route parameters like the above example, you must include the route variable in your parameter. If it is not specified, you will not have access to that value.

For example, the following `$Name` variable is always `$null`. The endpoint always returns false.

```powershell
New-PSUEndpoint -Url '/user/:name' -Endpoint {
    param($Role = "Default")
    
    $Name -eq 'Adam'
}
```

If you use the `CmdletBinding` or `Parameter` attribute within your param block, the endpoint will strictly enforce which parameters are allowed into the endpoint.&#x20;

For example, the following enforces that the name parameter is specified.&#x20;

```powershell
New-PSUEndpoint -Url '/user' -Endpoint {
    param([Parameter(Mandatory)$Name)
}
```

That said, you cannot specify additional parameters to the endpoint. Doing the following will cause an error.

```powershell
Invoke-RestMethod http://localhost:5000/user -Method Post -Body (@{ 
    Name = "adriscoll"
    DisplayName = 'Adam'
} | ConvertTo-Json) -ContentType 'application/json'
```

If you change your endpoint to avoid using the `Parameter` attribute, you can pass in any number of params and they will be bound as variables and not parameters to the endpoint.&#x20;

```powershell
New-PSUEndpoint -Url '/user' -Endpoint {
    param($Name)
}
```

## Returning Data

Data returned from endpoints is assumed to be JSON data. If you return an object from the endpoint script block, it is automatically serialized to JSON. If you want to return another type of data, you can return a string formatted however you chose.

## Processing Files

### Uploading Files

You can process uploaded files by using the `$Data` parameter to access the byte array of data uploaded to the endpoint.

```powershell
New-PSUEndpoint -Url '/file' -Method Post -Endpoint {
    $Data
}

PS C:\Users\adamr> iwr http://localhost:5000/file -method post -InFile '.\Desktop\add-dashboard.png'

StatusCode        : 200
StatusDescription : OK
Content           : [137,80,78,71,13,10,26,10,0,0,0,13,73,72,68,82,0,0,2,17,0,0,1,92,8,2,0,0,0,249,210,123,106,0,0,0,1,
                    115,82,71,66,0,174,206,28,233,0,0,0,4,103,65,77,65,0,0,177,143,11,252,97,5,0,0,0,9,112,72,89,115,0,
                    0,…
```

{% hint style="warning" %}
`The multipart/form-data`content type is not supported for uploading files to APIs.
{% endhint %}

You can also save the file into a directory.

```powershell
New-PSUEndpoint -Url '/file' -Method Post -Endpoint {
    [IO.File]::WriteAllBytes("tempfile.dat", $Data)
}
```

### Downloading Files

You can send files down using the `New-PSUApiResponse` cmdlet.

```powershell
New-PSUEndpoint -Url '/image' -Endpoint {
    $ImageData = [IO.File]::ReadAllBytes("image.jpeg")
    New-PSUApiResponse -ContentType 'image/jpg' -Data $ImageData
}
```

## Returning Custom Responses

You can return custom responses from endpoints by using the `New-PSUApiResponse` cmdlet in your endpoint. This cmdlet allows you to set the status code, content type and even specify the byte\[] data for the content to be returned.

```powershell
New-PSUEndpoint -Url '/file' -Method Get -Endpoint {
    New-PSUApiResponse -StatusCode 410
}
```

You can also return custom body data with the `-Body` parameter of `New-PSUApiResponse`.

```powershell
New-PSUEndpoint -Url '/file' -Method Get -Endpoint {
    New-PSUApiResponse -Body "Not what you're looking for." -StatusCode 404
}
```

Invoking the REST method returns the custom error code.

```powershell
PS C:\Users\adamr\Desktop> invoke-restmethod http://localhost:8080/file

Invoke-RestMethod: Not what you're looking for.
```

You can control the content type of the returned data with the `-ContentType` parameter.

```powershell
New-PSUEndpoint -Url '/file' -Method Get -Endpoint {
    New-PSUApiResponse -Body "<xml><node>1</node><node2>2</node2></xml>" -ContentType 'text/xml'
}
```

You can control the response headers with a hashtable of values that you pass to the `-Headers`parameter.

```powershell
New-PSUApiResponse -StatusCode 200 -Headers @{
    "Referrer-Policy" = "no-referrer"
}
```

## Persistent Runspaces

Persistent runspaces allow you to maintain runspace state between API calls. This is important for users that perform some sort of initialization within their endpoints that they do not want to execute on subsequent API calls.

By default, runspaces are reset after each execution. This removes variables, modules and functions defined during the execution of the API.

To enable persistent runspaces, you will need to configure an [environment ](../config/environments.md)for your API. Set the `-PersistentRunspace` parameter to enable this feature. This is configured in the `environments.ps1` script.

```powershell
New-PSUEnvironment -Name 'Env' -Path 'powershell.exe' -PersistentRunspace
```

You can then assign the API environment in the `settings.ps1` script.

```powershell
Set-PSUSetting -ApiEnvironment 'Env'
```

## Timeout

By default, endpoints will not time out. To set a timeout for your endpoints, you can use the `New-PSUEndpoint` `-Timeout` parameter. The timeout is set in the number of seconds.

## External Endpoint Content

You can define the path to an external endpoint content file with the `-Path` parameter of `New-PSUEndpoint`. The path is relative to the `.universal` directory in Repository.

The content of the `endpoints.ps1` file is then this:

```powershell
New-PSUEndpoint -Url "/path" -Path "endpoint-path.ps1"
```

## C# APIs

C# APIs are enabled as a [plugin](../platform/plugins/#c-api-environment).

There is no UI for creating a C# API, so you need to do so using configuration files. First, create a `.cs` file that runs your API.

You will have access to a `request` parameter that includes all the data about the API request.

```csharp
public class ApiRequest
{
    public long Id;
    public ICollection<KeyValue> Variables;
    public IEnumerable<ApiFile> Files { get; set; };
    public string Url;
    public ICollection<KeyValue> Headers;
    public byte[] Data;
    public int ErrorAction;
    public ICollection<KeyValue> Parameters;
    public string Method;
    public ICollection<KeyValue> Cookies;
    public string ClaimsPrincipal;
    public string ContentType;
}
```

You will also have access to a `ServiceProvider` property that allows you to access services within PowerShell Universal. These are not currently well-documented, but below is an example of restarting a dashboard.

```csharp
var dm = ServiceProvider.GetService(typeof(IDashboardManager));
var dashboard = dm.GetDashboard(1);
dm.Restart(dashboard);
```

Some other useful services include:

* IDatabase
* IApiService
* IConfigurationService
* IJobService

You can choose to return an `ApiResponse` from your endpoint.

```powershell
return new ApiResponse {
    StatusCode = 404
};
```

Once you have defined your C# endpoint file, you can add it by editing `endpoints.ps1`.

```powershell
New-PSUEndpoint -Url /csharp -Path endpoint.cs -Environment 'C#'
```

The PowerShell Universal service automatically compiles and runs C# endpoints.

## API

* [New-PSUEndpoint](../cmdlets/New-PSUEndpoint.txt)
* [Get-PSUEndpoint](../cmdlets/Get-PSUEndpoint.txt)
* [Remove-PSUEndpoint](../cmdlets/Remove-PSUEndpoint.txt)
* [New-PSUApiResponse](../cmdlets/New-PSUApiResponse.txt)
* [Set-PSUSetting](../cmdlets/Set-PSUSetting.txt)
