---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-PSULoginPage

## SYNOPSIS

Configuration settings for the login page in PowerShell Universal.

## SYNTAX

```
New-PSULoginPage [-Image <String>] [-Title <String>] [-PrimaryColor <String>] [-SecondaryColor <String>]
 [-PrimaryFontColor <String>] [-SecondaryFontColor <String>] [-HeaderColor <String>]
 [-HeaderFontColor <String>] [-Copyright <String>] [-ComputerName <String>] [-AppToken <String>]
 [<CommonParameters>]
```

## DESCRIPTION

Configuration settings for the login page in PowerShell Universal. The login page is displayed when using forms authentication. You can configure colors, text and images for the login page. 

Login page configurations are stored in .universal/loginPage.ps1

You can also use this cmdlet to update the login page through the REST API.

## EXAMPLES

### Example 1
```powershell
$LoginPage = @{
 PrimaryColor = '#5c2751' 
 Title = 'DBATools Web Portal'
 Copyright = 'DBATools 2020' 
 HeaderFontColor = 'white'
 HeaderColor = '#4bc0d9' 
 SecondaryColor = '#6457a6'
 SecondaryFontColor = 'white'
 Image = 'http://localhost:5000/images/dbatools.png'
}

New-PSULoginPage @LoginPage
```

Creates a custom login page with colors, images and text.

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

### -ComputerName
Specifies the computer name or URL that should be called when accessing the PowerShell Universal Management API. You can also use Connect-PSUServer before calling this cmdlet to set the computer name for the entire session. 

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

### -Copyright
The copyright text to display at the bottom of the page.

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

### -HeaderColor
The background color of the header.

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

### -HeaderFontColor
The font color of the header.

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

### -Image
An image to display within the login page. You can use published folders to host images. 

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

### -PrimaryColor
The primary background color.

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

### -PrimaryFontColor
The primary font color.

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

### -SecondaryColor
The secondary background color.

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

### -SecondaryFontColor
The secondary font color.

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

### -Title
The tile to display in the header.

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
[New-PSUPublishedFolder](New-PSUPublishedFolder)