---
description: Information about Universal Dashboard pages.
---

# Pages

A dashboard can consist of one or more pages. A page can have a particular name and URL. You can define a URL that accepts one or more variables in the URL to define a dynamic page. 

## Basic Page 

A basic page can be defined using the `New-UDPage` cmdlet. You could navigate to this page by visiting the `/dashboard` URL of your dashboard. 

```text
$Pages = @()
$Pages += New-UDPage -Name 'Dashboard' -Content {
    New-UDTypography -Text 'Dashboard'
}

New-UDDashboard -Title 'Pages' -Pages $Pages
```

## Dashboard with Multiple Pages

Dashboards can have multiple pages and those pages can be defined by passing an array of UDPages to `New-UDDashboard` 

```text
$Pages = @()
$Pages += New-UDPage -Name 'Dashboard One' -Content {
    New-UDTypography -Text 'Dashboard Two'
}

$Pages += New-UDPage -Name 'Dashboard Two' -Content {
    New-UDTypography -Text 'Dashboard Two'
}

New-UDDashboard -Title 'Pages' -Pages $Pages
```

You may want to organize your dashboard into multiple PS1 files. You can do this using pages. 

```text
$UDScriptRoot = $PSScriptRoot
$Pages = @()
$Pages += New-UDPage -Name 'Dashboard One' -Content {
    . "$PSScriptRoot\db1.ps1"
}

$Pages += New-UDPage -Name 'Dashboard Two' -Content {
    . "$PSScriptRoot\db2.ps1"
}

New-UDDashboard -Title 'Pages' -Pages $Pages
```

## Page with a Custom URL 

A page can have a custom URL by using the `-Url` parameter. You could navigate to this page by visiting the `/db` URL of your dashboard. 

```text
$Pages = @()
$Pages += New-UDPage -Name 'Dashboard' -Url '/db' -Content {
    New-UDTypography -Text 'Dashboard'
}

New-UDDashboard -Title 'Pages' -Pages $Pages
```

## Page with Variables in URL

You can define a page with variables in the URL to create pages that adapt based on that URL. 

```text
$Pages = @()
$Pages += New-UDPage -Name 'Dashboard' -Url '/db/:user' -Content {
    New-UDTypography -Text 'Dashboard for user: $User'
}

New-UDDashboard -Title 'Pages' -Pages $Pages
```

