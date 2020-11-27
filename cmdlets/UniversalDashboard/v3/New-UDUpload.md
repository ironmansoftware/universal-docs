---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDUpload

## SYNOPSIS
Upload files

## SYNTAX

```
New-UDUpload [[-Id] <String>] [[-Accept] <String>] [[-OnUpload] <Endpoint>] [[-Text] <String>]
 [[-Variant] <String>] [[-Color] <String>] [<CommonParameters>]
```

## DESCRIPTION
Upload files.
This component works with UDForm and UDStepper.

## EXAMPLES

### EXAMPLE 1
```
A file uploader
```

New-UDDashboard -Title "Hello, World!" -Content {
    New-UDUpload -Text "Upload" -OnUpload {
        Show-UDToast $Body
    }
}

### EXAMPLE 2
```
A file uploader in a form
```

New-UDDashboard -Title "Hello, World!" -Content {
    New-UDForm -Content {
        New-UDUpload -Text "Upload" 
    } -OnSubmit {
        Show-UDToast $Body
    }
}

## PARAMETERS

### -Id
The ID of the uploader.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: [Guid]::NewGuid()
Accept pipeline input: False
Accept wildcard characters: False
```

### -Accept
The type of files to accept.
By default, this component accepts all files.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 2
Default value: *
Accept pipeline input: False
Accept wildcard characters: False
```

### -OnUpload
A script block to execute when a file is uploaded.
This $body parameter will contain JSON in the following format: 

{
    data: 'base64 encoded string of file data',
    name: 'filename',
    type: 'type of file, if known'
}

```yaml
Type: Endpoint
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Text
The text to display on the upload button.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 4
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Variant
The variant of button

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 5
Default value: Contained
Accept pipeline input: False
Accept wildcard characters: False
```

### -Color
The color of the button.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 6
Default value: Primary
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
