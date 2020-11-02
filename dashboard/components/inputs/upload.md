---
description: Component for uploading files in Universal Dashboard.
---

# Upload

The UDUpload component is used to upload files to Universal Dashboard. You can process files the user uploads. You will receive the data for the file, a file name and the type of file if it can be determined by the web browser. 

This component works with [UDForm](form.md) and [UDStepper](../navigation/stepper.md). 

## Uploading a File

Uploads a file and shows the contents via a toast. 

```text
New-UDUpload -OnUpload {
    Show-UDToast $Body
}
```

The body of the `OnUpload` script block is a JSON string with the following format. 

```text
{
  data: 'base64 encoded string of data',
  name: 'file name of the file uploaded',
  type: 'file type as determined by the browser'
}
```

## Uploading a File with a Form 

Uploads a file as part of a UDForm. 

```text
New-UDForm -Content {
    New-UDUpload -Id 'myFile' 
} -OnSubmit {
    Show-UDToast $Body 
}
```

The body of the `OnSubmit` script block is the same one you will see with any form and the file will be contains as one of the fields within the form. 

## Example: Uploading a file and save to it the temp directory

This example allows a user to upload a file. Once the file is uploaded, it will be saved to the temporary directory.

```text
New-UDUpload -Id 'myFile' -Text 'Upload Image' -OnUpload {
    $Data = $Body | ConvertFrom-Json 
    $bytes = [System.Convert]::FromBase64String($Data.context.myfile.data)
    [System.IO.File]::WriteAllBytes("$env:temp\$($Data.context.myfile.name)", $bytes)
}
```



**New-UDUpload**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| Accept | String | The type of files to accept. By default, this component accepts all files. | false |
| OnUpload | Endpoint | A script block to call when the file is uploaded.  | false |
| Text | String | The text to display in the upload button.  | false |
| Variant | String | The type of button to show for the upload button.  | false |
| Color | String | The color to use for the upload button. | false |

