# About

Universal provides the ability to define REST API endpoints using PowerShell. When the endpoints are executed by a compatible HTTP client, the PowerShell script will execute and return the result to the end user.

{% hint style="info" %}
This feature is for developing custom APIs run by Universal. It not required for managing Universal. Universal provides a set of management APIs that are included with the platform.
{% endhint %}

{% embed url="https://youtu.be/M6z0iYhmUkQ" caption="" %}

## Endpoints

Endpoints are defined by their URI and HTTP method. Calls made to the Universal server that match the API endpoint and method that you define will execute the API endpoint script.

```text
New-PSUEndpoint -Url '/endpoint' -Method 'GET' -Endpoint {
   "Hello, world!"
}
```

To invoke the above method, you could use `Invoke-RestMethod`.

```text
Invoke-RestMethod http://localhost:5000/endpoint
```

### Authentication and Authorization

{% hint style="info" %}
This feature requires a [license](../licensing.md).
{% endhint %}

REST API authentication requires a Universal API license. Once enabled, you will be able to enforce authentication and authorization on your endpoints. Authentication and authorization for APIs is managed via app tokens. You can manage user app tokens under `Settings \ Security \ AppTokens`.

```text
New-PSUEndpoint -Url '/endpoint' -Method 'GET' -Endpoint {
   "Hello, world!"
} -Authentication -Role 'Administrator'
```

### Variable URL

URLs can contain variable segments. You can denote a variable segment using a colon \(`:`\). For example, the following URL would provide a variable for the ID of the user. The `$Id` variable will be defined within the endpoint when it is executed. Variables must be unique in the same endpoint URL.

```text
New-PSUEndpoint -Url '/user/:id' -Method 'GET' -Endpoint {
   Get-User -Id $Id
}
```

To call this API and specify the ID, you would do the following.

```text
Invoke-RestMethod http://localhost:5000/user/123
```

### Query String Parameters

Query string parameters are automatically passed into endpoints as variables that you can then access. For example, if you had an endpoint that expected an `$Id` variable, it could be provided via the query string.

```text
New-PSUEndpoint -Url '/user' -Method 'GET' -Endpoint {
   Get-User -Id $Id
}
```

The resulting `Invoke-RestMethod` call must then include the query string parameter.

```text
Invoke-RestMethod http://localhost:5000/user?Id=123
```

### Body

To access a request body, you will simply access the `$Body` variable. Universal `$Body` variable will be a string. If you expect JSON, you should use `ConvertFrom-Json`.

```text
New-PSUEndpoint -Url '/user' -Method Post -Endpoint {
    $User = ConvertFrom-Json $Body 
    New-User $User
}
```

To call the above endpoint, you would have to specify the body of `Invoke-RestMethod`.

```text
Invoke-RestMethod http://localhost:5000/user -Method Post -Body "{'username': 'adam'}"
```

### Returning Data

Data returned from endpoints will be assumed to be JSON data. If you return an object from the endpoint script block, it will be automatically serialized to JSON. If you want to return another type of data, you can return a string formatted however you chose.

### Processing Files

#### Uploading Files

You can process uploaded files by using the `$Data` parameter to access the byte array of data uploaded to the endpoint.

```text
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

```text
New-PSUEndpoint -Url '/file' -Method Post -Endpoint {
    [IO.File]::WriteAllBytes("tempfile.dat", $Data)
}
```

#### Downloading Files

You can send files down using the `New-PSUApiResponse` cmdlet.

```text
New-PSUEndpoint -Url '/image' -Endpoint {
    $ImageData = [IO.File]::ReadAllBytes("image.jpeg")
    New-PSUApiResponse -ContentType 'image/jpg' -Data $ImageData
}
```

### Returning Custom Responses

You can return custom responses from endpoints by using the `New-PSUApiResponse` cmdlet in your endpoint. This cmdlet allows you to set the status code, content type and even specify the byte\[\] data for the content to be returned.

```text
New-PSUEndpoint -Url '/file' -Method Get -Endpoint {
    New-PSUApiResponse -StatusCode 410
}
```

### Error Handling

By default, endpoints will return a 200 OK message even if there are non-terminating errors. To change this behavior, you can set the `-ErrorAction` parameter of `New-PSUEndpoint` to `Stop`. Any non-terminating errors will cause an 500 Internal Server Error to be returned with a list of the errors and stack trace.

Terminating errors will always return a 500 Internal Server Error.

```text
New-PSUEndpoint -Url "/user" -Endpoint { 
   $obj = [object]::new()
   $obj.UserName = "test"
} -ErrorAction stop
```

## Execution Environment

The REST API execution environment runs in your default PowerShell version. Unlike Automation jobs, which can also be run via the Universal management API, APIs that you define are run in a single PowerShell process. Because the PowerShell process is not started and stopped for each call to the endpoint, the API is much faster.

### Performance

Performance is relative to the hardware and network conditions that you are running Universal on. That said, in ideal conditions you can expect the Universal APIs to service about 500 requests per second. This is with an entirely empty endpoint so any script that you add to that endpoint will reduce the throughput. The reduction of throughput will depend on the cmdlets and script executed within the API endpoint.

### Variables

There are a set of predefined variables that are available in API endpoints. You'll be able to use these variables in your scripts.

| Variable | Description | Type |
| :--- | :--- | :--- |
| $Url | URL the client used to call the endpoint | String |
| $Headers | Headers provided by the client to call the endpoint | Hashtable |
| $Body | The UTF8 encoded string of the content of the request | String |
| $Data | Binary byte array for the content of the request | Byte\[\] |
| $RemoteIpAddress | The remote IP address used to make the request. | String |
| $LocalIpAddress | The local IP address used to service the request. | String |
| $RemotePort | The remote port that was called to make the request. | Integer |
| $LocalPort | The local port that was used to service the request. | Integer |
| $Identity | The identity name of the principal accessing the API. | String |

