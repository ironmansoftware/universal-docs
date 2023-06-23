---
description: Protect sections based on roles.
---

# Protect Section

The `Protect-UDSection` cmdlet hides it's content if a user does not have the specified roles.&#x20;

```powershell
Protect-UDSection -Role @("Administrator") -Content {
   New-UDTypography -Text 'Only Administrators see this'
}
```
