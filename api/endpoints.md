---
description: Endpoint configuration for Universal APIs.
---

# Endpoints

Endpoints are defined by their URI and HTTP method. Calls made to the Universal server that match the API endpoint and method that you define will execute the API endpoint script.

```
New-PSUEndpoint -Url '/endpoint' -Method 'GET' -Endpoint {
   "Hello, world!"
}
```

To invoke the above method, you could use `Invoke-RestMethod`.

```
Invoke-RestMethod http://localhost:5000/endpoint
```

When defining endpoints in the management API, you can skip the `New-PSUEndpoint` call as it will be defined by the admin console.&#x20;

![](<../.gitbook/assets/image (302) (1) (1).png>)

The only contents that you need to provide in the editor will be the script you wish to call.&#x20;

![](<../.gitbook/assets/image (303) (1).png>)

## Variable URL

URLs can contain variable segments. You can denote a variable segment using a colon (`:`). For example, the following URL would provide a variable for the ID of the user. The `$Id` variable will be defined within the endpoint when it is executed. Variables must be unique in the same endpoint URL.



```
New-PSUEndpoint -Url '/user/:id' -Method 'GET' -Endpoint {
   Get-User -Id $Id
}
```

To call this API and specify the ID, you would do the following.

```
Invoke-RestMethod http://localhost:5000/user/123
```

## Query String Parameters

Query string parameters are automatically passed into endpoints as variables that you can then access. For example, if you had an endpoint that expected an `$Id` variable, it could be provided via the query string.

```
New-PSUEndpoint -Url '/user' -Method 'GET' -Endpoint {
   Get-User -Id $Id
}
```

The resulting `Invoke-RestMethod` call must then include the query string parameter.

```
Invoke-RestMethod http://localhost:5000/user?Id=123
```

## Body

To access a request body, you will simply access the `$Body` variable. Universal `$Body` variable will be a string. If you expect JSON, you should use `ConvertFrom-Json`.

```
New-PSUEndpoint -Url '/user' -Method Post -Endpoint {
    $User = ConvertFrom-Json $Body 
    New-User $User
}
```

To call the above endpoint, you would have to specify the body of `Invoke-RestMethod`.

```
Invoke-RestMethod http://localhost:5000/user -Method Post -Body "{'username': 'adam'}"
```

## Form Data

You can pass data to an endpoint as form data. Form data will be passed into your endpoint as parameters.&#x20;

```
New-PSUEndpoint -Url '/user' -Method Post -Endpoint {
    param([Parameter(Mandatory)]$userName, $FirstName, $LastName)
     
    New-User $UserName -FirstName $FirstName -LastName $LastName
}
```

You can then use a hashtable with Invoke-RestMethod to pass form data.&#x20;

```
Invoke-RestMethod http://localhost:5000/user -Method Post -Body @{ 
    UserName = "adriscoll"
    FirstName = "Adam"
    LastName = "Driscoll"
}
```

## Param Block

You can use a `param` block within your script to enforce mandatory parameters and provide default values for optional parameters such as query string parameters. Variables such as `$Body`, `$Headers` and `$User` are provided automatically.

In the below example, the `$Name` parameter is mandatory and the `$Role` parameter has a default value of Default.

```
New-PSUEndpoint -Url '/user/:name' -Endpoint {
    param([Parameter(Mandatory)$Name, $Role = "Default")
}
```

## Returning Data

Data returned from endpoints will be assumed to be JSON data. If you return an object from the endpoint script block, it will be automatically serialized to JSON. If you want to return another type of data, you can return a string formatted however you chose.

## Processing Files

### Uploading Files

You can process uploaded files by using the `$Data` parameter to access the byte array of data uploaded to the endpoint.

```
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

You could also save the file into a directory.

```
New-PSUEndpoint -Url '/file' -Method Post -Endpoint {
    [IO.File]::WriteAllBytes("tempfile.dat", $Data)
}
```

### Downloading Files

You can send files down using the `New-PSUApiResponse` cmdlet.

```
New-PSUEndpoint -Url '/image' -Endpoint {
    $ImageData = [IO.File]::ReadAllBytes("image.jpeg")
    New-PSUApiResponse -ContentType 'image/jpg' -Data $ImageData
}
```

## Returning Custom Responses

You can return custom responses from endpoints by using the `New-PSUApiResponse` cmdlet in your endpoint. This cmdlet allows you to set the status code, content type and even specify the byte\[] data for the content to be returned.

```
New-PSUEndpoint -Url '/file' -Method Get -Endpoint {
    New-PSUApiResponse -StatusCode 410
}
```

You can also return custom body data by using the `-Body` parameter of `New-PSUApiResponse`.

```
New-PSUEndpoint -Url '/file' -Method Get -Endpoint {
    New-PSUApiResponse -Body "Not what you're looking for." -StatusCode 404
}
```

Invoking the REST method will return the custom error code.

```
PS C:\Users\adamr\Desktop> invoke-restmethod http://localhost:8080/file

Invoke-RestMethod: Not what you're looking for.
```

You can control the content type of the data that is returned by using the `-ContentType` parameter.

```
New-PSUEndpoint -Url '/file' -Method Get -Endpoint {
    New-PSUApiResponse -Body "<xml><node>1</node><node2>2</node2></xml>" -ContentType 'text/xml'
}
```

## Persistent Runspaces

Persistent runspaces allow you to maintain runspace state between API calls. This is important for users that perform some sort of initialization within their endpoints that they do not want to execute on subsequent API calls.

By default, runspaces will be reset after each execution. This will cause variables, modules and functions defined during the execution of the API to be removed.

To enable persistent runspaces, you will need to configure an [environment ](../config/environments.md)for your API. Set the `-PersistentRunspace` parameter to enable this feature. This is configured in the `environments.ps1` script.

```
New-PSUEnvironment -Name 'Env' -Path 'powershell.exe' -PersistentRunspace
```

You can then assign the API environment in the `settings.ps1` script.

```
Set-PSUSetting -ApiEnvironment 'Env'
```

## Related Cmdlets

* [New-PSUEndpoint](../cmdlets/Universal/New-PSUEndpoint.md)
* [Get-PSUEndpoint](../cmdlets/Universal/Get-PSUEndpoint.md)
* [Remove-PSUEndpoint](../cmdlets/Universal/Remove-PSUEndpoint.md)
* [New-PSUApiResponse](../cmdlets/Universal/New-PSUApiResponse.md)
* [Set-UASetting](../cmdlets/Universal/Set-UASetting.md)
