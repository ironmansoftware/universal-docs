---
description: Component for uploading files in Universal Dashboard.
---

# Upload

The UDUpload component is used to upload files to Universal Dashboard. You can process files the user uploads. You will receive the data for the file, a file name and the type of file if it can be determined by the web browser.

This component works with [UDForm](form.md) and [UDStepper](../navigation/stepper.md).

## Uploading a File

Uploads a file and shows the contents via a toast.

```powershell
New-UDUpload -OnUpload {
    Show-UDToast $Body
}
```

The body of the `OnUpload` script block is a JSON string with the following format.

```javascript
{
  data: "base64 encoded string of data",
  name: "file name of the file uploaded",
  type: "file type as determined by the browser"
}
```

The `$EventData` is an object with the following structure.&#x20;

```csharp
public class Upload
{
    public string Name { get; set; }
    public string FileName { get; set; }
    public DateTime TimeStamp { get; set; }
    public string ContentType { get; set; }
    public string Type => ContentType;
}
```

## Uploading a File with a Form

Uploads a file as part of a UDForm.

```powershell
New-UDForm -Content {
    New-UDUpload -Id 'myFile' 
} -OnSubmit {
    Show-UDToast $Body 
}
```

The body of the `OnSubmit` script block is the same one you will see with any form and the file will be contains as one of the fields within the form.

## Example: Uploading a file and save to it the temp directory

This example allows a user to upload a file. Once the file is uploaded, it will be saved to the temporary directory.

```powershell
New-UDUpload -Text 'Upload Image' -OnUpload {
    $Data = $Body | ConvertFrom-Json 
    $bytes = [System.Convert]::FromBase64String($Data.Data)
    [System.IO.File]::WriteAllBytes("$env:temp\$($Data.Name)", $bytes)
}
```

## API

**New-UDUpload**

```markdown
    .SYNOPSIS
    Upload files
    
    .DESCRIPTION
    Upload files. This component works with UDForm and UDStepper.
    
    .PARAMETER Id
    The ID of the uploader.
    
    .PARAMETER Accept
    The type of files to accept. By default, this component accepts all files. 
    
    .PARAMETER OnUpload
    A script block to execute when a file is uploaded. This $body parameter will contain JSON in the following format: 

    {
        data: 'base64 encoded string of file data',
        name: 'filename',
        type: 'type of file, if known'
    }

    $EventData will contain a class with the following properties:

    public string Name { get; set; }
    public string FileName { get; set; }
    public DateTime TimeStamp { get; set; }
    public string ContentType { get; set; }
    public string Type => ContentType;
    
    .PARAMETER Text
    The text to display on the upload button.
    
    .PARAMETER Variant
    The variant of button. Defaults to contained. Valid values: "text", "outlined", "contained"
    
    .PARAMETER Color
    The color of the button. Defaults to 'default'. Valid values: "default", "primary", "secondary", "inherit"

    .PARAMETER ClassName
    A CSS class to apply to the button.

    .EXAMPLE
    A file uploader 

    New-UDDashboard -Title "Hello, World!" -Content {
        New-UDUpload -Text "Upload" -OnUpload {
            Show-UDToast $Body
        }
    }
    
    .EXAMPLE
    A file uploader in a form 

    New-UDDashboard -Title "Hello, World!" -Content {
        New-UDForm -Content {
            New-UDUpload -Text "Upload" 
        } -OnSubmit {
            Show-UDToast $Body
        }
    }
```
