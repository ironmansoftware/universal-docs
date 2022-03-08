---
description: Role based access for dashboards.
---

# Role Based Access

{% hint style="info" %}
This feature requires a [license](../../licensing.md).
{% endhint %}

## Dashboard Roles

When dashboard authentication is enabled, you can define the role that a user must be a part of in order to access the dashboard. Roles are configured on the Settings  Security page or from within the `roles.ps1` configuration file.

![](<../../.gitbook/assets/image (134).png>)

If a user attempts to visit a dashboard that they do not have access to, they will be presented with a Not Authorized page.

![](<../../.gitbook/assets/image (135).png>)

## Pages Roles

You can also show or hide pages based on roles. To define a role for a page, use the `-Role` parameter of `New-UDPage`. Only users of the specified role will have access to this page.

```powershell
New-UDPage -Role 'Administrators' -Content {
    New-UDTypography -Text 'Admins only'
}
```

## $Roles Variable

In addition to dashboard and page roles, you can also check with roles a user is a part of by using the `$Roles` variable that is available within Dashboards. This variable contains an array of the roles that are assigned to the user.

For example, you could show the `Restart-Computer` button to only Administrators.

```powershell
if ($Roles -contains "Administrator") {
    New-UDButton -Text 'Restart Server' -OnClick {
        Restart-Computer
    }
}
```
