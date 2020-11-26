---
description: Image Processing examples
---

# Image Processing

## Convert JPEG to PNG

This example uses [PowerShell Universal Dashboard](../dashboard/about.md). 

This examples accepts a JPEG file and converts to to a PNG using Universal Dashboard. To implement this example, we need to use published folders and a dashboard that uses UDForm and the UDUpload component. After converting the image, it displays it. 

```text
Start-PSUServer -Port 8080 -Configuration {
    New-PSUPublishedFolder -Path 'C:\images' -RequestPath '/images'

    New-PSUDashboard -Name 'Convert' -BaseUrl '/' -Framework 'UniversalDashboard:Latest' -Content {
        New-UDDashboard -Title 'Convert' -Content {
            New-UDForm -Content {
                New-UDUpload -Id 'image' -Text 'Image to Convert'
            } -OnSubmit {
                $bytes = [System.Convert]::FromBase64String($EventData.image.Data)
                [System.IO.File]::WriteAllBytes("C:\$($EventData.Image.Name)", $bytes)

                $Bitmap = [System.Drawing.Image]::FromStream([System.IO.MemoryStream]::new($bytes))
                $Bitmap.Save("C:\images\$($EventData.Image.Name)".Replace("jpeg", "png"), 'PNG')

                New-UDImage -Url "/images/$($EventData.Image.Name.Replace('jpeg', 'png'))"
            }
        }
    }

}
```

![](../.gitbook/assets/convert.gif)

