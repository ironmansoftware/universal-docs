---
description: Endpoint configuration for Universal APIs.
---

# Endpoints

Endpoints are defined by their URI and HTTP method. Calls made to the Universal server that match the API endpoint and method that you define will execute the API endpoint script.

```powershell
New-PSUEndpoint -Url '/endpoint' -Method 'GET' -Endpoint {
   "Hello, world!"
}
```

To invoke the above method, you could use `Invoke-RestMethod`.

```powershell
Invoke-RestMethod http://localhost:5000/endpoint
```

When defining endpoints in the management API, you can skip the `New-PSUEndpoint` call as it will be defined by the admin console.&#x20;

![API Properties](<../.gitbook/assets/image (442).png>)

The only contents that you need to provide in the editor will be the script you wish to call.&#x20;

![API Content](<../.gitbook/assets/image (550).png>)

## Variable URL

URLs can contain variable segments. You can denote a variable segment using a colon (`:`). For example, the following URL would provide a variable for the ID of the user. The `$Id` variable will be defined within the endpoint when it is executed. Variables must be unique in the same endpoint URL.



```powershell
New-PSUEndpoint -Url '/user/:id' -Method 'GET' -Endpoint {
   Get-User -Id $Id
}
```

To call this API and specify the ID, you would do the following.

```powershell
Invoke-RestMethod http://localhost:5000/user/123
```

## Query String Parameters

Query string parameters are automatically passed into endpoints as variables that you can then access. For example, if you had an endpoint that expected an `$Id` variable, it could be provided via the query string.

```powershell
New-PSUEndpoint -Url '/user' -Method 'GET' -Endpoint {
   Get-User -Id $Id
}
```

The resulting `Invoke-RestMethod` call must then include the query string parameter.

```powershell
Invoke-RestMethod http://localhost:5000/user?Id=123
```

### Security Considerations

When accepting input via Query String parameters you may be vulnerable to [CWE-914: Improper Control of Dynamically-Identified Variables](https://cwe.mitre.org/data/definitions/914.html). Consider using a `param` block to ensure that only valid parameters are provided to the endpoint.&#x20;

Below is an example of CWE-914. A `$IsChallengePassed` query string parameter could be included to bypass the challenge.&#x20;

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

In order to avoid this particular issue, you can use a `param` block.&#x20;

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

Request headers are available in APIs using the `$Headers` variable. The variable is a hashtable. To access a header, use the following syntax.&#x20;

```powershell
$Headers['Content-Type']
```

## Cookies

Request cookies are availablein APIs using the `$Cookies` variable. The variable is a hashtable. To access a cookie, use the following syntax.&#x20;

```powershell
$Cookies['Request-Cookie']
```

Request cookies can be sent back using the `New-PSUApiResponse` cmdlet. Use the `-Cookies` parameter with a supplied hashtable.&#x20;

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

To call the above endpoint, you would have to specify the body of `Invoke-RestMethod`.

```powershell
Invoke-RestMethod http://localhost:5000/user -Method Post -Body "{'username': 'adam'}"
```

## Live Log

You can view the live log information for any endpoint by clicking the log tab. Live logs include URL, HTTP method, source IP address, PowerShell streams, status code, return Content Type and HTTP content length.&#x20;

![](<../.gitbook/assets/image (407).png>)

## Form Data

You can pass data to an endpoint as form data. Form data will be passed into your endpoint as parameters.&#x20;

```powershell
New-PSUEndpoint -Url '/user' -Method Post -Endpoint {
    param([Parameter(Mandatory)]$userName, $FirstName, $LastName)
     
    New-User $UserName -FirstName $FirstName -LastName $LastName
}
```

You can then use a hashtable with Invoke-RestMethod to pass form data.&#x20;

```powershell
Invoke-RestMethod http://localhost:5000/user -Method Post -Body @{ 
    UserName = "adriscoll"
    FirstName = "Adam"
    LastName = "Driscoll"
}
```

## JSON Data

You can pass JSON data to an endpoint and it will automatically bind to a param block.&#x20;

```powershell
New-PSUEndpoint -Url '/user' -Method Post -Endpoint {
    param([Parameter(Mandatory)]$userName, $FirstName, $LastName)
     
    New-User $UserName -FirstName $FirstName -LastName $LastName
}
```

You can then send JSON data to the endpoint.&#x20;

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

## Returning Data

Data returned from endpoints will be assumed to be JSON data. If you return an object from the endpoint script block, it will be automatically serialized to JSON. If you want to return another type of data, you can return a string formatted however you chose.

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
`The multipart/form-data`content type is not supported for uploading files to APIs.&#x20;
{% endhint %}

You could also save the file into a directory.

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

You can also return custom body data by using the `-Body` parameter of `New-PSUApiResponse`.

```powershell
New-PSUEndpoint -Url '/file' -Method Get -Endpoint {
    New-PSUApiResponse -Body "Not what you're looking for." -StatusCode 404
}
```

Invoking the REST method will return the custom error code.

```powershell
PS C:\Users\adamr\Desktop> invoke-restmethod http://localhost:8080/file

Invoke-RestMethod: Not what you're looking for.
```

You can control the content type of the data that is returned by using the `-ContentType` parameter.

```powershell
New-PSUEndpoint -Url '/file' -Method Get -Endpoint {
    New-PSUApiResponse -Body "<xml><node>1</node><node2>2</node2></xml>" -ContentType 'text/xml'
}
```

## Documenting APIs

API documentation can be produced for your endpoints by creating a new OpenAPI definition and assigning endpoints to it. To create an OpenAPI definition, click APIs \ Documentation and then Create new Endpoint Documentation. You can set the name, URL, description and authentication details for the documentation.&#x20;

<figure><img src="../.gitbook/assets/image (233).png" alt=""><figcaption><p>Endpoint Documentation</p></figcaption></figure>

Once created, you can assign endpoints to the documentation by editing the endpoint.&#x20;

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption><p>Edit Endpoint</p></figcaption></figure>

The documentation for your endpoint will appear within the Swagger dashboard. Select the definition with the Select a definition dropdown.&#x20;

<figure><img src="../.gitbook/assets/image (146).png" alt=""><figcaption></figcaption></figure>

All your custom endpoints will be listed.

![Swagger Documentation for APIs](<../.gitbook/assets/image (22).png>)

### Help Text

You can specify help text for your APIs using comment-based help. Including a synopsis, description and parameter descriptions will result in each of those pieces being documented in the OpenAPI documentation and Swagger age.&#x20;

For example, with a simple `/get/:id` endpoint, we could have comment-based help such as this.&#x20;

```powershell
<# 
.SYNOPSIS
This is an endpoint

.DESCRIPTION
This is a description

.PARAMETER ID
This is an ID.

#>
param($ID)
    
$Id
```

The resulting Swagger page will show each of these descriptions.&#x20;

![Swagger Documentation for an API](<../.gitbook/assets/image (347).png>)

### Input and Output Types

Types can be defined within an endpoint documentation scriptblock. Click the Edit Details button on the API documentation record.&#x20;

<figure><img src="../.gitbook/assets/image (231).png" alt=""><figcaption><p>Edit Details for API Documentation</p></figcaption></figure>

APIs can also be documented using input and output types by creating a PowerShell class and referencing it within your comment-based help. PowerShell Universal takes advantage of the `.INPUTS` and `.OUTPUTS` sections to specify accepted formats and define status code return values.&#x20;

Within the `.INPUTS` and `.OUTPUTS` , you will define a YAML block to provide this information. You can create types in the read-only section of the PowerShell Universal configuration file.&#x20;

```powershell
#region PSUHeader 

[Documentation()]
class MyReturnType {
    [string]$Value
}

#endregion
New-PSUEndpoint -Url "/documented" -Method @('GET') -Endpoint {
<# 
.SYNOPSIS
This is an endpoint
    
.DESCRIPTION
This is a description

.PARAMETER Id
This is an ID.

.PARAMETER AnotherOne
This is AnotherOne

.OUTPUTS
    200:
        Description: This is an output value. 
        Content:
            application/json: MyReturnType

    400:
        Description: Invalid input
.INPUTS 
    Required: false
    Description: This is an input value.
    Content: 
        application/json: MyReturnType

#>
param($Id, $AnotherOne)
} -Authentication
```

## Persistent Runspaces

Persistent runspaces allow you to maintain runspace state between API calls. This is important for users that perform some sort of initialization within their endpoints that they do not want to execute on subsequent API calls.

By default, runspaces will be reset after each execution. This will cause variables, modules and functions defined during the execution of the API to be removed.

To enable persistent runspaces, you will need to configure an [environment ](../config/environments.md)for your API. Set the `-PersistentRunspace` parameter to enable this feature. This is configured in the `environments.ps1` script.

```powershell
New-PSUEnvironment -Name 'Env' -Path 'powershell.exe' -PersistentRunspace
```

You can then assign the API environment in the `settings.ps1` script.

```powershell
Set-PSUSetting -ApiEnvironment 'Env'
```

## Timeout&#x20;

By default, endpoints will not time out. To set a timeout for your endpoints, you can use the `New-PSUEndpoint` `-Timeout` parameter. The timeout is set in the number of seconds.&#x20;

## External Endpoint Content

You can define the path to an external endpoint content file by using the `-Path` parameter of `New-PSUEndpoint`. The path is relative to the `.universal` directory in Repository.&#x20;

The content of the `endpoints.ps1` file is then this.&#x20;

```powershell
New-PSUEndpoint -Url "/path" -Path "endpoint-path.ps1"
```

## Experimental Feature: C# APIs

As for PowerShell Universal 3.5, you can now enable C# APIs as an experimental feature. To learn more about enabling experimental features, [click here](../config/feature-flags.md). C# APIs are significantly faster than PowerShell APIs (5 - 20 times faster).

There is no UI for creating a C# API and you will need to do so using configuration files. First, you will need to create a `.cs` file that will run your API.&#x20;

You will have access to a `request` parameter that includes all the data about the API request.&#x20;

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

You will also have access to a `ServiceProvider` property that will allow you to access services within PowerShell Universal. These are currently not well documented but below is an example of restarting a dashboard.&#x20;

```csharp
var dm = ServiceProvider.GetService(typeof(IDashboardManager));
var dashboard = dm.GetDashboard(1);
dm.Restart(dashboard);
```

Some other useful services may include:

* IDatabase
* IApiService
* IConfigurationService
* IJobService

You can choose to return an `ApiResponse` from your endpoint.&#x20;

```powershell
return new ApiResponse {
    StatusCode = 404
};
```

Once you have defined your C# endpoint file, you can add it by editing `endpoints.ps1`.&#x20;

```powershell
New-PSUEndpoint -Url /csharp -Path endpoint.cs -Environment 'C#'
```

C# endpoints are compiled and run directly in the PowerShell Universal service.&#x20;

## API

* [New-PSUEndpoint](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSUEndpoint.txt)
* [Get-PSUEndpoint](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Get-PSUEndpoint.txt)
* [Remove-PSUEndpoint](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Remove-PSUEndpoint.txt)
* [New-PSUApiResponse](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSUApiResponse.txt)
* [Set-PSUSetting](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Set-PSUSetting.txt)
