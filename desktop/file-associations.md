---
description: Launch PowerShell scripts based on file associations.
---

# File Associations

![File associations in the admin console. ](<../.gitbook/assets/image (383) (1).png>)

## Define a File Association

File associations are stored within the `fileAssociations.ps1` file within the configuration directory. You can use the `New-PSUFileAssociation` cmdlet to define associations directly.&#x20;

By default, you'll need to include the script to run and the extension to associate with it.&#x20;

```powershell
New-PSUFileAssociation -Script FileAssociation.ps1 -Extension .ps3
```

## Accessing the File Path

By default, you can use the `$File` parameter within your script to access the full path to the file that caused the file association to trigger.

```powershell
param($File)

$Json = Get-Content $File | ConvertFrom-Json 
```
