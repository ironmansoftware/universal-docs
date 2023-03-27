---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-PSUEndpoint

## SYNOPSIS

Creates a new REST API endpoint. 

## SYNTAX

### Endpoint
```
New-PSUEndpoint [-Method <String[]>] -Url <String> [-Description <String>] -Endpoint <ScriptBlock>
 [-Authentication] [-Role <String[]>] [-RegEx] [-Tag <Tag[]>] [-Timeout <Int32>] [-Environment <String>]
 [-PersistentLog] [-Documentation <String>] [-ComputerName <String>] [-AppToken <String>]
 [-UseDefaultCredentials] [-Integrated] [<CommonParameters>]
```

### Path
```
New-PSUEndpoint [-Method <String[]>] -Url <String> [-Description <String>] -Path <String> [-Authentication]
 [-Role <String[]>] [-RegEx] [-Tag <Tag[]>] [-Timeout <Int32>] [-Environment <String>] [-PersistentLog]
 [-Documentation <String>] [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials] [-Integrated]
 [<CommonParameters>]
```

## DESCRIPTION
Creates a new REST API endpoint. 

This cmdlet is a configuration cmdlet. You can use it with the PowerShell Universal configuration system as well as the PowerShell Universal Management API. Endpoints are stored within the ./universal/endpoints.ps1 file. 

## EXAMPLES

### Example 1
```
New-PSUEndpoint -Url "/hello" -Method GET -Endpoint {
    "Hello"
}
PS C:\> Invoke-RestMethod http://localhost:5000/hello
```

Creates a REST API endpoint that returns "Hello" when the user calls it via the GET HTTP method. 

### Example 2
```
New-PSUEndpoint -Url "/hello/:variable" -Method GET -Endpoint {
    $Variable
}

PS C:\> Invoke-RestMethod http://localhost:5000/hello/world
```

Creates a REST API that users variables. Variables allow users to pass data to the REST API. They will appear as PowerShell variables within the endpoint script block. 

### Example 3
```
New-PSUEndpoint -Url "/hello/" -Method GET -Endpoint {
    "Hello authenticated user"
} -Authentication -Role 'Administrators'

PS C:\> Invoke-RestMethod http://localhost:5000/hello/world -Headers @{ Authorization = "Bearer appTokenGoesHere" }
```

Creates a REST API that requires authentication and authorization. Only users with a valid AppToken can access this endpoint and only users that hold the Administrators role. 

### Example 4
```
New-PSUEndpoint -Url "/hello/" -Method GET -Endpoint {
    "Hello user"
} -ComputerName http://localhost:5000 -AppToken 'appToken'

PS C:\> Invoke-RestMethod http://localhost:5000/hello/world -Headers @{ Authorization = "Bearer appTokenGoesHere" }
```

Creates a REST API using the PowerShell Universal Management API. When calling the management API, you will need to define the computer name and the app token to successfully call the API.

## PARAMETERS

### -AppToken

The AppToken that is used for calling the PowerShell Universal Management API. You can also call Connect-PSUServer before calling this cmdlet to set the AppToken for the entire session.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Authentication

Specifies whether this endpoint requires authentication. Authentication requires an API license.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -ComputerName

Specifies the computer name or URL that should be called when accessing the PowerShell Universal Management API. You can also use Connect-PSUServer before calling this cmdlet to set the computer name for the entire session. 

```yaml
Type: String
Parameter Sets: (All)
Aliases: Uri

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Endpoint

The contents of the endpoint. This is the PowerShell script that will be called when the REST API is executed. 

```yaml
Type: ScriptBlock
Parameter Sets: Endpoint
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Method

The HTTP methods that are required for calling this endpoint.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases:
Accepted values: GET, POST, PUT, DELETE, OPTIONS

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -RegEx

Specifies whether to process the URL provided as a RegEx string rather than a literal URL.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Role

Specifies the role that is required for accessing this endpoint. The -Authentication parameter should also be specified when using the -Role parameter. Roles require an API license.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Url

The URL of the endpoint. This URL can be a RegEx expression if you specify the -RegEx switch parameter. This URL can also contain variables using the colon (:) prefix. 

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Description
A description for the endpoint to display in the console.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -UseDefaultCredentials
Use default credentials when connecting to the management API

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Integrated
Executes the command internally rather than using the Management API. Only works when running script from within PowerShell Universal. 

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Tag
{{ Fill Tag Description }}

```yaml
Type: Tag[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Timeout
The timeout in seconds for this API endpoint. 0 or not defined means no timeout. 

```yaml
Type: Int32
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path
The path to a PS1 file containing the content of this endpoint.

```yaml
Type: String
Parameter Sets: Path
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Environment
The environment to run this endpoint within. 

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -PersistentLog
Whether to store the log for this endpoint in the database. 

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Documentation
The documentation definition to associate this end with.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### None
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS

[New-PSUApiResponse](New-PSUApiResponse.md)