# About

Universal provides the ability to define REST API endpoints using PowerShell. When the endpoints are executed by a compatible HTTP client, the PowerShell script will execute and return the result to the end user. 

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
Invoke-RestMethod http://localhost:5000?Id=123
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

## Execution Environment 

The REST API execution environment runs in your default PowerShell version. Unlike Automation jobs, which can also be run via the Universal management API, APIs that you define are run in a single PowerShell process. Because the PowerShell process is not started and stopped for each call to the endpoint, the API is much faster. 

### Performance

Performance is relative to the hardware and network conditions that you are running Universal on. That said, in ideal conditions you can expect the Universal APIs to service about 500 requests per second. This is with an entirely empty endpoint so any script that you add to that endpoint will reduce the throughput. The reduction of throughput will depend on the cmdlets and script executed within the API endpoint. 



