---
description: >-
  This sample shows how to generate data with Export-CSV and send it to the user
  via a download.
---

# Export-CSV Download

```powershell
New-UDButton -Text 'Generate Report' -OnClick {
    $TempFile = New-TemporaryFile
    Get-Process | Select-Object -First 5 | Export-CSV -Path $TempFile
    $Csv = Get-Content -Path $TempFile -Raw 
    Remove-Item $TempFile
    Start-UDDownload -StringData $Csv -FileName 'processes.csv' -ContentType 'text/csv'
} -ShowLoading
```

This sample collects the first 5 processes and outputs them to a temporary CSV using Export-CSV and then uses `Start-UDDownload` to send the data to the end user.&#x20;

Note that the CSV is saved to the server using a temporary file and then read into memory using `Get-Content`. That content is then downloaded via the end user's browser.&#x20;

`-ShowLoading` is used on the button to display feedback to the user while the download is prepared.&#x20;
