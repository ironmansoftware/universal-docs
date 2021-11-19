---
description: Error handling for Universal API.
---

# Error Handling

By default, endpoints will return a 200 OK message even if there are errors. If an error occurs, you will get a blank response from the endpoint. This document demonstrates different ways to handle errors within APIs.

## Automatically Returning Errors

To automatically return errors from APIs, you can change the default behavior by setting the `-ErrorAction` parameter of `New-PSUEndpoint` to `Stop`. Any errors will cause an 500 Internal Server Error to be returned with a list of the errors and stack trace.

Terminating errors will always return a 500 Internal Server Error.

```powershell
New-PSUEndpoint -Url "/error" -Endpoint { 
   throw "Uh oh!"
} -ErrorAction stop

New-PSUEndpoint -Url /error2 -Endpoint {
    Write-Error "Whoa!"
} -ErrorAction Stop
```

You will notice different behavior in Windows PowerShell and PowerShell 7 when calling REST APIs that return errors. In Windows PowerShell, you will receive a generic error that doesn't return the error message.

```powershell
PS C:\Users\adamr> invoke-restmethod http://localhost:5000/error2
invoke-restmethod : The remote server returned an error: (500) Internal Server Error.
At line:1 char:1
+ invoke-restmethod http://localhost:5000/error2
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (System.Net.HttpWebRequest:HttpWebRequest) [Invoke-RestMethod], Web
   Exception
    + FullyQualifiedErrorId : WebCmdletWebResponseException,Microsoft.PowerShell.Commands.InvokeRestMethodCommand
```

In PowerShell 7, when an error is returned, you will see the error message returned.

```powershell
PS C:\Users\adamr\Desktop> invoke-restmethod http://localhost:5000/error 

Invoke-RestMethod: Uh oh!
at , : line 2
at , : line 1

PS C:\Users\adamr\Desktop> invoke-restmethod http://localhost:5000/error2

Invoke-RestMethod: Whoa
at , : line 2
at , : line 1
```

You can retrieve the error message in Windows PowerShell, by using the following syntax.

```powershell
PS C:\Users\adamr> try { invoke-restmethod http://localhost:5000/error2 } catch { [System.IO.StreamReader]::new($_.Exception.Response.GetResponseStream()).ReadToEnd()}
Whoa!
at <ScriptBlock>, <No file>: line 2
at <ScriptBlock>, <No file>: line 1
```

## Manually Returning Errors

To manually return errors, you need to use the `New-PSUApiResponse` cmdlet. This cmdlet allows you to define the status code and body for the response.

In this example, we are returning a 404 error code from the endpoint.

```powershell
New-PSUEndpoint -Url /broken -Endpoint {
    New-PSUApiResponse -StatusCode 404 -Body 'Failed!'
}
```

Similar to the automatic error codes, error codes returned manually will as display better in PowerShell 7. Here's an example of calling the endpoint.

```powershell
PS C:\Users\adamr\Desktop> invoke-restmethod http://localhost:5000/broken

Invoke-RestMethod: Failed!
```

If called from Windows PowerShell, you will receive an error similar to the one returned automatically.

```powershell
PS C:\Users\adamr> invoke-restmethod http://localhost:5000/broken
invoke-restmethod : The remote server returned an error: (404) Not Found.
At line:1 char:1
+ invoke-restmethod http://localhost:5000/broken
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (System.Net.HttpWebRequest:HttpWebRequest) [Invoke-RestMethod], Web
   Exception
    + FullyQualifiedErrorId : WebCmdletWebResponseException,Microsoft.PowerShell.Commands.InvokeRestMethodCommand
```

You can choose to return error codes if certain conditions are met by using your PowerShell script within the endpoint.

```powershell
New-PSUEndpoint -Url /user/:name -Endpoint {
    if ($Name -eq 'User')
    {
        @{ UserName = "Adam" }
    }
    else
    {
        New-PSUApiResponse -StatusCode 404 -Body 'Unknown user!'    
    }

}
```

## API

* [New-PSUEndpoint](../cmdlets/New-PSUEndpoint.txt)
* [Get-PSUEndpoint](../cmdlets/Get-PSUEndpoint.txt)
* [Remove-PSUEndpoint](../cmdlets/Remove-PSUEndpoint.txt)
* [New-PSUApiResponse](../cmdlets/New-PSUApiResponse.txt)
* [Set-PSUSetting](../cmdlets/Set-PSUSetting.txt)
