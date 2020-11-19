---
external help file: Universal-help.xml
Module Name: Universal
online version:
schema: 2.0.0
---

# Start-PSUServer

## SYNOPSIS
Starts the PowerShell Universal server. 

## SYNTAX

```
Start-PSUServer [[-ExecutablePath] <String>] [[-ListenAddress] <String>] [-Port <Int32>]
 [-Configuration <ScriptBlock>] [<CommonParameters>]
```

## DESCRIPTION
Starts the PowerShell Universal server. This cmdlet performs discovery and configuration of the Universal.Server executable. It uses Start-Process to start up the server after the configuration has been completed. This cmdlet requires that it can find the Universal.Server executable. You can use Install-PSUServer to download the proper binaries for your system. 

## EXAMPLES

### Example 1
```
PS C:\> Start-PSUServer -Port 8080
```

Starts a PowerShell Universal server on port 8080

### Example 2
```
PS C:\> Start-PSUServer -Port 8080 -Configuration {
    New-PSUEndpoint -Url '/test' -Method 'GET' -Endpoint {
        "Hi"
    }
}
```

Starts a PowerShell Universal server on port 8080 and uses single-file configuration to setup a new endpoint listening on '/test'

### Example 3
```
PS C:\> $Env:Data__RepositoryPath = "C:\repo" 
PS C:\> Start-PSUServer -Port 8080 
```

Sets an alternative repository path and starts the PowerShell Universal server. 

## PARAMETERS

### -ExecutablePath
The path to the Universal.Server executable. This defaults to $Env:ProgramData\Universal.Server. If not found in this location, Start-PSUServer will also search the $ENV:PATH

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ListenAddress
The address to listen on. For example: http://*:4000

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Configuration
A configuration script block. This enables single-file configuration. 

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Port
A port to listen on. 

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### None
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS

[Install-PSUServer](Install-PSUServer.md)