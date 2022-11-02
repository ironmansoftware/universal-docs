---
description: Image component for dashboards.
---

# Image

## Image by URL

Display an image based on a URL. You can host URLs using [Published Folders](../../../../platform/published-folders.md).

```powershell
New-UDImage -Url "https://ironmansoftware.com/img/ps-logo.png"
```

## Image by Path

Display an image based on a file local to the server.&#x20;

```powershell
New-UDImage -Path C:\users\adamr\Desktop\ps-logo.png
```

## Image Size

Change the size of the image using the `-Width` and `-Height` parameters.

```powershell
New-UDImage -Url "https://ironmansoftware.com/img/ps-logo.png" -Width 250 -Height 250
```

## Attributes

Apply additional attributes to the image.&#x20;

```powershell
New-UDImage -Url "https://ironmansoftware.com/img/ps-logo.png" -Attributes @{
    alt = "Ironman Software Logo"
}
```

## API

* [New-UDImage](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDImage.txt)
