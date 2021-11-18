---
description: Alert component for Universal Dashboard.
---

# Alert

Alerts provide a simple way to communicate information to a user.

## Simple Alerts

Alerts have four different severities and can include text or other content.

```
New-UDAlert -Severity 'error' -Text 'This is an error alert — check it out!' 
New-UDAlert -Severity 'warning' -Text 'This is an warning alert — check it out!'
New-UDAlert -Severity 'info' -Text 'This is an error info — check it out!' 
New-UDAlert -Severity 'success' -Text 'This is an success alert — check it out!'
```

![Alert Types](<../../../../.gitbook/assets/image (210).png>)

## Advanced Alerts

Alerts can contain any component and also a title.

```
New-UDAlert -Severity 'error' -Content { New-UDHtml 'This is an error alert — <strong>check it out!</strong>' } -Title "Error"
New-UDAlert -Severity 'warning' -Content { New-UDHtml 'This is an warning alert — <strong>check it out!</strong>' } -Title "Warning"
New-UDAlert -Severity 'info' -Content { New-UDHtml 'This is an error info — <strong>check it out!</strong>' } -Title "Info"
New-UDAlert -Severity 'success' -Content { New-UDHtml 'This is an success alert — <strong>check it out!</strong>' } -Title "Success"
```

![Advanced Alerts](<../../../../.gitbook/assets/image (211).png>)

## API

[New-UDAlert](../../../../cmdlets/New-UDAlert.txt)
